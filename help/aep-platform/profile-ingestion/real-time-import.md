---
title: Importación en tiempo real
description: Obtenga información sobre cómo importar datos en AEP en tiempo real.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Transmitir datos a AEP

Adobe [!DNL Experience Platform] permite que los eventos de perfil y experiencia se transmitan y estén disponibles en tiempo casi real. Todos los datos enviados a AEP mediante streaming se conservan en el lago de datos. Los datos se pueden transmitir a conjuntos de datos existentes o a conjuntos de datos completamente nuevos mediante API o mediante Adobe Launch.

Este artículo trata sobre lo siguiente:

* Flujo hacia el perfil individual de XDM
* Transmisión a ExperienceEvent de XDM
* Uso de AEP con la extensión Launch para el flujo

El [Colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) se hace referencia a en todo el artículo mediante las llamadas asociadas por número. Encontrará más información sobre la instalación y el uso de la colección Postman en Github [LÉAME](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. También hay conjuntos de datos de ejemplo de [fidelidad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) datos.

## Requisitos previos

* [Autenticar en la plataforma](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html).
* Recopile los valores de los encabezados necesarios del tutorial de autenticación vinculado anteriormente.

## Creación de una conexión de flujo continuo

Para transmitir a AEP, primero debe crear una conexión de flujo continuo. Las conexiones de flujo continuo contienen atributos como el origen de los datos de flujo continuo y si está enviando o no registros que pertenecen a la variable [!DNL Experience Data Model] Esquemas de (XDM). Después de crear una conexión de flujo continuo, se le proporcionará una dirección URL única que utilizará para transmitir datos a AEP.

Ir [aquí](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) para obtener instrucciones sobre cómo crear una conexión de flujo continuo a través de API o [aquí](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) para obtener instrucciones sobre cómo crear una conexión de flujo continuo a través de la interfaz de usuario.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Respuesta:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Asegúrese de guardar el ID proporcionado en la respuesta anterior para futuras llamadas de ingesta de transmisión (la colección Postman lo guardará en la variable de entorno CONNECTION_ID).

## Transmitir datos de perfil a AEP

Para esta sección, utilice las carpetas de llamadas de Postman: 3: Importación en tiempo real, 3a: Importación en tiempo real para datos de PERFIL.

Se documentan solicitudes JSON detalladas con respuestas para datos de perfil de streaming [aquí](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Pasos:

1. Creación de un esquema de perfil individual de XDM
1. Definición del descriptor de identidad principal para el perfil individual XDM (clave principal)
1. Crear un conjunto de datos para registros de perfil individuales de XDM
1. Llame a las API de ingesta de transmisión para crear un registro de perfil individual de XDM
1. Recupere el perfil recién creado

## Transmitir eventos de experiencia a AEP

Para esta sección, utilice las carpetas de llamadas de Postman: 3: Importación en tiempo real, 3b: Importación en tiempo real para datos de PERFIL.

Se documentan solicitudes JSON detalladas con respuestas para datos de experiencia de streaming [aquí](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Pasos:

1. Creación de un esquema XDM ExperienceEvent
1. Establezca el descriptor de identidad principal para el ExperienceEvent de XDM (clave principal)
1. Crear un conjunto de datos para ExperienceEvents de XDM
1. Llame a las API de ingesta de transmisión para crear un ExperienceEvent de XDM
1. Recupere el evento recién creado

## Usar etiquetas de Experience Platform para transmitir a AEP

El Adobe [!DNL Experience Platform] La extensión de Launch proporciona una forma de transmitir a AEP a través de Launch. Para obtener más información, consulte [esta guía](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Artículos de referencia

* [API de ingesta de datos](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Resumen de ingesta de streaming](https://docs.adobe.com/content/help/es-ES/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Guía para desarrolladores de ingesta de streaming](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Uso de la extensión Launch de AEP](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
