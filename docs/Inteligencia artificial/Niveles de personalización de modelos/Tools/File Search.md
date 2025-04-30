---
title: File Search (Búsqueda de archivos)
---


## ¿Qué es File Search?

File Search es una herramienta que permite cargar documentos (por ejemplo, PDFs, archivos Word, TXT) para que el modelo de OpenAI pueda buscar y recuperar automáticamente fragmentos relevantes en función de una consulta.  
A diferencia del enfoque manual, en el cual es necesario copiar y pegar el contenido directamente en el prompt, File Search indexa los documentos y realiza búsquedas inteligentes sobre ellos.  
Esta funcionalidad resulta especialmente útil para gestionar grandes volúmenes de información o múltiples documentos, permitiendo una recuperación de datos más eficiente y precisa.

## Metodología de comparación

La comparación se realiza considerando los siguientes factores:
- Costos asociados (subida, procesamiento y recuperación de información).
- Complejidad de uso (manual vs. automatizado).
- Escenarios ideales de aplicación según el tamaño de los documentos.
- Estimaciones de costos prácticos utilizando un archivo ejemplo.
- Recomendaciones de uso basadas en tipo y tamaño de documentos.

## 2. Tabla Comparativa: Texto manual vs. File Search

| Aspecto | Copiar/pegar texto en el prompt | Utilizar File Search |
|:---|:---|:---|
| **Costo de subida** | No aplica | Gratuito |
| **Costo por tokens de entrada** | ~USD $0.003 por 1,000 tokens | ~USD $0.003 por 1,000 tokens |
| **Costo adicional** | No aplica | USD $0.20 por 1,000 tokens recuperados |
| **Ideal para** | Archivos pequeños o medianos (menos de 100,000 tokens) | Archivos grandes, múltiples documentos o necesidad de búsquedas automáticas |
| **Complejidad** | Manual (copiar y pegar) | Automática (recuperación inteligente) |
| **Límite práctico** | Hasta ~100,000 tokens (con GPT-4-turbo-128k) | Sin límite práctico; fragmenta y recupera según necesidad |

## 3. Ejemplo práctico: Costos estimados para un PDF de 50 páginas

| Concepto | Valor |
|:---|:---|
| **Tamaño estimado** | ~25,000 tokens |
| **Costo utilizando copiar/pegar** | ~USD $0.075 |
| **Costo utilizando File Search** | ~USD $5.075 |
| **Diferencia** | File Search resulta aproximadamente 67 veces más costoso en este escenario |

## 4. Recomendaciones de uso según el escenario

| Escenario | Opción recomendada |
|:---|:---|
| Documento corto (1–20 páginas) | Copiar/pegar directamente en el prompt |
| Documento medio (20–80 páginas) | Depende: copiar/pegar si entra en el contexto, fragmentar si excede |
| Documento largo (100+ páginas o múltiples documentos) | Utilizar File Search |
| Necesidad de búsquedas inteligentes o contenido desconocido | Utilizar File Search |

## 5. Notas adicionales

- La carga de archivos en File Search es gratuita.
- Se incurre en costos únicamente al recuperar fragmentos durante una consulta.
- Cuanto más general o amplia sea la consulta, mayor cantidad de tokens serán recuperados y, por tanto, mayor será el costo.
- File Search ofrece mejores resultados cuando los documentos tienen una estructura clara y bien organizada.

✅ **Resumen Final**  
Para optimizar los costos en el uso de OpenAI Assistants:
- Para documentos pequeños, se recomienda copiar/pegar el contenido directamente.
- Para documentos grandes o múltiples archivos, File Search es conveniente solo si es necesario realizar búsquedas inteligentes.
