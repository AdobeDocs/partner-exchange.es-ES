---
title: "[!DNL Platform] Información general sobre la Guía de integración de acceso e ingesta de perfiles"
description: Obtenga información acerca de la integración de para [!DNL Experience Platform] ingesta de perfiles y acceso.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Guía de integración: [!DNL Experience Platform] ingesta de perfiles y acceso

Los socios deben utilizar esta guía de integración para ayudarles a crear la funcionalidad de entrada y salida con el Adobe [!DNL Experience Platform] (AEP). Existen API para la ingesta por lotes, la transmisión por secuencias y el acceso al perfil unificado (salida).

Para ayudar en el desarrollo, una [Colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) ha sido creado por el equipo de intercambio de Adobe. Se hace referencia a esta colección Postman en toda la guía de integración.

Encontrará más información sobre la instalación y el uso de la colección Postman en Github [LÉAME](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. También hay conjuntos de datos de ejemplo de [fidelidad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) datos.

## Ejemplo de caso de uso de integración: sistema de respuesta de voz interactivo

Para los integradores, la variable [!DNL Experience Platform] Las API proporcionan todas las funcionalidades de la plataforma que se ofrecen en toda la interfaz de usuario, pero ahora con la capacidad de crear flujos de trabajo de clientes y flujos de datos automatizados. Como integrador, comprueba periódicamente el estado de los conjuntos de datos, configura nuevos procedimientos de ingesta de datos e integra su propia solución de activación de audiencia con el perfil unificado.

Considere el mundo de los sistemas de respuesta de voz interactiva (IVR) y el software de administración de centros de llamadas. El proveedor puede utilizar el [!DNL Experience Platform] API para introducir información histórica de la actividad del centro de llamadas del cliente en el lago de datos de experiencia. Si los datos se incorporan en el XDM `ExperienceEvent` Esquema (un esquema que expresa las interacciones de los clientes), estas interacciones se pueden ingerir sin fricción directamente en el servicio de perfil unificado. En este caso, la variable `callerId` se utiliza como identificador del cliente. El servicio de identidad se encargará de la resolución de identidades y ayudará al servicio de perfil unificado a añadir cualquier punto de datos de interacciones recientes con el centro de llamadas al perfil del cliente.

La próxima vez que un cliente llame al centro de llamadas, primero recibirá una respuesta del IVR. Para personalizar el mensaje y ofrecer una oferta adaptada a la persona que llama, el sistema IVR necesita saber más sobre la persona que llama. Aquí es donde entra en juego la integración de la API con el perfil unificado. El servidor IVR puede ponerse en contacto con el servicio de perfil unificado para realizar una búsqueda de puntos. A continuación, consulte los atributos de perfil que se aplican solo a las interacciones del centro de llamadas o el perfil completo del cliente, que también tiene atributos para interacciones en otros puntos de contacto. Al combinar datos de múltiples fuentes de datos, mediante la resolución de identidades y el perfil unificado, el centro de llamadas y el proveedor de IVR pueden ofrecer una experiencia de cliente adaptada, con el apoyo del Adobe [!DNL Experience Platform].&quot;

## Recursos generales

* AEP [Documentación del producto](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html).
* AEP [Extensibilidad](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## ¿Preguntas o comentarios?

Envíe todas sus preguntas y comentarios a través de la [canal de soporte](https://adobeexchangeec.zendesk.com/hc/es-es/requests/new)
