---
title: Corrector de texto 
sidebar_position: 1
---

# Corrector de texto

El **Corrector de texto** es una herramienta que permite identificar y sugerir correcciones ortográficas o de redacción en fragmentos de texto. Su diseño modular permite la integración con múltiples proveedores de inteligencia artificial, facilitando el mantenimiento y la extensión del sistema. La arquitectura del proyecto se divide en dos grandes componentes: el **backend**, responsable del procesamiento y la comunicación con los proveedores de IA, y el **frontend**, que gestiona la interfaz de usuario y la interacción con el sistema.


## Backend 

El backend está construido con una estructura orientada a objetos que promueve la extensibilidad y la reutilización de código. A continuación, se explica la estructura basada en el siguiente diagrama:


```mermaid

classDiagram
    direction TB

    %% Clase abstracta base
    class AbstractAiProvider.php {
        <<abstract>>
        Define la lógica común para interactuar
        con modelos de IA.
    }
    AbstractAiProvider.php <-- GoogleProvider.php : extiende
    AbstractAiProvider.php <-- OpenAiProvider.php : extiende

    %% Proveedores concretos
    class GoogleProvider.php {
        Adapta la lógica base para 
        usar la API de Google.
    }
    class OpenAiProvider.php {
        Adapta la lógica base para 
        usar la API de OpenAI.
    }

    GoogleProvider.php <-- AiProviderFactory.php : registra
    OpenAiProvider.php <-- AiProviderFactory.php : registra

    %% Fábrica de proveedores
    class AiProviderFactory.php {
        Crea instancias del proveedor de 
        IA según el tipo requerido.
    }
    AiProviderFactory.php <-- CorrectorController.php : usa

    %% Controller de corrección
    class CorrectorController.php {
        Lógica backend:  Maneja la corrección 
        de texto y coordina el uso del proveedor 
        de IA.
    }

```

### Descripción técnica
- **AbstractAiProvider.php**: Clase abstracta que define una interfaz común para todos los proveedores de IA. Permite estandarizar las operaciones independientemente del proveedor específico.

- **GoogleProvider.php** y **OpenAiProvider.php**: Implementaciones concretas que adaptan la lógica para comunicarse con las APIs respectivas de Google y OpenAI.

- **AiProviderFactory.php**: Implementa el patrón Factory. Esta clase es responsable de instanciar el proveedor correspondiente según una configuración o solicitud.

- **CorrectorController.php**: Es el punto de entrada del backend. Recibe solicitudes del frontend, obtiene el texto a corregir, utiliza la fábrica para elegir el proveedor y retorna la respuesta procesada.

## Frontend

El frontend gestiona la experiencia del usuario, generando dinámicamente la interfaz del corrector, comunicándose con el backend y presentando los cambios sugeridos.

```mermaid

classDiagram
    direction TB

    class Corrector.php {
        Interfaz visual del corrector de texto; 
        funciona solo en vistas que importen 
        CorrectorAssets.php
    }

    %% View y Assets (descripciones)
    class CorrectorAssets.php {
        Carga las dependencias necesarias 
        para el funcionamiento del corrector de 
        texto
    }

    Corrector.php --> CorrectorAssets.php : importa

    %% Ficheros estáticos manejados por Assets (descripciones)
    class Corrector.js {
        Lógica frontend: Genera estructura html,
        envía texto, recibe respuestas y gestiona
        botones
    }
    class DiffPatchMatch {
        Biblioteca para calcular diferencias 
        y generar parches de texto
    }
    class Corrector.css {
        Conjuntos de estilos CSS para la visualización 
        de cambios y botones
    }

    class jQuery {
        Biblioteca JavaScript para 
        manipulación del DOM y 
        peticiones AJAX.
    }
    class MaterialIcons {
        Fuente de iconos de Material
        Design para interfaz de usuario
    }

    %% Relaciones front-end
    CorrectorAssets.php --> Corrector.js : importa
    CorrectorAssets.php --> DiffPatchMatch : importa
    CorrectorAssets.php --> Corrector.css : importa
    CorrectorAssets.php --> jQuery : importa
    CorrectorAssets.php --> MaterialIcons : importa

    MaterialIcons <-- Corrector.css : usa
    jQuery <-- Corrector.js : usa
    DiffPatchMatch <-- Corrector.js : usa

    %% Flujo AJAX
    Corrector.js <-- Corrector.css : aplica estilos

```

### Descripción técnica

- **Corrector.php**: Plantilla de vista principal del corrector. Solo se activa cuando se importan sus recursos `CorrectorAssets.php`.
- **CorrectorAssets.php**: Clase que encapsula todos los recursos necesarios del frontend (scripts, estilos, librerías).
- **Corrector.js**: Script principal que construye dinámicamente la interfaz, envía el texto ingresado al backend y presenta la respuesta del modelo.
- **DiffPatchMatch**: Biblioteca externa especializada en mostrar diferencias entre textos originales y corregidos.
- **Corrector.css**: Archivo de estilos para marcar visualmente las correcciones y demás elementos de la interfaz.
- **jQuery**: Usado para operaciones DOM y AJAX.
- **MaterialIcons**: Conjunto de íconos que mejora la experiencia visual del usuario.

## Conexión del frontend con el backend

La conexión entre ambos componentes se realiza mediante llamadas AJAX realizadas por el JavaScript del frontend hacia el controlador backend.

```mermaid

classDiagram
    direction RL

    class Corrector.js {
        Lógica frontend: Genera estructura html,
        envía texto, recibe respuestas y gestiona
        botones
    }

    CorrectorController.php <--> Corrector.js

    class CorrectorController.php {
        Lógica backend:  Maneja la corrección 
        de texto y coordina el uso del proveedor 
        de IA.
    }

```

### Descripción técnica

Cuando el usuario ingresa un texto y pulsa el botón de corrección, Corrector.js envía una solicitud AJAX al CorrectorController.php.

- El controlador procesa la solicitud, escoge el proveedor de IA adecuado mediante la AiProviderFactory.php, y devuelve la respuesta con el texto corregido.
- El frontend interpreta y muestra los cambios utilizando la biblioteca DiffPatchMatch, resaltando lo que fue corregido.