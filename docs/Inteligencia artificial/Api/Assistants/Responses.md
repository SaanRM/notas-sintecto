---
title: /v1/chat/responses
---

## `/v1/chat/responses`
Este endpoint se usa en el **flujo de conversación** de la Assistants API, para **generar respuestas** dentro de una conversación (thread).

El flujo completo incluye:

1. **Crear un asistente** → `/v1/assistants`
2. **Crear un thread** (una conversación) → `/v1/threads`
3. **Agregar un mensaje** al thread → `/v1/threads/{thread_id}/messages`
4. **Solicitar una respuesta** (run) → `/v1/threads/{thread_id}/runs`
5. **Obtener la respuesta** → `/v1/threads/{thread_id}/messages` o monitorear el run

El paso de **generar la respuesta** en este flujo es donde entra `/v1/chat/responses`, aunque este endpoint **no suele usarse directamente**, sino a través de la gestión de threads y runs.
