# OpenAPI Breaking Change Guard

Detecta cambios incompatibles en contratos OpenAPI antes de integrar una nueva versión de tu API. La comparación se ejecuta en tu equipo o en el runner de GitHub.

**Código abierto y gratuito bajo MIT:** [repositorio del proyecto](https://github.com/fr14arru/openapi-guard) · [licencia del código](https://github.com/fr14arru/openapi-guard/blob/main/LICENSE) · [contribuir](https://github.com/fr14arru/openapi-guard/blob/main/CONTRIBUTING.md).

No necesitas comprar una licencia, crear una cuenta de producto ni activar una suscripción. Se puede usar para proyectos personales o profesionales; las bibliotecas conservan sus licencias. Las aportaciones económicas serán voluntarias y su enlace todavía está pendiente.

## Qué aporta

- Operaciones eliminadas y cambios incompatibles en parámetros, cuerpos y esquemas.
- Reglas que distinguen peticiones y respuestas.
- Informes en texto, JSON con sangría y Markdown, con ubicaciones del candidato cuando están disponibles.
- Anotaciones, informes y comentario opcional en la conversación de la PR.
- Política para permitir rupturas intencionadas cuando el análisis está completo.

No requiere base de datos, Docker ni un servidor propio. La compatibilidad se limita al perfil analizado: no certifica toda la API.

## Empieza aquí

1. [Primer uso: clonar, compilar y comparar](docs/getting-started.md).
2. [Configurar GitHub Actions](docs/github-actions.md).
3. [Interpretar los resultados](docs/results.md).
4. [Cobertura y límites](docs/coverage.md).
5. [Estado y próximos pasos](docs/availability.md).
6. [Preguntas frecuentes](docs/faq.md).

El código ya es público. La release binaria MIT y la instalación de la Action por versión siguen pendientes; hoy puedes compilar desde el código y preparar un paquete local para tu workflow.

## Colaborar

Abre una [issue](https://github.com/fr14arru/openapi-guard/issues) con versión, perfil, código de salida y un ejemplo mínimo anonimizado, o contribuye mediante fork y PR. No adjuntes secretos ni contratos confidenciales. Contacto público: [rayopuyi5@gmail.com](mailto:rayopuyi5@gmail.com).

Este repositorio contiene documentación de usuario bajo [MIT](LICENSE). La documentación técnica y el código están en el repositorio del proyecto. El soporte es comunitario, sin SLA ni plazos garantizados.
