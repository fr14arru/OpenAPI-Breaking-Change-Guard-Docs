# OpenAPI Breaking Change Guard

Detecta cambios incompatibles en tus contratos OpenAPI antes de integrar una nueva versión de tu API.

OpenAPI Guard compara un contrato anterior con el contrato propuesto y explica qué cambia, por qué puede afectar a los consumidores y dónde revisar el contrato candidato. Puedes ejecutarlo en tu equipo o incorporarlo a las pull requests con GitHub Actions.

## Qué aporta

- Detecta operaciones eliminadas y cambios incompatibles en parámetros, cuerpos y esquemas.
- Distingue entre peticiones y respuestas: sus reglas de compatibilidad tienen direcciones diferentes.
- Muestra resultados en texto, JSON con sangría y Markdown.
- Incluye ubicaciones del contrato candidato cuando están disponibles.
- En GitHub Actions ofrece anotaciones, informes y un comentario opcional en la conversación de la PR.
- Permite informar de rupturas intencionadas sin fallar el check, cuando el análisis está completo.

No requiere bases de datos, Docker ni un servidor propio del usuario. La comparación se ejecuta en tu equipo o en el runner de GitHub.

## Empieza aquí

1. [Estado y disponibilidad](docs/availability.md).
2. [Primer uso con el paquete](docs/getting-started.md).
3. [Configurar GitHub Actions](docs/github-actions.md).
4. [Interpretar los resultados](docs/results.md).
5. [Cobertura y límites](docs/coverage.md).
6. [Preguntas frecuentes](docs/faq.md).

## Disponibilidad comercial

La distribución pública y el checkout están en preparación. Todavía no hay un enlace público de compra o descarga ni una versión instalable desde GitHub Marketplace.

La oferta prevista es **4,99 EUR al año por repositorio, impuestos incluidos**, para uso personal o profesional. Las condiciones definitivas se publicarán antes de abrir las ventas.

## Soporte

Producto de **Francisco Arce Ruiz**. Contacto: [rayopuyi5@gmail.com](mailto:rayopuyi5@gmail.com).

Al informar de un problema, indica la versión, el perfil, el código de salida y un ejemplo mínimo sin datos confidenciales.

Este repositorio contiene documentación de usuario. No contiene el código fuente del motor ni concede una licencia sobre él. La compatibilidad siempre se limita al perfil analizado; no certifica toda la API.
