---
title: Api Batch
---

#### Documentación oficial: https://platform.openai.com/docs/guides/batch

Se procesan trabajos de forma asíncrona con la API por lotes (Api Batch).

Esta API permite enviar grupos de solicitudes asíncronas con un costo un 50% menor, límites de tasa significativamente más altos y un plazo garantizado de resolución de 24 horas. Resulta ideal para procesar tareas que no requieren respuesta inmediata..

## Visión general

En ciertos casos no es necesaria una respuesta inmediata o los [límites de tasa](/docs/guides/rate-limits) impiden ejecutar un gran número de consultas de forma rápida. El procesamiento por lotes resulta útil en situaciones como:

1. Realización de evaluaciones
2. Clasificación de grandes conjuntos de datos
3. Generación de embeddings de repositorios de contenido

La API por lotes ofrece endpoints que permiten:

* Agrupar varias solicitudes en un único archivo `.jsonl`.
* Iniciar un trabajo de procesamiento por lotes para ejecutar dichas solicitudes.
* Consultar el estado del lote mientras se ejecuta.
* Recuperar los resultados agrupados al completarse el proceso.

Frente al uso directo de endpoints sincrónicos, esta API proporciona:

1. **Mayor eficiencia de costos:** descuento del 50 % respecto a las APIs sincrónicas.
2. **Límites de tasa superiores:** capacidad de procesamiento notablemente mayor.
3. **Tiempos de finalización garantizados:** cada lote concluye en un plazo máximo de 24 horas.

## Primeros pasos

### 1. Preparación del archivo de lote

Se crea un archivo `.jsonl` en el que cada línea describe una solicitud individual. Actualmente, los endpoints compatibles son:

* `/v1/responses` (Responses API)
* `/v1/chat/completions` (Chat Completions API)
* `/v1/embeddings` (Embeddings API)
* `/v1/completions` (Completions API)

Cada solicitud necesita un valor único en `custom_id` para permitir su identificación en los resultados. Ejemplo con dos solicitudes (modelo `gpt-3.5-turbo-0125`):

```jsonl
{"custom_id":"request-1","method":"POST","url":"/v1/chat/completions","body":{"model":"gpt-3.5-turbo-0125","messages":[{"role":"system","content":"You are a helpful assistant."},{"role":"user","content":"Hello world!"}],"max_tokens":1000}}
{"custom_id":"request-2","method":"POST","url":"/v1/chat/completions","body":{"model":"gpt-3.5-turbo-0125","messages":[{"role":"system","content":"You are an unhelpful assistant."},{"role":"user","content":"Hello world!"}],"max_tokens":1000}}
```

### 2. Subida del archivo de entrada

Al igual que con la [API de fine-tuning](/docs/guides/fine-tuning), el archivo debe subirse primero mediante la [Files API](/docs/api-reference/files), especificando `purpose="batch"`.

### 3. Creación del lote

Con el ID del archivo subido (por ejemplo, `file-abc123`), se crea el lote indicando:

* `input_file_id`: ID del archivo de entrada.
* `endpoint`: ruta del endpoint a procesar.
* `completion_window`: `"24h"`.

Opcionalmente puede agregarse `metadata` para describir el lote.

### 4. Consulta del estado

El estado del lote puede consultarse en cualquier momento mediante la recuperación del objeto Batch correspondiente. Los posibles estados incluyen: `validating`, `in_progress`, `finalizing`, `completed`, `failed`, `expired`, `cancelling` y `cancelled`.

### 5. Recuperación de resultados

Al completarse el lote, los resultados se obtienen descargando el archivo indicado en `output_file_id` mediante la Files API. Cada línea del archivo de salida es la respuesta a una solicitud del archivo de entrada; en caso de error o vencimiento, se incluye información en un archivo de errores accesible vía `error_file_id`.

### 6. Cancelación de un lote

Para cancelar un lote en curso, se invoca el endpoint de cancelación correspondiente. El estado transicionará a `cancelling` y, una vez completadas las solicitudes en vuelo, cambiará a `cancelled`.

### 7. Listado de todos los lotes

Se puede obtener un listado de todos los lotes existentes, con opciones de paginación (`limit` y `after`) para usuarios con gran cantidad de lotes.

## Disponibilidad de modelos

La API por lotes está disponible para la mayoría de los modelos, aunque no para todos. Es recomendable consultar la [referencia de modelos](/docs/models) para verificar compatibilidad.

## Límites de tasa

* **Por lote:** hasta 50 000 solicitudes y 200 MB de tamaño de archivo (`.jsonl`). Para `/v1/embeddings`, el máximo es de 50 000 entradas en total.
* **Tokens en cola por modelo:** cada modelo dispone de un límite de tokens en cola para procesamiento por lotes; puede consultarse en la página de [Configuración de la organización](/settings/organization/limits).

Estos límites son independientes de los límites estándar, por lo que no afectan el consumo de tokens de las APIs sincrónicas.

## Vencimiento de lotes

Los lotes que no concluyen en 24 horas pasan a estado `expired`; las respuestas completadas permanecen disponibles, y las pendientes se registran en el archivo de errores con código `batch_expired`.

## Recursos adicionales

Para ejemplos prácticos, se sugiere consultar **[OpenAI Cookbook: Batch Processing](https://cookbook.openai.com/examples/batch_processing)**.
