---
title: Información general sobre la Guía de integración de acceso e ingesta de perfiles [!DNL Platform]
description: Obtenga información acerca de la integración de  [!DNL Experience Platform] ingesta de perfiles y acceso.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
TQID: https://experienceleague.adobe.com/whnqurJyM4QXl5ikRvez7hpKWRDuU4onzROsUk-WeSI
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 1%

---

# Guía de integración: ingesta de perfiles y acceso de [!DNL Experience Platform]

Los socios deben utilizar esta guía de integración para ayudarles a crear la funcionalidad de entrada y salida con Adobe [!DNL Experience Platform] (AEP). Existen API para la ingesta por lotes, la transmisión por secuencias y el acceso al perfil unificado (salida).

Para ayudar en el desarrollo, el equipo de Adobe Exchange ha creado una [colección de Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman). Se hace referencia a esta colección Postman en toda la guía de integración.

Encontrará más información sobre cómo instalar y usar la colección Postman en la página de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). También hay conjuntos de datos de ejemplo de [lealtad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y datos de [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Ejemplo de caso de uso de integración: sistema de respuesta de voz interactivo

Para los integradores, las API de [!DNL Experience Platform] proporcionan todas las capacidades de la plataforma que se ofrecen en toda la interfaz de usuario, pero ahora con la capacidad de crear flujos de trabajo de clientes y flujos de datos automatizados. Como integrador, comprueba periódicamente el estado de los conjuntos de datos, configura nuevos procedimientos de ingesta de datos e integra su propia solución de activación de audiencia con el perfil unificado.

Considere el mundo de los sistemas de respuesta de voz interactiva (IVR) y el software de administración de centros de llamadas. El proveedor puede usar las API [!DNL Experience Platform] para ingerir información histórica de la actividad del centro de llamadas del cliente en el lago de datos de experiencia. Si los datos se incorporan en el esquema XDM `ExperienceEvent` (un esquema que expresa las interacciones de los clientes), estas interacciones se pueden introducir sin fricción directamente en el servicio de perfil unificado. En este caso, `callerId` se usa como identificador del cliente. El servicio de identidad se encargará de la resolución de identidades y ayudará al servicio de perfil unificado a añadir cualquier punto de datos de interacciones recientes con el centro de llamadas al perfil del cliente.

La próxima vez que un cliente llame al centro de llamadas, primero recibirá una respuesta del IVR. Para personalizar el mensaje y ofrecer una oferta adaptada a la persona que llama, el sistema IVR necesita saber más sobre la persona que llama. Aquí es donde entra en juego la integración de la API con el perfil unificado. El servidor IVR puede ponerse en contacto con el servicio de perfil unificado para realizar una búsqueda de puntos. A continuación, consulte los atributos de perfil que se aplican solo a las interacciones del centro de llamadas o el perfil completo del cliente, que también tiene atributos para interacciones en otros puntos de contacto. Al combinar datos de varias fuentes de datos, mediante la resolución de identidades y el perfil unificado, el centro de llamadas y el proveedor de IVR pueden ofrecer una experiencia de cliente adaptada, compatible con Adobe [!DNL Experience Platform]&quot;.

## Recursos generales

* [Documentación del producto](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html) de AEP.
* AEP [Extensibilidad](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## ¿Preguntas o comentarios?

Envíe todas sus preguntas y comentarios a través del [canal de asistencia](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new)
