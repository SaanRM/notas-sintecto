---
title: 🛠 Tools 
---

## 1. ¿Qué son las Tools en los Assistants?

- Las **Tools** son funciones especiales que amplían las capacidades de un Asistente de OpenAI.
- Permiten, por ejemplo:
  - Buscar en archivos (`File Search`)
  - Ejecutar código (`Code Interpreter`)
  - Llamar APIs externas (`Function Calling`)
- Las Tools se activan al **configurar un Assistant** desde el **OpenAI Platform Dashboard** (https://platform.openai.com/).

---

## 2. Tabla Comparativa: Uso de texto manual vs. File Search

| Aspecto | Pegar texto manualmente en prompt | Usar Tool: File Search |
|:---|:---|:---|
| **Costo de subida** | No aplica | Gratis |
| **Costo por tokens de entrada** | ~$0.003 por 1,000 tokens | ~$0.003 por 1,000 tokens |
| **Costo adicional** | No | **$0.20 por 1,000 tokens recuperados** |
| **Ideal para** | Archivos pequeños o medianos (menos de 100k tokens) | Archivos grandes, múltiples documentos, necesidad de búsqueda automática |
| **Complejidad** | Manual (copiar/pegar) | Automático (busca por ti) |
| **Límite práctico** | Hasta ~100,000 tokens (con GPT-4-turbo-128k) | No hay límite práctico en tamaño (fragmenta y busca) |

---

## 3. Ejemplo Real: Costos estimados para un archivo PDF de 50 páginas

| Concepto | Valor |
|:---|:---|
| **Tamaño estimado** | ~25,000 tokens |
| **Costo pegando texto** | ~$0.075 USD |
| **Costo usando File Search** | ~$5.075 USD |
| **Diferencia** | **File Search es ~67 veces más caro** en este escenario |

---

## 4. ¿Dónde usar cada opción?

| Escenario | Recomendación |
|:---|:---|
| Documento corto (1–20 páginas) | Pegar directamente en el prompt |
| Documento medio (20–80 páginas) | Depende: Si entra en el contexto, pegarlo; si no, considerar fragmentarlo |
| Documento largo (100+ páginas o varios documentos) | Usar File Search |
| Necesidad de búsquedas inteligentes (no sabes qué parte usar) | Usar File Search |

---

## 5. Notas Adicionales

- **Subir archivos a File Search es gratis.**  
  Solo se paga si se **recupera información** de ellos durante una consulta.
- **Recuperar más fragmentos aumenta el costo.**  
  Si haces preguntas muy generales o amplias, más tokens serán recuperados.
- **File Search funciona mejor si el contenido está bien estructurado.**

---

# ✅ Resumen Final

> Para maximizar costos en OpenAI Assistants:  
> - **Textos chicos →** copiar/pegar.  
> - **Textos grandes/múltiples archivos →** usar `File Search` solo cuando sea necesario.
