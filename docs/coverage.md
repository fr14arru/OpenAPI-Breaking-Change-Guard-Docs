# Cobertura y límites

[Inicio](../README.md)

El perfil full selecciona operations-data-response-policy-v1. Full significa toda la cobertura implementada, no todo OpenAPI.

## Qué analiza

- Retirada de rutas y métodos HTTP.
- Parámetros nuevos obligatorios y cambios de obligatoriedad.
- Obligatoriedad del cuerpo de petición y disponibilidad de sus formatos.
- Tipos escalares, enums, nullabilidad y límites numéricos o de longitud soportados.
- Propiedades, required, objetos abiertos/cerrados y proyección de readOnly/writeOnly según dirección.
- Arrays homogéneos, esquema de items y límites minItems/maxItems.
- Retirada de códigos concretos y representaciones de respuesta según la política de disponibilidad documental.

Las restricciones se consideran conjuntamente: un cambio textual no demuestra por sí solo una ruptura.

## Por qué petición y respuesta se evalúan de manera diferente

Una petición aceptada antes debe seguir siendo aceptada después. Una respuesta permitida después debe seguir siendo válida para los consumidores anteriores.

| Cambio aislado | Petición | Respuesta |
| --- | --- | --- |
| Reducir un enum | Puede romper al rechazar valores anteriores. | Restringe las salidas; normalmente compatible. |
| Ampliar un enum | Amplía las entradas; normalmente compatible. | Puede romper al permitir valores desconocidos. |
| Hacer obligatoria una propiedad opcional | Puede romper a consumidores que no la enviaban. | Refuerza su presencia; comprobar también sus demás restricciones. |

Las conclusiones presuponen esquemas soportados y satisfacibles. Las restricciones combinadas pueden modificar el resultado.

## Cuándo requiere revisión

No se certifican construcciones como composición allOf/oneOf/anyOf, patrones, additionalProperties con esquema o ciclos relevantes sin soporte suficiente.

Retirar un parámetro no demuestra por sí solo que el servidor vaya a rechazarlo: solicita revisión. Añadir códigos o representaciones de respuesta puede requerir revisión. La retirada de un código concreto sin fallback aplicable se considera ruptura por política de disponibilidad documental, no por una prueba sobre el servidor real.

Rangos de respuesta, default y negociación no resuelta pueden impedir un análisis completo. OpenAPI 3.0.x es el alcance comercial inicial; no se anuncia soporte comercial completo para 3.1.

## Facetas excluidas

El perfil declara estas facetas excluidas:

parameterSerialization, formatAssertions, requestEncoding, responseNegotiation, responseHeaders, responseLinks, security, servers, callbacks, webhooks.

Una exclusión no certifica que esos aspectos sean compatibles. Una construcción no soportada que afecte a los datos comprometidos obliga a revisión.

Las referencias externas, a otros archivos o remotas, no se resuelven. Usa documentos autocontenidos con referencias internas soportadas. El límite de entrada es 5 MiB por contrato y los documentos deben ser UTF-8.

La comparación no ejecuta tu API ni sustituye las pruebas funcionales o de seguridad.
