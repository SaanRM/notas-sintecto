---
title: 2. Asistentes (Estructurada)
sidebar_position: 2
---

:::note
**Nota:** El Assistants API será reemplazado por el **Responses API**, que será gratuito para desarrolladores hasta mediados de 2026.
:::

La API de **Asistentes** permite definir y reutilizar un conjunto persistente de instrucciones, herramientas y archivos, simplificando la integración de modelos en aplicaciones complejas. A diferencia del flujo manual con prompts, aquí se centraliza toda la configuración en un solo objeto llamado “asistente”, el cual se crea una vez y se puede invocar múltiples veces con entradas nuevas (llamadas _threads_).

- El contexto no necesita reenviarse en cada solicitud, ya que el asistente lo conserva internamente.
- El comportamiento es más consistente, ya que las instrucciones del sistema no cambian entre ejecuciones.
- Se pueden asociar herramientas como **retrieval**, **code interpreter** y funciones personalizadas.

## Facturación

Los tokens de entrada y salida se facturan igual que en un flujo de prompts estándar, según el modelo utilizado.  
Adicionalmente, si se activan herramientas opcionales, pueden aplicarse costes extra:

| Funcionalidad         | Coste adicional                       |
|--|--|
| Retrieval             | \$0.20 / GB / día                     |
| Code Interpreter      | Tarifa por tiempo de ejecución activa |

## Ejemplo de ejecución con Assistants API

En este caso se utilizó un asistente previamente configurado para responder a dos entradas similares:

> Aunque no se muestra en la imagen, en cada ejecución también se incluye automáticamente un mensaje de sistema con las instrucciones del asistente. Ese mensaje cuenta como parte de los tokens de entrada, del mismo modo que ocurre al usar un flujo de prompts normales.

![Ejemplo de ejecución con Assistants API](image.png)

| Ejecución | Tokens de entrada | Tokens de salida | Total de tokens |
|--|--|--|--|
| **1**     | 915               | 176              | **1.091**        |

> La respuesta fue comparable a la obtenida en un flujo manual, pero sin necesidad de reenviar instrucciones ni contexto manualmente.

## Conclusión

El uso de asistentes permite mantener instrucciones persistentes y construir flujos más organizados y reutilizables. Es especialmente útil cuando se desea mantener consistencia en el comportamiento o trabajar con herramientas especializadas integradas al modelo.
