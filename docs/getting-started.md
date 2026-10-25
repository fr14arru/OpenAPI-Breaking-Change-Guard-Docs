# Primer uso

[Inicio](../README.md) · [Disponibilidad](availability.md)

Hoy puedes utilizar el código público y compilarlo. No hay todavía un ejecutable MIT publicado para descargar directamente. La comparación no necesita cuentas de producto ni infraestructura propia.

## Requisitos para compilar

- Git.
- Amazon Corretto Java 25, sin funcionalidades preview.
- Apache Maven 3.10.0. Se recomienda mvnd para acelerar compilaciones locales.
- Windows es el entorno verificado; otros sistemas siguen pendientes de validación de extremo a extremo.

Comprueba `java -version` y `mvn -version`: Maven debe utilizar el JDK 25. El IDE es opcional.

## Clonar y compilar

Desde una terminal en el directorio donde quieras guardar el proyecto:

~~~powershell
git clone https://github.com/fr14arru/openapi-guard.git
cd openapi-guard
mvn clean verify
~~~

Si ya utilizas mvnd, puedes sustituir el último comando por `mvnd clean verify`. La primera compilación necesita obtener las dependencias de Maven. No necesitas Node para compilar el motor Java.

## Ejecutar los ejemplos

Desde la raíz del proyecto compilado:

~~~powershell
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --profile=full --format=text examples/catalog/base.yaml examples/catalog/compatible.yaml
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --profile=full --format=text examples/catalog/base.yaml examples/catalog/breaking.yaml
~~~

La primera comparación devuelve código 0. La segunda devuelve 1 porque contiene rupturas deliberadas: ese resultado es correcto. Usa siempre `--profile=full` para solicitar toda la cobertura implementada; el perfil predeterminado histórico es más reducido.

## Comparar contratos propios

Sustituye las rutas ilustrativas por dos documentos OpenAPI completos que existan, en YAML o JSON UTF-8:

~~~powershell
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --profile=full --format=text --baseline="C:/Mis contratos/anterior.yaml" --candidate="C:/Mis contratos/nuevo.yaml"
~~~

Baseline es la versión anterior. Candidate es la nueva versión que estás revisando. Consulta los [límites](coverage.md), incluidos los de referencias externas.

## Guardar el informe

~~~powershell
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --profile=full --format=json --output=reports/report.json examples/catalog/base.yaml examples/catalog/breaking.yaml
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --profile=full --format=markdown --output=reports/report.md examples/catalog/base.yaml examples/catalog/breaking.yaml
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --help
java -jar target/openapi-breaking-change-guard-0.1.0-SNAPSHOT.jar --list-profiles
~~~

Los comandos incompatibles conservan el código 1 aunque guarden el informe. Los archivos de salida existentes se reemplazan: no elijas un archivo que quieras conservar. Ver [resultados y códigos](results.md).

Una vez construido, ejecutar el JAR solo necesita Java 25. Si vas a redistribuir el ejecutable o usarlo en otro repositorio, prepara el paquete completo con licencia, avisos y fuentes de terceros siguiendo [GitHub Actions](github-actions.md).
