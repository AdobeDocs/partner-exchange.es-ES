---
title: Importar datos por lotes a AEP
description: Obtenga información sobre cómo importar archivos por lotes en Experience Platform
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Importar datos por lotes a AEP

AEP puede introducir archivos por lotes que contengan datos de perfil de un archivo plano (como parquet) o datos que se ajusten a un esquema conocido en [!UICONTROL Modelo de datos de experiencia] (XDM).

AEP puede introducir datos mediante archivos por lotes. Se aceptan los siguientes formatos: JSON, Parquet y CSV.

Este artículo trata sobre lo siguiente:

* Requisitos previos de ingesta por lotes
* Prácticas recomendadas y límites de ingesta por lotes
* Cómo crear un lote
* Cómo completar un lote
* Comprobación del estado de un lote

El [Colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) se hace referencia a en todo el artículo mediante las llamadas asociadas por número. Encontrará más información sobre la instalación y el uso de la colección Postman en Github [LÉAME](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. También hay conjuntos de datos de ejemplo de [fidelidad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) datos.

Para todas las llamadas de este tutorial, utilice las carpetas de llamadas de Postman: 4: Importación por lotes, 4a: Importación por lotes para datos de PERFIL O 4b: Importación por lotes para datos de EVENTO.

## Requisitos previos de ingesta por lotes

* Defina un esquema y cree un conjunto de datos.
* Los datos deben tener el formato JSON, Parquet o CSV.
* [Autenticar en la plataforma](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Recopile los valores de los encabezados necesarios del tutorial de autenticación vinculado anteriormente.

## Prácticas recomendadas y límites de ingesta por lotes

* Tamaño máximo del lote: 100 GB
* Número máximo de archivos por lote: 1500
* Si un archivo tiene más de 512 MB, deberá dividirse en fragmentos más pequeños. Puede encontrar más información en la [guía para desarrolladores](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Número máximo de propiedades o campos por fila: 10 000
* Número máximo de lotes por minuto, por usuario: 138

## Crear un lote

En este tutorial utilizaremos JSON como formato. Encontrará más ejemplos de formato en la [guía para desarrolladores](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Cree un lote utilizando JSON como formato de entrada (asegúrese de incluir un ID de conjunto de datos y de que los datos se ajusten al esquema XDM vinculado al conjunto de datos):

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Respuesta:

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Cargar archivos

Ahora se pueden cargar archivos en el lote recién creado (utilizando batch_id de la respuesta anterior).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>La API solo admite la carga de una sola parte, lo que significa que cada archivo/microlote deberá cargarse con llamadas individuales. Asegúrese de que content-type es application/octet-stream.

Respuesta:

```
200 OK
```

## Completar un lote

Una vez cargados todos los archivos, esta llamada indicará que el lote está listo para la promoción:

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Respuesta:

```
200 OK
```

## Comprobar el estado de un lote

El estado del lote puede comprobarse en la interfaz de usuario o a través de la API (consulte la llamada a continuación). Para proteger la interfaz de usuario, vaya al DataSet para ver el estado.

Se pueden encontrar los distintos estados de ingesta por lotes [aquí](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Respuesta:

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Artículos de referencia

* [API de ingesta de datos](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Resumen de ingesta por lotes](https://docs.adobe.com/content/help/es-ES/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Guía para desarrolladores de ingesta por lotes](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Guía de resolución de problemas de ingesta por lotes](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Ingesta de datos Postman Collection](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Tutorial de autenticación](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
