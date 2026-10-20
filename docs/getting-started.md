# Primer uso

[Inicio](../README.md) · [Disponibilidad](availability.md)

Esta guía describe el paquete preparado para distribución. Su descarga pública sigue pendiente; no necesitas acceso al repositorio privado del motor. No hay que compilar el producto.

## Requisitos locales

- Java 25; Amazon Corretto 25 es la distribución de referencia.
- Dos contratos OpenAPI completos en YAML o JSON, guardados como UTF-8.
- Windows es el entorno verificado. Otros sistemas siguen pendientes de validación de extremo a extremo.

## Ejecutar una comparación

1. Obtén el ZIP a través del canal oficial cuando esté disponible.
2. Extrae la carpeta completa. Conserva licencias, atribuciones y fuentes de terceros junto al ejecutable.
3. Abre una terminal en la carpeta extraída.
4. Comprueba Java:

~~~powershell
java -version
~~~

5. Ejecuta el ejemplo incompatible incluido:

~~~powershell
java -jar guard.jar --profile=full --format=text examples/base.yaml examples/breaking.yaml
~~~

Ese ejemplo devuelve código 1 porque contiene una ruptura deliberada. No significa que la herramienta se haya averiado.

Para usar contratos propios, sustituye estas rutas ilustrativas por archivos que existan:

~~~powershell
java -jar guard.jar --profile=full --format=text --baseline="C:/Mis contratos/anterior.yaml" --candidate="C:/Mis contratos/nuevo.yaml"
~~~

Baseline es la versión anterior. Candidate es la nueva versión que estás revisando.

## Guardar y automatizar

~~~powershell
java -jar guard.jar --profile=full --format=json --output=reports/report.json --baseline=anterior.yaml --candidate=nuevo.yaml
java -jar guard.jar --profile=full --format=markdown --output=reports/report.md --baseline=anterior.yaml --candidate=nuevo.yaml
java -jar guard.jar --help
java -jar guard.jar --list-profiles
~~~

Los archivos de salida existentes se reemplazan. No elijas un archivo que quieras conservar como destino del informe.

Utiliza siempre --profile=full para solicitar toda la cobertura implementada. El perfil predeterminado histórico es más reducido. Consulta [códigos y resultados](results.md).

No necesitas Maven, IntelliJ ni un script PowerShell para ejecutar el JAR.
