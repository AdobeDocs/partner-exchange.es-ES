---
title: Acceso y exploración de la zona protegida de AEP
description: Obtenga información sobre cómo acceder y explorar la zona protegida de Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
TQID: https://experienceleague.adobe.com/A5sl-xNZBPjIKn6HO1iwM78IaQWQs4yBgbw9wwpMrGw
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2: id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2: id: b75843fa-0a67-4a44-a6b1-cc627b0481dcid: fef08361-6ac5-460c-93fe-d063e40b6a49
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 1%

---

# Acceso y exploración de la zona protegida de AEP

Este artículo trata sobre lo siguiente:

* Las diferencias entre una organización de zona protegida de Adobe Exchange Partner existente y la zona protegida de AEP compartida.
* Solicitud de acceso a la zona protegida compartida de AEP.
* Recepción de una invitación por correo electrónico a la zona protegida compartida de AEP.
* Invitando a nuevos usuarios en [!DNL Admin Console].
* Navegación por la IU de AEP.

Para obtener una descripción general de la tecnología de espacio aislado en AEP, consulte este [artículo](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html).

## La zona protegida compartida de AEP

Los socios de Exchange reciben acceso a varios productos de Adobe [!DNL Experience Cloud] (productos que no son de AEP como [!DNL Analytics], [!DNL Target], etiquetas de Platform, etc.) a través de su propia organización de Adobe [!DNL Experience Cloud] (no compartida). A los socios se les otorgan derechos de acceso de administrador del sistema a su propia organización para administrar usuarios y otros permisos. Adobe [!DNL Experience Platform] (AEP) se trata de forma diferente que otras zonas protegidas de Adobe. Estas son las diferencias clave:

* El acceso a AEP NO se realizará a través de la organización de la zona protegida [!DNL Experience Cloud] de Adobe principal de los socios.
* El acceso a AEP se realiza mediante una organización compartida de Adobe Exchange.
* Muchas otras empresas asociadas a Adobe Exchange acceden a AEP con la misma organización
   * A través de la función de zona protegida de AEP, los datos y las actividades dentro de esta organización compartida no se pueden ver ni modificar por parte de los otros socios; cada socio tendrá acceso a una zona protegida diferente dentro de la organización compartida.
* Los derechos de administración dentro de esta organización compartida son muy limitados.
* Después de obtener acceso a una zona protegida en AEP, los socios verán dos organizaciones en el conmutador de organizaciones en la parte superior derecha de la interfaz de usuario, mientras se encuentran en la página de inicio de Admin Console o de Experience Cloud principal. Sin embargo, cuando se inicia sesión en AEP, solo debe ser visible la organización compartida.

## Solicitar acceso a la zona protegida compartida de AEP

Enviar [solicitud de asistencia](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new) con la siguiente información:

* Correo electrónico
* Asunto: Solicitud de zona protegida de AEP
* Producto: Aprovisionamiento general / Sandbox
* Tipo de vale: Soporte del programa - Programa de Exchange / Preguntas de solicitud de aprovisionamiento
* Descripción: Proporcione una breve descripción de los casos de uso de integración que requieren el uso de una zona protegida de AEP
* Asegúrese de proporcionar también todos los nombres de usuario y correos electrónicos que deben añadirse a la zona protegida de AEP. Es posible que se agreguen usuarios adicionales después de realizar la solicitud, pero Adobe deberá agregar los usuarios a través de un ticket adicional (ver a continuación).

## Recibir la invitación por correo electrónico

El contacto principal que solicitó la zona protegida de AEP recibirá un mensaje de correo electrónico automatizado invitándolos a &quot;comenzar&quot; con Adobe [!DNL Experience Platform]. El contacto principal también tendrá algunos privilegios de administración que se tratan en la siguiente sección.

En lugar de seleccionar el botón &quot;Comenzar&quot; en el correo electrónico, vaya directamente a `https://platform.adobe.com.` e inicie sesión con el Adobe ID asociado a la dirección de correo electrónico en la invitación, o cree uno si no está asociado a un Adobe ID.

## Invitar a usuarios adicionales

Enviar [solicitud de asistencia](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new) con la siguiente información:

* Dirección de correo electrónico del solicitante
* Asunto: Entorno aislado de AEP: añadir administrador/usuario
* Producto: Aprovisionamiento general / Sandbox
* Tipo de vale: Soporte del programa - Programa de Exchange / Preguntas de solicitud de aprovisionamiento
* Descripción: Lista de usuarios que se van a añadir (nombres y correos electrónicos)

## Navegación por la IU de AEP

Vea el [vídeo de introducción](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html) de la interfaz de usuario de AEP

Hay 12 áreas principales dentro de la interfaz de usuario de AEP a las que se puede navegar mediante el panel izquierdo. Sin embargo, las secciones más importantes para este tipo de integración son Esquemas, Conjuntos de datos y Perfiles.

* Inicio: la pantalla de aterrizaje

   * Sugiere algunas actividades de introducción
   * Proporciona algunos vínculos al contenido de aprendizaje
   * Proporciona una vista de panel para algunos de los objetos AEP principales, como Esquemas, Conjuntos de datos y Perfiles

* Flujos de trabajo: inicie flujos de trabajo comunes para introducir datos en AEP
* Conexiones/fuentes: administrar las fuentes de datos que llegan a AEP
* Conexiones / Destinos: administre las conexiones para enviar datos a sistemas externos
* Perfiles: vea y administre perfiles de cliente individuales
* Segmentos: examine, cree y modifique segmentos de clientes
* Identidades: examine, cree y modifique áreas de nombres de identidad; estos son los tipos de ID principales que se utilizan para identificar a un cliente de forma exclusiva
* Modelos (ciencia de datos): Participe en actividades de ciencia de datos, incluido el uso de un entorno Jupyter Notebooks integrado
* Servicios (ciencia de datos): publicar fórmulas de ciencia de datos como servicios
* Esquemas: examinar, crear y modificar esquemas; estas son las definiciones de datos detalladas utilizadas para mantener organizados los datos
* DataSets: examine, cree y administre DataSets; un DataSet se define mediante un esquema y es donde residen los datos en AEP
* Consultas: examine, cree, modifique y utilice un repositorio de consultas para obtener información de los datos de DataSets
* Monitorización: vea el estado de todos los datos que entran y salen de AEP tanto para el lote como para la transmisión
