---
title: Acceso al perfil unificado
description: Utilice las API para acceder al perfil unificado.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: 0690a52c3be0981a626e49729e51cb1729816c87
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Acceso al perfil unificado mediante la API de perfil

Adobe [!DNL Experience Platform] puede acceder al perfil del cliente en tiempo real; la [[!DNL Experience Platform] API del perfil del cliente en tiempo real](https://adobe.ly/2TtDHWr) se ha diseñado para interactuar con eso. Consulte este [tutorial](https://docs.adobe.com/content/help/es-ES/experience-platform/profile/api/getting-started.html) para obtener acceso a los datos de perfil del cliente en tiempo real mediante la API de perfil.

Este artículo hará referencia sustancial al tutorial vinculado anteriormente.

Se hace referencia a la [colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) en todo el artículo mediante las llamadas asociadas por número. Encontrará más información sobre cómo instalar y usar la colección Postman en la página de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). También hay conjuntos de datos de ejemplo de [lealtad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y datos de [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

Para esta sección, utilice la carpeta Postman 5: Búsqueda de perfiles, 5a: Búsqueda en tiempo real de datos de PERFIL O 5b: Búsqueda en tiempo real de datos de EVENTO.

## Uso de la API

Las siguientes secciones le ayudan a autenticarse en Experience Platform. Obtenga información sobre la ruta de la API, la información del encabezado y mucho más.

### Autenticar en [!DNL Platform]

Ver [este](https://docs.adobe.com/content/help/es-ES/experience-platform/tutorials/authentication.html) tutorial de autenticación antes de realizar cualquiera de las llamadas siguientes.

### Ruta de API

La URL de puerta de enlace de plataforma necesaria para la API del perfil del cliente en tiempo real es: `https://platform.adobe.io/`

La ruta de acceso base para la API es: `/data/core/ups/access/entities`

Un ejemplo de ruta de acceso completa es: `https://platform.adobe.io/data/core/ups/access/entities`

### Información de encabezado

El encabezado debe incluir:

* Autorización
* x-gw-ims-org-id: obtener a través de console.adobe.io
* x-api-key: obtener a través de console.adobe.io
* x-sandbox-name: obtenido de Adobe Integration Manager
* Content-Type: application/json

Encontrará más información sobre el encabezado en el [tutorial](https://adobe.ly/2PTHuKv).

## Acceso a perfiles de clientes en tiempo real mediante identidades

La API de perfil permite acceder a perfiles mediante una solicitud de GET. Las secciones a continuación seguirán esta [guía](https://docs.adobe.com/content/help/es-ES/experience-platform/profile/api/entities.html).

### Acceso a datos de perfil mediante identidad

La API de proporciona acceso a la información de perfil mediante el uso de identidad. Para ello, realice una petición GET a /access/entities con el ID de entidad como uno de los parámetros y el área de nombres del ID de entidad. NOTA: Tenga en cuenta que cualquier solicitud que devuelva 50 registros solo enviará un estado HTTP 422 y un mensaje que indique &quot;demasiadas identidades relacionadas&quot;, y la búsqueda deberá restringirse con más parámetros.

Solicitud:

La siguiente solicitud recupera el correo electrónico y el nombre de un cliente mediante una identidad:

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Respuesta:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Acceso a perfiles por lista de identidades

La API proporciona acceso a perfiles mediante una lista de identidades mediante una petición POST al extremo /access/entities y proporciona las identidades en la carga útil. Estas identidades consisten en un valor de ID (entityId) y un área de nombres de identidad (entityIdNS).

Solicitud:
La siguiente solicitud recupera los nombres y direcciones de correo electrónico de varios clientes mediante una lista de identidades:

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Respuesta:
Una respuesta correcta devuelve los campos solicitados de las entidades especificadas en el cuerpo de la solicitud.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Eventos de series temporales

Los socios pueden acceder a los eventos de series temporales según la identidad de la entidad de perfil asociada realizando una petición GET al extremo /access/entities.

### Acceso a eventos de series temporales para un perfil por identidad

La identidad de su entidad de perfil asociada accede a los eventos de serie temporal realizando una petición GET al extremo /access/entities. Esta identidad consta de un valor de ID (entityId) y un área de nombres de identidad (entityIdNS).

Solicitud:
La siguiente solicitud encuentra una entidad de perfil por ID y recupera los valores de las propiedades endUserIDs, web y channel **para todos los** eventos de series temporales asociados a la entidad.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Respuesta:

Una respuesta correcta devuelve una lista paginada de eventos de series temporales y campos asociados especificados en los parámetros de solicitud.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Paginación de eventos de series temporales para un perfil

Los resultados se paginan al recuperar eventos de series temporales. Si hay páginas de resultados subsiguientes, el parámetro &lowbar;page.next de la respuesta contendrá un ID. Además, el parámetro &lowbar;links.next.href de la respuesta proporciona un URI de solicitud para recuperar la página siguiente.

Solicitud:

La siguiente solicitud recupera la siguiente página de resultados utilizando el URI _links.next.href como ruta de solicitud.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Respuesta:

Una respuesta correcta devuelve la siguiente página de resultados. En este ejemplo se muestra una respuesta en la que no hay páginas de resultados subsiguientes, como indican los valores de cadena vacíos de &lowbar;page.next y &lowbar;links.next.href.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Artículos de referencia

* [API de perfil de cliente en tiempo real](https://adobe.ly/2TtDHWr)
* [Acceder a los datos de perfil del cliente en tiempo real mediante el tutorial de la API del perfil](https://docs.adobe.com/content/help/es-ES/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Guía de autenticación](https://docs.adobe.com/content/help/es-ES/experience-platform/tutorials/authentication.html)
