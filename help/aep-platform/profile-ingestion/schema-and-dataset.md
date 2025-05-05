---
title: Creación de esquemas y conjuntos de datos de AEP
description: Cree esquemas y conjuntos de datos en Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 10%

---

# Creación de esquemas y conjuntos de datos

Se hace referencia a la [colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) en todo el artículo mediante las llamadas asociadas por número. Encontrará más información sobre cómo instalar y usar la colección Postman en la página de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). También hay conjuntos de datos de ejemplo de [lealtad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y datos de [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Esquemas

Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. En un nivel superior, los esquemas proporcionan una definición abstracta de un objeto del mundo real (como una persona) y describen qué datos deben incluirse en cada instancia de ese objeto (como nombre, apellido, cumpleaños, etc.). Los esquemas se pueden crear en la interfaz de usuario o mediante las API [!DNL Experience Platform].

Consulte [esta documentación](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) para obtener más detalles.

### Creación de un esquema

Los socios pueden crear un esquema mediante la interfaz de usuario si siguen este [tutorial](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/tutorials/create-schema-ui.html). Este ejemplo utiliza el esquema de perfil del programa de fidelización. Aunque el ejemplo es un esquema de perfil, los esquemas basados en eventos se pueden utilizar con un proceso similar.

Para usar las API, los socios deben tener una integración de Adobe I/O existente con permisos de [!DNL Experience Platform] habilitados. Consulte esta guía para [crear una integración de E/S](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

A continuación, visite [este vínculo](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/tutorials/create-schema-api.html) para aprender a crear esquemas mediante la API.

Para crear un esquema mediante Postman, utilice las llamadas contenidas en folders 1: Create Schema, 1a: Create Schema for PROFILE data O 1b: Create Schema for EVENT data.

## Conjuntos de datos

Todos los datos introducidos en el Adobe [!DNL Experience Platform] están contenidos en conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

El servicio de catálogo es el sistema de registro para la ubicación y el linaje de datos dentro de [!DNL Experience Platform], y se usa para crear y administrar conjuntos de datos. El catálogo rastrea los metadatos de cada conjunto de datos, que incluyen una referencia al esquema del Modelo de datos de experiencia (XDM) al que se ajusta el conjunto de datos (explicado en la siguiente sección) y el número de registros ingeridos en ese conjunto de datos.

Vaya [aquí](https://docs.adobe.com/content/help/es-ES/experience-platform/catalog/datasets/overview.html) para ver una descripción general detallada del conjunto de datos.

### Crear un conjunto de datos

![Creando Conjunto De Datos Gif Animado](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Cree un conjunto de datos a través de la IU:

1. Haga clic en **[!UICONTROL Crear conjunto de datos]**.

1. Haga clic en **[!UICONTROL Crear a partir del esquema]**.

1. Haga clic en **[!UICONTROL Finalizar]**.

Vaya [aquí](https://docs.adobe.com/content/help/es-ES/experience-platform/catalog/datasets/user-guide.html) para obtener una guía de usuario del conjunto de datos.

[Crear un conjunto de datos mediante las API](https://docs.adobe.com/content/help/es-ES/experience-platform/catalog/datasets/create.html).

Para crear un conjunto de datos a través de Postman, utilice las carpetas 2: Crear conjunto de datos, 2a: Crear conjunto de datos para datos de PERFIL O 2b: Crear conjunto de datos para datos de EVENTO.

## Prácticas recomendadas de esquemas y conjuntos de datos para socios

* Los datos del socio deben utilizar un esquema de perfil independiente en lugar de crear un mix-in para el esquema de perfil y el esquema de experiencia existentes de un cliente.
* Los socios deben utilizar clases de Adobe y mezclas siempre que sea posible.
* Los socios deben cargar sus datos mediante un conjunto de datos independiente en lugar de intentar combinar sus datos en uno existente.
* Por ahora, los socios no pueden cargar sus esquemas en el registro global.
