---
title: Conexión Apis IA
sidebar_position: 1
---

## Backend 

El backend está construido con una estructura orientada a objetos que promueve la extensibilidad y la reutilización de código. A continuación, se explica la estructura basada en el siguiente diagrama:


```mermaid

classDiagram
    direction TB

    %% Clase abstracta base
    class AbstractAiProvider.php {
        <<abstract>>
        Define la lógica común para 
        interactuar con modelos de IA y 
        almacenar el uso en logs.
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
    AiProviderFactory.php <-- Controller.php : usa

    %% Controller de corrección
    class Controller.php {
        Cualquier controlador que necesite usar
        servicios de IA en la nube fácilmente
    }

```