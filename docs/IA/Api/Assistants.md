---
title: Assistants
---

## `/v1/assistants`
Este endpoint **define o administra asistentes**. Es decir:

- Crea un nuevo asistente.
- Recupera, edita o elimina asistentes existentes.

Un **asistente** es un objeto que tiene:
- Un modelo (por ejemplo, `gpt-4-turbo`).
- Instrucciones base (como un system prompt).
- Herramientas que puede usar (funciones, código, archivos, etc.).

Este endpoint **no genera respuestas**, solo configura el "perfil" del asistente.
