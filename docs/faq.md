# Preguntas frecuentes

[Inicio](../README.md)

## ¿Necesito el código fuente o compilar el proyecto?

No. Se utiliza el paquete distribuido. Para la CLI local necesitas Java 25; Maven es una herramienta del desarrollo del producto.

## ¿Puedo permitir una ruptura intencionada?

Sí. Configura fail-on-breaking: 'false'. El informe conserva la ruptura y el check puede pasar cuando el análisis es completo. Los errores y la revisión pendiente siguen fallando.

## ¿Un check verde garantiza toda la API?

No. El alcance depende del perfil, la cobertura y la política de bloqueo. Revisa el informe y sus exclusiones.

## ¿Por qué no aparece un comentario en la PR?

Comprueba pr-comment: 'true', el permiso pull-requests: write y que la PR pertenezca al mismo repositorio. Los forks y eventos distintos de pull_request omiten el comentario. Las políticas de tu organización también pueden impedirlo.

## ¿Por qué falla al abrir anterior.yaml?

Ese nombre es ilustrativo: debe existir el archivo en la ruta desde la que ejecutas el comando. Comprueba ruta, permisos, UTF-8 y tamaño. Si la entrada no puede leerse, no se ha comparado el contrato.

## ¿Puedo comparar un contrato dividido en archivos?

El perfil actual no resuelve referencias externas. Prepara un documento autocontenido antes de compararlo; la herramienta no descarga referencias ni elige una utilidad de empaquetado por ti.

## ¿Se envían mis contratos a un servidor del producto?

La comparación se ejecuta en tu equipo o runner. La instalación de Java y las funciones de GitHub requieren sus conexiones propias. Si activas el comentario o publicas artefactos, compartes sus informes con quienes tengan acceso a la PR o ejecución: revisa si contienen información sensible.

## ¿Dónde informo de un problema?

Escribe a rayopuyi5@gmail.com con versión, perfil, código de salida y un ejemplo mínimo anonimizado. No incluyas tokens, secretos ni contratos privados de terceros.

## ¿Dónde compro o descargo?

Consulta [disponibilidad](availability.md). Los enlaces oficiales se añadirán cuando la distribución esté preparada.
