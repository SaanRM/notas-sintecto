---
title: Solicitud Ajax con CHtml::link
---

# Uso de Ajax en Yii 1

## ¿Qué es AJAX?

AJAX (Asynchronous JavaScript And XML) permite enviar y recibir información entre el navegador y el servidor **sin recargar toda la página**. Esto mejora mucho la experiencia del usuario, haciendo la aplicación más rápida y dinámica.

## ¿Cómo funciona AJAX en Yii 1?

Yii 1 facilita el uso de AJAX gracias a helpers como `CHtml::link()` o `CHtml::ajax()`, que permiten definir la lógica de envío y recepción directamente desde la vista.


# Ejemplo práctico: Obtener datos con AJAX

### ¿Qué hace este ejemplo?

Cuando se hace clic en un enlace, se envía una solicitud AJAX al servidor, el servidor devuelve información (en formato JSON), y esa información **se muestra automáticamente en la página** sin recargarla.


## Código de ejemplo

### 1. Vista (link que dispara el AJAX)

```php
<?php
echo CHtml::link('Obtener Datos', '#', array(
    'ajax' => array(
        'type' => 'POST', // tipo de petición (POST o GET)
        'url' => Yii::app()->createUrl('site/obtenerDatos'), // acción del controlador
        'data' => array('parametro' => 'valor'), // datos enviados
        'dataType' => 'json', // esperamos una respuesta en JSON
        'success' => 'function(data) {
            // mostramos la respuesta en elementos HTML
            $("#miElemento").text(data.mensaje);
            $("#otroElemento").append("<li>" + data.item + " (" + data.otroDato + ")</li>");
        }',
        'error' => 'function() {
            alert("Ocurrió un error al obtener los datos.");
        }'
    ),
));
?>
```

```html
<!-- Elementos donde se mostrará la información -->
<div id="miElemento"></div>
<ul id="otroElemento"></ul>
```

---

### 2. Controlador (respuesta a la petición AJAX)

```php
public function actionObtenerDatos() {
    if (Yii::app()->request->isAjaxRequest) {
        $param = Yii::app()->request->getPost('parametro'); // recibe el dato enviado
        $respuesta = array(
            'mensaje' => 'Dato recibido: ' . CHtml::encode($param),
            'item' => 'Elemento nuevo',
            'otroDato' => 123
        );
        echo CJSON::encode($respuesta); // responde en formato JSON
        Yii::app()->end(); // detiene la ejecución
    } else {
        throw new CHttpException(400, 'Petición inválida.');
    }
}
```

