# Interpretar los resultados

[Inicio](../README.md)

El informe distingue entre el veredicto de compatibilidad y el estado del análisis.

| Veredicto | Significado |
| --- | --- |
| COMPATIBLE | Compatible dentro del perfil y la cobertura declarados. |
| BREAKING | Se ha demostrado al menos una ruptura dentro del perfil. |
| INDETERMINATE | No se puede concluir la compatibilidad. |

| Estado | Significado |
| --- | --- |
| COMPLETED | El análisis comprometido por el perfil se completó. |
| PARTIAL | Hay aspectos relevantes que requieren revisión. |
| FAILED | No se pudo completar por un error de entrada o ejecución. |

Una ruptura demostrada puede coexistir con análisis parcial. No interpretes BREAKING como prueba de que se ha analizado todo.

## Códigos del proceso

| Código | Significado |
| --- | --- |
| 0 | Compatible dentro del perfil. |
| 1 | Ruptura detectada; revisa también el estado y los diagnósticos. |
| 2 | Entrada inválida o error de ejecución. |
| 3 | Revisión necesaria sin una ruptura demostrada que determine el código 1. |

## Ubicaciones

El texto muestra un hallazgo por línea, con regla, motivo, operación y posiciones candidatas cuando existen. Ejemplo ilustrativo:

~~~text
Error 1 - Lines 9 | [ERROR] PARAMETER_BECAME_REQUIRED | GET /pets | The parameter limit in query becomes required. | C:/Contracts/new.yaml:9:7 | L9: required: true
~~~

- Las posiciones empiezan en 1 y corresponden a la revisión analizada.
- Una referencia interna puede mostrar tanto el uso como la definición en el contrato candidato.
- Si se eliminó un elemento, se señala un contenedor candidato existente; no se inventa una línea del elemento desaparecido.
- Las posiciones son ayudas de navegación y contexto, no un diff exacto.
- Para un archivo ilegible no hay una línea que señalar. El diagnóstico identifica la entrada que falló, incluso si es el contrato anterior.
- Que una ruta sea clicable depende del editor o terminal.

## En GitHub

Consulta el comentario de la PR, las anotaciones del check y los artefactos report.json y summary.md.

Con fail-on-breaking: 'false', un check verde puede contener un resultado BREAKING: la política permite integrar la ruptura. Los errores y la revisión pendiente siguen fallando. No se eluden otras protecciones de la rama.

Los mensajes de la herramienta están en inglés. Los nombres y fragmentos de tus contratos conservan Unicode. JSON es el formato para automatización.
