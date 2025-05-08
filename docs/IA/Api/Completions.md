---
title: Completions
---

> **Descripción**  
> Se trata de un endpoint que posibilita interacciones directas con un modelo de lenguaje (por ejemplo, `gpt-4`, `gpt-4-turbo`, `gpt-3.5-turbo`, etc.) mediante el envío de un array de mensajes estructurados (`system`, `user`, `assistant`).

### ¿Para qué sirve?

- Para enviar un prompt organizado como una secuencia de mensajes.  
- Para recibir la respuesta generada por el modelo junto con el detalle de uso de tokens.

### ¿Cuándo usarlo?

- Cuando se requiera control total del contexto de la conversación.  
- En tareas breves o sencillas que no involucren dependencias externas.  
- En aplicaciones ligeras que integren de forma directa un modelo conversacional.  
- Siempre que no sea necesario mantener estado persistente ni emplear herramientas externas.

### Limitaciones

- No conserva contexto entre llamadas.  
- No gestiona estado ni archivos de manera automática.  
- No admite lógica de ejecución por turnos (no equivale a la Assistants API).

### Ejemplo de solicitud

```http
POST https://api.openai.com/v1/chat/completions
Content-Type: application/json
Authorization: Bearer YOUR_API_KEY
```

```json title="Cuerpo de la solicitud"
{
  "model": "gpt-4",
  "messages": [
    { "role": "system",  "content": "Eres un asistente útil." },
    { "role": "user",    "content": "¿Cuál es la capital de Francia?" }
  ]
}
```

### Ejemplo de respuesta

```json title="Respuesta exitosa"
{
  "id": "chatcmpl-BS5roVqqmIyPiJJCbV119IYscZ8v6",
  "object": "chat.completion",
  "created": 1746035436,
  "model": "gpt-4.1-nano-2025-04-14",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "París",
        "refusal": null,
        "annotations": []
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 18,
    "completion_tokens": 1,
    "total_tokens": 19,
    "prompt_tokens_details": { "cached_tokens": 0, "audio_tokens": 0 },
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "audio_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "service_tier": "default",
  "system_fingerprint": "fp_eede8f0d45"
}
```