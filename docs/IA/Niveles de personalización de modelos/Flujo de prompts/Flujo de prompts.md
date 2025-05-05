---
title: 1. Flujo de prompts (Básico)
sidebar_position: 1
---

Este nivel de personalización se basa en la interacción manual y directa con el modelo, sin componentes persistentes por defecto (aunque pueden implementarse con programación). Ofrece máxima flexibilidad al permitir ajustar el rol, el contexto y las herramientas en cada solicitud, pero también implica que todas las instrucciones deben repetirse en cada llamada, por eso, se considera la opción más «básica» frente a alternativas como la Assistants API o el Fine-tuning.

En un flujo de prompts manual:

1. Cada llamada a la API de OpenAI (`/v1/chat/completions`) se procesa de forma aislada, sin conservar automáticamente el estado entre peticiones.

2. El contexto completo de la conversación (instrucciones del sistema, mensajes del usuario y respuestas del asistente) debe reenviarse explícitamente como un array de objetos con `role` y `content`. Si no se incluyen mensajes anteriores, el modelo no tendrá conocimiento de ese historial.

3. La respuesta de la API incluye un desglose del uso de tokens:
   - `prompt_tokens`: tokens usados en los mensajes de entrada.
   - `completion_tokens`: tokens generados por el modelo en la respuesta.
   - `total_tokens`: suma de ambos, base para la facturación.

4. El coste se calcula a partir de `total_tokens` según la tarifa vigente del modelo elegido.

5. Cada modelo tiene un límite de tokens de contexto tanto de entrada como de salida (por ejemplo, 4 096 o 32 768 tokens). Si el conjunto de mensajes supera ese límite, debe resumirse o recortarse antes de enviar la solicitud.


## Cómo se calculan los tokens en `/v1/chat/completions`

Cada llamada a la API (`POST /v1/chat/completions`) convierte a tokens:

1. **Entrada**: Todo el contenido enviado, mensaje de instrucciones (opcional), historial previo (opcional) y mensaje actual.
2. **Salida**: Todo el texto que devuelve el modelo.

El coste total de la llamada es la suma de ambos. (Tokens de entrada + Tokens de salida)

## Ejemplo de un mismo chat en dos llamadas

### 1. Primera llamada

![Contexto inicial y primera respuesta](image-1.png)

| Llamada   | Tokens de entrada | Tokens de salida | Total de tokens |
|:---------:|:-----------------:|:---------------:|:-----:|
| **1**     | 421               | 26              | 447   |

<br/>

### 2. Segunda llamada

![Contexto ampliado y segunda respuesta](image.png)

| Llamada   | Tokens de entrada | Tokens de salida | Total de tokens |
|:---------:|:-----------------:|:---------------:|:-----:|
| **2**     | 457               | 127             | 584   |

<br/>

## **Total de tokens usados en ambas llamadas:**  
> 447 + 584 = **1 031 Tokens**

<br/>

## ¿Por qué crece el conteo?

- Cada llamada reenvía _todo_ el historial, aunque el mensaje nuevo sea breve.  
- Los tokens de entrada aumentan con cada interacción acumulada.  

**Conclusión:**  
La factura de tokens se genera por _cada_ token procesado (entrada + salida). Si también enviamos todo el contexto en cada petición, el coste sube linealmente con el número de mensajes anteriores.
