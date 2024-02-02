---
title: Acceso al perfil unificado
description: Utilice las API para acceder al perfil unificado.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Acceso al perfil unificado mediante la API de perfil

El Adobe [!DNL Experience Platform] puede acceder al perfil del cliente en tiempo real; la variable [[!DNL Experience Platform] API de perfil del cliente en tiempo real](https://adobe.ly/2TtDHWr) se ha diseñado para interactuar con eso. Ver esto [tutorial](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html) para obtener información sobre cómo acceder a los datos de perfil del cliente en tiempo real mediante la API de perfil.

Este artículo hará referencia sustancial al tutorial vinculado anteriormente.

El [Colección Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) se hace referencia a en todo el artículo mediante las llamadas asociadas por número. Encontrará más información sobre la instalación y el uso de la colección Postman en Github [LÉAME](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. También hay conjuntos de datos de ejemplo de [fidelidad](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) y [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) datos.

Para esta sección, utilice la carpeta Postman 5: Búsqueda de perfiles, 5a: Búsqueda en tiempo real de datos de PERFIL O 5b: Búsqueda en tiempo real de datos de EVENTO.

## Uso de la API

Las siguientes secciones le ayudan a autenticarse en Experience Platform. Obtenga información sobre la ruta de la API, la información del encabezado y mucho más.

### Autenticar en [!DNL Platform]

Consulte [esta](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html) tutorial de autenticación antes de realizar cualquiera de las llamadas siguientes.

### Ruta de API

La URL de puerta de enlace de plataforma necesaria para la API del perfil del cliente en tiempo real es: `https://platform.adobe.io/`

La ruta base para la API es: `/data/core/ups/access/entities`

Un ejemplo de ruta completa es: `https://platform.adobe.io/data/core/ups/access/entities`

### Información de encabezado

El encabezado debe incluir:

* Autorización
* x-gw-ims-org-id: obtener a través de console.adobe.io
* x-api-key: obtener a través de console.adobe.io
* x-sandbox-name: obtenido de Adobe Integration Manager
* Content-Type: application/json

Encontrará más información acerca del encabezado en la [tutorial](https://adobe.ly/2PTHuKv).

## Acceso a perfiles de clientes en tiempo real mediante identidades

La API de perfil permite acceder a perfiles mediante una solicitud de GET. Las secciones a continuación seguirán esto [guía](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html).

### Acceso a datos de perfil mediante identidad

La API de proporciona acceso a la información de perfil mediante el uso de identidad. Para ello, realice una solicitud de GET a /access/entities con el ID de entidad como uno de los parámetros y el área de nombres del ID de entidad. NOTA: Tenga en cuenta que cualquier solicitud que devuelva 50 registros solo enviará un estado HTTP 422 y un mensaje que indique &quot;demasiadas identidades relacionadas&quot;, y la búsqueda deberá restringirse con más parámetros.

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

La API proporciona acceso a perfiles mediante una lista de identidades mediante una solicitud de POST al extremo /access/entities y proporciona las identidades en la carga útil. Estas identidades consisten en un valor de ID (entityId) y un área de nombres de identidad (entityIdNS).

Solicitud: la siguiente solicitud recupera los nombres y direcciones de correo electrónico de varios clientes mediante una lista de identidades:

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

Respuesta: Una respuesta correcta devuelve los campos solicitados de las entidades especificadas en el cuerpo de la solicitud.

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

Los socios pueden acceder a los eventos de series temporales según la identidad de la entidad de perfil asociada realizando una solicitud de GET al extremo /access/entities.

### Acceso a eventos de series temporales para un perfil por identidad

La identidad de su entidad de perfil asociada accede a los eventos de serie temporal realizando una solicitud de GET al extremo /access/entities. Esta identidad consta de un valor de ID (entityId) y un área de nombres de identidad (entityIdNS).

Solicitud: La siguiente solicitud encuentra una entidad de perfil por ID y recupera los valores de las propiedades endUserIDs, web y channel **para todos** eventos de series temporales asociados a la entidad.

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

Los resultados se paginan al recuperar eventos de series temporales. Si hay páginas de resultados subsiguientes, el parámetro _page.next de la respuesta contendrá un ID. Además, el parámetro _links.next.href de la respuesta proporciona un URI de solicitud para recuperar la página siguiente.

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

Una respuesta correcta devuelve la siguiente página de resultados. En este ejemplo se muestra una respuesta en la que no hay páginas de resultados subsiguientes, como indican los valores de cadena vacíos de _page.next y _links.next.href.

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

* [API de perfil del cliente en tiempo real](https://adobe.ly/2TtDHWr)
* [Acceso a los datos de perfil del cliente en tiempo real mediante el tutorial de API de perfil](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Guía de autenticación](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)
