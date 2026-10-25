# GitHub Actions: revisión de contratos en una PR

[Inicio](../README.md) · [Resultados](results.md)

Esta guía utiliza el paquete local. La instalación desde una Action pública por referencia todavía está pendiente.

## 1. Incorporar el paquete

Primero sigue [primer uso](getting-started.md) para clonar y compilar el código público. Para preparar el paquete, necesitas además Node 20 o superior y PowerShell 7. Desde la raíz de openapi-guard, con el JAR ya construido:

~~~powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File scripts/prepare-evaluation.ps1 -Destination dist/local-action
node scripts/verify-package.mjs dist/local-action
~~~

El parámetro Bypass se limita a ese proceso; no cambia la política de ejecución del sistema. El destino debe ser nuevo: si ya existe, elige otro para no sobrescribirlo. El script conserva su nombre histórico, pero incluye MIT para el código propio y las licencias, avisos y fuentes correspondientes de terceros. No publica nada ni genera una release.

Copia **todo el contenido** de dist/local-action a una carpeta .guard-action en la raíz de tu repositorio consumidor. Deben quedar .guard-action/action.yml, .guard-action/guard.jar, .guard-action/manifest.json, los scripts y las atribuciones. No copies el directorio padre con otro nivel de anidamiento.

Conserva todos sus archivos. No copies únicamente el JAR ni mezcles versiones.

Añade esta línea a .gitattributes, conservando las que ya existan:

~~~gitattributes
.guard-action/** -text
~~~

## 2. Añadir el workflow

Guarda el siguiente contenido en .github/workflows/openapi-guard.yml. Si tus contratos no están en contracts/, cambia contracts-root por su directorio relativo.

~~~yaml
name: OpenAPI contract review

on:
  pull_request:
  merge_group:
    types: [checks_requested]

permissions:
  contents: read
  pull-requests: write

concurrency:
  group: openapi-guard-${{ github.workflow }}-${{ github.event.pull_request.number || github.ref }}
  cancel-in-progress: true

jobs:
  guard:
    name: OpenAPI contract guard
    runs-on: windows-latest
    timeout-minutes: 20
    steps:
      - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1
        with:
          fetch-depth: 0
          persist-credentials: false

      - id: guard
        uses: ./.guard-action
        with:
          contracts-root: contracts
          pr-comment: 'true'
          fail-on-breaking: 'false'

      - name: Retain comparison reports
        if: always() && steps.guard.outputs.report-path != ''
        uses: actions/upload-artifact@cf430e030ddbb5b0abf93d22962f4752f3646cd9
        with:
          name: openapi-guard-reports
          if-no-files-found: error
          retention-days: 7
          path: |
            ${{ steps.guard.outputs.report-path }}
            ${{ steps.guard.outputs.summary-path }}
~~~

La Action prepara Corretto 25. No necesitas Maven ni un token personal. Este ejemplo usa Windows, el entorno contrastado actualmente.

El permiso pull-requests: write se usa para el comentario en la conversación. Para desactivarlo, usa pr-comment: 'false' y retira ese permiso.

## 3. Abrir una PR de prueba

Incorpora primero un contrato base, el paquete y el workflow a la rama principal de tu proyecto por su proceso habitual. Después abre una PR con un cambio de contrato.

Verás el comentario del bot en Conversation, las anotaciones en Checks y report.json/summary.md en los artefactos de la ejecución.

Con fail-on-breaking: 'false' se permiten rupturas demostradas cuando el análisis es completo. Para fallar el check por rupturas, utiliza 'true'. Para impedir el merge debes exigir ese check mediante las protecciones de tu repositorio.

Los valores predeterminados de la Action son más estrictos: fail-on-breaking es 'true' y pr-comment es 'false'. Copia el workflow completo para obtener el comportamiento de esta guía.

## Límites y resolución de problemas

- Los contratos deben estar versionados y ser documentos OpenAPI completos.
- Las PR de forks no publican el comentario; no cambies a pull_request_target para conseguir permisos.
- El permiso de escritura puede estar restringido por tu organización.
- Un fallo de publicación del comentario solicitado puede fallar el check, conservando los informes.
- Un contrato eliminado puede no tener una línea candidata que anotar: consulta el informe.
- Las posiciones se refieren a la revisión analizada, que puede ser el merge propuesto por GitHub.
- Si falla la integridad, sustituye el paquete completo y conserva .gitattributes.
- Las actualizaciones del motor requieren actualizar el paquete. Este repositorio documental no instala ni actualiza binarios.

El check no sustituye otras protecciones de la rama ni garantiza compatibilidad global.
