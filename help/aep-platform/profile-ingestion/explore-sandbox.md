---
title: Acceso y exploración de la zona protegida de AEP
description: Obtenga información sobre cómo acceder y explorar la zona protegida de Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Acceso y exploración de la zona protegida de AEP

Este artículo trata sobre lo siguiente:

* Las diferencias entre una organización de zona protegida de socios de Adobe Exchange existente y la zona protegida de AEP compartida.
* Solicitud de acceso a la zona protegida compartida de AEP.
* Recepción de una invitación por correo electrónico a la zona protegida compartida AEP.
* Invitar a nuevos usuarios a la [!DNL Admin Console].
* Navegación por la IU de AEP.

Para obtener una descripción general de la tecnología de espacio aislado en AEP, consulte esto [artículo](https://docs.adobe.com/content/help/es-ES/experience-platform/sandbox/home.html).

## La zona protegida de AEP compartida

Los socios de Exchange tienen acceso a varios Adobes [!DNL Experience Cloud] productos (productos que no son de AEP como [!DNL Analytics], [!DNL Target], etiquetas de Platform, etc.) mediante su propio Adobe [!DNL Experience Cloud] Organización (no compartida). A los socios se les otorgan derechos de acceso de administrador del sistema a su propia organización para administrar usuarios y otros permisos. Adobe [!DNL Experience Platform] (AEP) se trata de forma diferente que otras zonas protegidas de Adobe. Estas son las diferencias clave:

* El acceso a AEP NO se realiza a través del Adobe principal de los socios [!DNL Experience Cloud] organización de zona protegida.
* El acceso a AEP se realiza a través de una organización de intercambio de Adobe compartido.
* Muchas otras empresas asociadas de Adobe Exchange acceden a AEP con la misma organización
   * A través de la función de zona protegida de AEP, los datos y las actividades dentro de esta organización compartida no pueden ser vistos ni modificados por los otros socios; cada socio tendrá acceso a una zona protegida diferente dentro de la organización compartida.
* Los derechos de administración dentro de esta organización compartida son muy limitados.
* Después de obtener acceso a una zona protegida en AEP, los socios verán dos organizaciones en el conmutador de organizaciones en la parte superior derecha de la interfaz de usuario, mientras se encuentran en la página de inicio del Admin Console o del Experience Cloud principal. Sin embargo, cuando se inicia sesión en AEP, solo debe ser visible la organización compartida.

## Solicitar acceso a la zona protegida compartida de AEP

Enviar una [solicitud de asistencia](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new) con la siguiente información:

* Dirección de correo electrónico
* Asunto: Solicitud de zona protegida de AEP
* Producto: Aprovisionamiento general / Sandbox
* Tipo de vale: Soporte del programa - Programa de Exchange / Preguntas de solicitud de aprovisionamiento
* Descripción: Proporcione una breve descripción de los casos de uso de integración que requieren el uso de una zona protegida de AEP
* Asegúrese de proporcionar también todos los nombres de usuario y correos electrónicos que deben añadirse a la zona protegida de AEP. Es posible que se agreguen usuarios adicionales después de realizar la solicitud, pero los usuarios deberán agregarse por Adobe a través de un ticket adicional (ver a continuación).

## Recibir la invitación por correo electrónico

El contacto principal que solicitó la zona protegida de AEP recibirá un correo electrónico automatizado invitándolos a &quot;comenzar&quot; con el Adobe [!DNL Experience Platform]. El contacto principal también tendrá algunos privilegios de administración que se tratan en la siguiente sección.

En lugar de seleccionar el botón &quot;empezar&quot; en el correo electrónico, vaya directamente a `https://platform.adobe.com.` Inicie sesión con el Adobe ID asociado a la dirección de correo electrónico de la invitación o cree una si no está asociada a un Adobe ID.

## Invitar a usuarios adicionales

Enviar una [solicitud de asistencia](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new) con la siguiente información:

* Dirección de correo electrónico del solicitante
* Asunto: Zona protegida de AEP: Añadir administrador/usuario
* Producto: Aprovisionamiento general / Sandbox
* Tipo de vale: Soporte del programa - Programa de Exchange / Preguntas de solicitud de aprovisionamiento
* Descripción: Lista de usuarios que se van a añadir (nombres y correos electrónicos)

## Navegación por la IU de AEP

Vea la IU de AEP [vídeo de introducción](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Hay 12 áreas principales dentro de la interfaz de usuario de AEP que se pueden navegar mediante el panel izquierdo. Sin embargo, las secciones más importantes para este tipo de integración son Esquemas, Conjuntos de datos y Perfiles.

* Inicio: la pantalla de aterrizaje

   * Sugiere algunas actividades de introducción
   * Proporciona algunos vínculos al contenido de aprendizaje
   * Proporciona una vista de panel para algunos de los objetos de AEP principales, como Esquemas, Conjuntos de datos y Perfiles

* Flujos de trabajo: Inicie flujos de trabajo comunes para introducir datos en AEP
* Conexiones/fuentes: administrar fuentes de datos que llegan a AEP
* Conexiones / Destinos: administre las conexiones para enviar datos a sistemas externos
* Perfiles: vea y administre perfiles de cliente individuales
* Segmentos: examine, cree y modifique segmentos de clientes
* Identidades: examine, cree y modifique áreas de nombres de identidad; estos son los tipos de ID principales que se utilizan para identificar a un cliente de forma exclusiva
* Modelos (ciencia de datos): Participe en actividades de ciencia de datos, incluido el uso de un entorno Jupyter Notebooks integrado
* Servicios (ciencia de datos): publicar fórmulas de ciencia de datos como servicios
* Esquemas: examinar, crear y modificar esquemas; estas son las definiciones de datos detalladas utilizadas para mantener organizados los datos
* DataSets: examine, cree y administre DataSets; un DataSet se define mediante un esquema y es donde residen los datos dentro de AEP
* Consultas: examine, cree, modifique y utilice un repositorio de consultas para obtener información de los datos de DataSets
* Monitorización: vea el estado de todos los datos que entran y salen de AEP tanto para lote como para flujo
