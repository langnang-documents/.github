---
created: 2022-11-29T13:37:46 (UTC +08:00)
tags: []
source: https://spec.openapis.org/oas/v3.1.0.html
author: Darrel Miller
---

# OpenAPI Specification v3.1.0 | Introduction, Definitions, & More

> ## Excerpt
> The OpenAPI Specification (OAS) defines a standard, programming language-agnostic interface description for HTTP APIs.

---
## Schema

In the following description, if a field is not explicitly **_REQUIRED_** or described with a _MUST_ or _SHALL_, it can be considered _OPTIONAL_.

### OpenAPI Object

This is the root object of the [OpenAPI document](https://spec.openapis.org/oas/v3.1.0.html#oasDocument).

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| openapi | `string` | **_REQUIRED_**. This string _MUST_ be the [version number](https://spec.openapis.org/oas/v3.1.0.html#versions) of the OpenAPI Specification that the OpenAPI document uses. The `openapi` field _SHOULD_ be used by tooling to interpret the OpenAPI document. This is _not_ related to the API [`info.version`](https://spec.openapis.org/oas/v3.1.0.html#infoVersion) string. |
| info | [Info Object](https://spec.openapis.org/oas/v3.1.0.html#infoObject) | **_REQUIRED_**. Provides metadata about the API. The metadata _MAY_ be used by tooling as required. |
| jsonSchemaDialect | `string` | The default value for the `$schema` keyword within [Schema Objects](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) contained within this OAS document. This _MUST_ be in the form of a URI. |
| servers | \[[Server Object](https://spec.openapis.org/oas/v3.1.0.html#serverObject)\] | An array of Server Objects, which provide connectivity information to a target server. If the `servers` property is not provided, or is an empty array, the default value would be a [Server Object](https://spec.openapis.org/oas/v3.1.0.html#serverObject) with a [url](https://spec.openapis.org/oas/v3.1.0.html#serverUrl) value of `/`. |
| paths | [Paths Object](https://spec.openapis.org/oas/v3.1.0.html#pathsObject) | The available paths and operations for the API. |
| webhooks | Map\[`string`, [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] \] | The incoming webhooks that _MAY_ be received as part of this API and that the API consumer _MAY_ choose to implement. Closely related to the `callbacks` feature, this section describes requests initiated other than by an API call, for example by an out of band registration. The key name is a unique string to refer to each webhook, while the (optionally referenced) Path Item Object describes a request that may be initiated by the API provider and the expected responses. An [example](https://github.com/OAI/OpenAPI-Specification/tree/master/examples/v3.1/webhook-example.yaml) is available. |
| components | [Components Object](https://spec.openapis.org/oas/v3.1.0.html#componentsObject) | An element to hold various schemas for the document. |
| security | \[[Security Requirement Object](https://spec.openapis.org/oas/v3.1.0.html#securityRequirementObject)\] | A declaration of which security mechanisms can be used across the API. The list of values includes alternative security requirement objects that can be used. Only one of the security requirement objects need to be satisfied to authorize a request. Individual operations can override this definition. To make security optional, an empty security requirement (`{}`) can be included in the array. |
| tags | \[[Tag Object](https://spec.openapis.org/oas/v3.1.0.html#tagObject)\] | A list of tags used by the document with additional metadata. The order of the tags can be used to reflect on their order by the parsing tools. Not all tags that are used by the [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) must be declared. The tags that are not declared _MAY_ be organized randomly or based on the tools’ logic. Each tag name in the list _MUST_ be unique. |
| externalDocs | [External Documentation Object](https://spec.openapis.org/oas/v3.1.0.html#externalDocumentationObject) | Additional external documentation. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

### Info Object

The object provides metadata about the API. The metadata _MAY_ be used by the clients if needed, and _MAY_ be presented in editing or documentation generation tools for convenience.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| title | `string` | **_REQUIRED_**. The title of the API. |
| summary | `string` | A short summary of the API. |
| description | `string` | A description of the API. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| termsOfService | `string` | A URL to the Terms of Service for the API. This _MUST_ be in the form of a URL. |
| contact | [Contact Object](https://spec.openapis.org/oas/v3.1.0.html#contactObject) | The contact information for the exposed API. |
| license | [License Object](https://spec.openapis.org/oas/v3.1.0.html#licenseObject) | The license information for the exposed API. |
| version | `string` | **_REQUIRED_**. The version of the OpenAPI document (which is distinct from the [OpenAPI Specification version](https://spec.openapis.org/oas/v3.1.0.html#oasVersion) or the API implementation version). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Info Object Example

```

{
  "title": "Sample Pet Store App",
  "summary": "A pet store manager.",
  "description": "This is a sample server for a pet store.",
  "termsOfService": "https://example.com/terms/",
  "contact": {
    "name": "API Support",
    "url": "https://www.example.com/support",
    "email": "support@example.com"
  },
  "license": {
    "name": "Apache 2.0",
    "url": "https://www.apache.org/licenses/LICENSE-2.0.html"
  },
  "version": "1.0.1"
}
```

```

title: Sample Pet Store App
summary: A pet store manager.
description: This is a sample server for a pet store.
termsOfService: https://example.com/terms/
contact:
  name: API Support
  url: https://www.example.com/support
  email: support@example.com
license:
  name: Apache 2.0
  url: https://www.apache.org/licenses/LICENSE-2.0.html
version: 1.0.1
```

### Contact Object

Contact information for the exposed API.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| name | `string` | The identifying name of the contact person/organization. |
| url | `string` | The URL pointing to the contact information. This _MUST_ be in the form of a URL. |
| email | `string` | The email address of the contact person/organization. This _MUST_ be in the form of an email address. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Contact Object Example

```

{
  "name": "API Support",
  "url": "https://www.example.com/support",
  "email": "support@example.com"
}
```

```

name: API Support
url: https://www.example.com/support
email: support@example.com
```

### License Object

License information for the exposed API.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| name | `string` | **_REQUIRED_**. The license name used for the API. |
| identifier | `string` | An [SPDX](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60) license expression for the API. The `identifier` field is mutually exclusive of the `url` field. |
| url | `string` | A URL to the license used for the API. This _MUST_ be in the form of a URL. The `url` field is mutually exclusive of the `identifier` field. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### License Object Example

```

{
  "name": "Apache 2.0",
  "identifier": "Apache-2.0"
}
```

```

name: Apache 2.0
identifier: Apache-2.0
```

### Server Object

An object representing a Server.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| url | `string` | **_REQUIRED_**. A URL to the target host. This URL supports Server Variables and _MAY_ be relative, to indicate that the host location is relative to the location where the OpenAPI document is being served. Variable substitutions will be made when a variable is named in `{`brackets`}`. |
| description | `string` | An optional string describing the host designated by the URL. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| variables | Map\[`string`, [Server Variable Object](https://spec.openapis.org/oas/v3.1.0.html#serverVariableObject)\] | A map between a variable name and its value. The value is used for substitution in the server’s URL template. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Server Object Example

A single server would be described as:

```

{
  "url": "https://development.gigantic-server.com/v1",
  "description": "Development server"
}
```

```

url: https://development.gigantic-server.com/v1
description: Development server
```

The following shows how multiple servers can be described, for example, at the OpenAPI Object’s [`servers`](https://spec.openapis.org/oas/v3.1.0.html#oasServers):

```

{
  "servers": [
    {
      "url": "https://development.gigantic-server.com/v1",
      "description": "Development server"
    },
    {
      "url": "https://staging.gigantic-server.com/v1",
      "description": "Staging server"
    },
    {
      "url": "https://api.gigantic-server.com/v1",
      "description": "Production server"
    }
  ]
}
```

```

servers:
- url: https://development.gigantic-server.com/v1
  description: Development server
- url: https://staging.gigantic-server.com/v1
  description: Staging server
- url: https://api.gigantic-server.com/v1
  description: Production server
```

The following shows how variables can be used for a server configuration:

```

{
  "servers": [
    {
      "url": "https://{username}.gigantic-server.com:{port}/{basePath}",
      "description": "The production API server",
      "variables": {
        "username": {
          "default": "demo",
          "description": "this value is assigned by the service provider, in this example `gigantic-server.com`"
        },
        "port": {
          "enum": [
            "8443",
            "443"
          ],
          "default": "8443"
        },
        "basePath": {
          "default": "v2"
        }
      }
    }
  ]
}
```

```

servers:
- url: https://{username}.gigantic-server.com:{port}/{basePath}
  description: The production API server
  variables:
    username:
      # note! no enum here means it is an open value
      default: demo
      description: this value is assigned by the service provider, in this example `gigantic-server.com`
    port:
      enum:
        - '8443'
        - '443'
      default: '8443'
    basePath:
      # open meaning there is the opportunity to use special base paths as assigned by the provider, default is `v2`
      default: v2
```

### Server Variable Object

An object representing a Server Variable for server URL template substitution.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| enum | \[`string`\] | An enumeration of string values to be used if the substitution options are from a limited set. The array _MUST NOT_ be empty. |
| default | `string` | **_REQUIRED_**. The default value to use for substitution, which _SHALL_ be sent if an alternate value is _not_ supplied. Note this behavior is different than the [Schema Object’s](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) treatment of default values, because in those cases parameter values are optional. If the [`enum`](https://spec.openapis.org/oas/v3.1.0.html#serverVariableEnum) is defined, the value _MUST_ exist in the enum’s values. |
| description | `string` | An optional description for the server variable. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

### Components Object

Holds a set of reusable objects for different aspects of the OAS. All objects defined within the components object will have no effect on the API unless they are explicitly referenced from properties outside the components object.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| schemas | Map\[`string`, [Schema Object](https://spec.openapis.org/oas/v3.1.0.html#schemaObject)\] | An object to hold reusable [Schema Objects](https://spec.openapis.org/oas/v3.1.0.html#schemaObject). |
| responses | Map\[`string`, [Response Object](https://spec.openapis.org/oas/v3.1.0.html#responseObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Response Objects](https://spec.openapis.org/oas/v3.1.0.html#responseObject). |
| parameters | Map\[`string`, [Parameter Object](https://spec.openapis.org/oas/v3.1.0.html#parameterObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Parameter Objects](https://spec.openapis.org/oas/v3.1.0.html#parameterObject). |
| examples | Map\[`string`, [Example Object](https://spec.openapis.org/oas/v3.1.0.html#exampleObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Example Objects](https://spec.openapis.org/oas/v3.1.0.html#exampleObject). |
| requestBodies | Map\[`string`, [Request Body Object](https://spec.openapis.org/oas/v3.1.0.html#requestBodyObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Request Body Objects](https://spec.openapis.org/oas/v3.1.0.html#requestBodyObject). |
| headers | Map\[`string`, [Header Object](https://spec.openapis.org/oas/v3.1.0.html#headerObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Header Objects](https://spec.openapis.org/oas/v3.1.0.html#headerObject). |
| securitySchemes | Map\[`string`, [Security Scheme Object](https://spec.openapis.org/oas/v3.1.0.html#securitySchemeObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Security Scheme Objects](https://spec.openapis.org/oas/v3.1.0.html#securitySchemeObject). |
| links | Map\[`string`, [Link Object](https://spec.openapis.org/oas/v3.1.0.html#linkObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Link Objects](https://spec.openapis.org/oas/v3.1.0.html#linkObject). |
| callbacks | Map\[`string`, [Callback Object](https://spec.openapis.org/oas/v3.1.0.html#callbackObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Callback Objects](https://spec.openapis.org/oas/v3.1.0.html#callbackObject). |
| pathItems | Map\[`string`, [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | An object to hold reusable [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

All the fixed fields declared above are objects that _MUST_ use keys that match the regular expression: `^[a-zA-Z0-9\.\-_]+$`.

Field Name Examples:

```

User
User_1
User_Name
user-name
my.org.User
```

#### Components Object Example

```

"components": {
  "schemas": {
    "GeneralError": {
      "type": "object",
      "properties": {
        "code": {
          "type": "integer",
          "format": "int32"
        },
        "message": {
          "type": "string"
        }
      }
    },
    "Category": {
      "type": "object",
      "properties": {
        "id": {
          "type": "integer",
          "format": "int64"
        },
        "name": {
          "type": "string"
        }
      }
    },
    "Tag": {
      "type": "object",
      "properties": {
        "id": {
          "type": "integer",
          "format": "int64"
        },
        "name": {
          "type": "string"
        }
      }
    }
  },
  "parameters": {
    "skipParam": {
      "name": "skip",
      "in": "query",
      "description": "number of items to skip",
      "required": true,
      "schema": {
        "type": "integer",
        "format": "int32"
      }
    },
    "limitParam": {
      "name": "limit",
      "in": "query",
      "description": "max records to return",
      "required": true,
      "schema" : {
        "type": "integer",
        "format": "int32"
      }
    }
  },
  "responses": {
    "NotFound": {
      "description": "Entity not found."
    },
    "IllegalInput": {
      "description": "Illegal input for operation."
    },
    "GeneralError": {
      "description": "General Error",
      "content": {
        "application/json": {
          "schema": {
            "$ref": "#/components/schemas/GeneralError"
          }
        }
      }
    }
  },
  "securitySchemes": {
    "api_key": {
      "type": "apiKey",
      "name": "api_key",
      "in": "header"
    },
    "petstore_auth": {
      "type": "oauth2",
      "flows": {
        "implicit": {
          "authorizationUrl": "https://example.org/api/oauth/dialog",
          "scopes": {
            "write:pets": "modify pets in your account",
            "read:pets": "read your pets"
          }
        }
      }
    }
  }
}
```

```

components:
  schemas:
    GeneralError:
      type: object
      properties:
        code:
          type: integer
          format: int32
        message:
          type: string
    Category:
      type: object
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
    Tag:
      type: object
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
  parameters:
    skipParam:
      name: skip
      in: query
      description: number of items to skip
      required: true
      schema:
        type: integer
        format: int32
    limitParam:
      name: limit
      in: query
      description: max records to return
      required: true
      schema:
        type: integer
        format: int32
  responses:
    NotFound:
      description: Entity not found.
    IllegalInput:
      description: Illegal input for operation.
    GeneralError:
      description: General Error
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/GeneralError'
  securitySchemes:
    api_key:
      type: apiKey
      name: api_key
      in: header
    petstore_auth:
      type: oauth2
      flows: 
        implicit:
          authorizationUrl: https://example.org/api/oauth/dialog
          scopes:
            write:pets: modify pets in your account
            read:pets: read your pets
```

### Paths Object

Holds the relative paths to the individual endpoints and their operations. The path is appended to the URL from the [`Server Object`](https://spec.openapis.org/oas/v3.1.0.html#serverObject) in order to construct the full URL. The Paths _MAY_ be empty, due to [Access Control List (ACL) constraints](https://spec.openapis.org/oas/v3.1.0.html#securityFiltering).

#### Patterned Fields

| Field Pattern | Type | Description |
| --- | --- | --- |
| /{path} | [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) | A relative path to an individual endpoint. The field name _MUST_ begin with a forward slash (`/`). The path is **appended** (no relative URL resolution) to the expanded URL from the [`Server Object`](https://spec.openapis.org/oas/v3.1.0.html#serverObject)’s `url` field in order to construct the full URL. [Path templating](https://spec.openapis.org/oas/v3.1.0.html#pathTemplating) is allowed. When matching URLs, concrete (non-templated) paths would be matched before their templated counterparts. Templated paths with the same hierarchy but different templated names _MUST NOT_ exist as they are identical. In case of ambiguous matching, it’s up to the tooling to decide which one to use. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Path Templating Matching

Assuming the following paths, the concrete definition, `/pets/mine`, will be matched first if used:

```

  /pets/{petId}
  /pets/mine
```

The following paths are considered identical and invalid:

```

  /pets/{petId}
  /pets/{name}
```

The following may lead to ambiguous resolution:

```

  /{entity}/me
  /books/{id}
```

#### Paths Object Example

```

{
  "/pets": {
    "get": {
      "description": "Returns all pets from the system that the user has access to",
      "responses": {
        "200": {          
          "description": "A list of pets.",
          "content": {
            "application/json": {
              "schema": {
                "type": "array",
                "items": {
                  "$ref": "#/components/schemas/pet"
                }
              }
            }
          }
        }
      }
    }
  }
}
```

```

/pets:
  get:
    description: Returns all pets from the system that the user has access to
    responses:
      '200':
        description: A list of pets.
        content:
          application/json:
            schema:
              type: array
              items:
                $ref: '#/components/schemas/pet'
```

### Path Item Object

Describes the operations available on a single path. A Path Item _MAY_ be empty, due to [ACL constraints](https://spec.openapis.org/oas/v3.1.0.html#securityFiltering). The path itself is still exposed to the documentation viewer but they will not know which operations and parameters are available.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| $ref | `string` | Allows for a referenced definition of this path item. The referenced structure _MUST_ be in the form of a [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject). In case a Path Item Object field appears both in the defined object and the referenced object, the behavior is undefined. See the rules for resolving [Relative References](https://spec.openapis.org/oas/v3.1.0.html#relativeReferencesURI). |
| summary | `string` | An optional, string summary, intended to apply to all operations in this path. |
| description | `string` | An optional, string description, intended to apply to all operations in this path. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| get | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a GET operation on this path. |
| put | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a PUT operation on this path. |
| post | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a POST operation on this path. |
| delete | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a DELETE operation on this path. |
| options | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a OPTIONS operation on this path. |
| head | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a HEAD operation on this path. |
| patch | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a PATCH operation on this path. |
| trace | [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) | A definition of a TRACE operation on this path. |
| servers | \[[Server Object](https://spec.openapis.org/oas/v3.1.0.html#serverObject)\] | An alternative `server` array to service all operations in this path. |
| parameters | \[[Parameter Object](https://spec.openapis.org/oas/v3.1.0.html#parameterObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | A list of parameters that are applicable for all the operations described under this path. These parameters can be overridden at the operation level, but cannot be removed there. The list _MUST NOT_ include duplicated parameters. A unique parameter is defined by a combination of a [name](https://spec.openapis.org/oas/v3.1.0.html#parameterName) and [location](https://spec.openapis.org/oas/v3.1.0.html#parameterIn). The list can use the [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) to link to parameters that are defined at the [OpenAPI Object’s components/parameters](https://spec.openapis.org/oas/v3.1.0.html#componentsParameters). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Path Item Object Example

```

{
  "get": {
    "description": "Returns pets based on ID",
    "summary": "Find pets by ID",
    "operationId": "getPetsById",
    "responses": {
      "200": {
        "description": "pet response",
        "content": {
          "*/*": {
            "schema": {
              "type": "array",
              "items": {
                "$ref": "#/components/schemas/Pet"
              }
            }
          }
        }
      },
      "default": {
        "description": "error payload",
        "content": {
          "text/html": {
            "schema": {
              "$ref": "#/components/schemas/ErrorModel"
            }
          }
        }
      }
    }
  },
  "parameters": [
    {
      "name": "id",
      "in": "path",
      "description": "ID of pet to use",
      "required": true,
      "schema": {
        "type": "array",
        "items": {
          "type": "string"
        }
      },
      "style": "simple"
    }
  ]
}
```

```

get:
  description: Returns pets based on ID
  summary: Find pets by ID
  operationId: getPetsById
  responses:
    '200':
      description: pet response
      content:
        '*/*' :
          schema:
            type: array
            items:
              $ref: '#/components/schemas/Pet'
    default:
      description: error payload
      content:
        'text/html':
          schema:
            $ref: '#/components/schemas/ErrorModel'
parameters:
- name: id
  in: path
  description: ID of pet to use
  required: true
  schema:
    type: array
    items:
      type: string  
  style: simple
```

### Operation Object

Describes a single API operation on a path.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| tags | \[`string`\] | A list of tags for API documentation control. Tags can be used for logical grouping of operations by resources or any other qualifier. |
| summary | `string` | A short summary of what the operation does. |
| description | `string` | A verbose explanation of the operation behavior. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| externalDocs | [External Documentation Object](https://spec.openapis.org/oas/v3.1.0.html#externalDocumentationObject) | Additional external documentation for this operation. |
| operationId | `string` | Unique string used to identify the operation. The id _MUST_ be unique among all operations described in the API. The operationId value is **case-sensitive**. Tools and libraries _MAY_ use the operationId to uniquely identify an operation, therefore, it is _RECOMMENDED_ to follow common programming naming conventions. |
| parameters | \[[Parameter Object](https://spec.openapis.org/oas/v3.1.0.html#parameterObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | A list of parameters that are applicable for this operation. If a parameter is already defined at the [Path Item](https://spec.openapis.org/oas/v3.1.0.html#pathItemParameters), the new definition will override it but can never remove it. The list _MUST NOT_ include duplicated parameters. A unique parameter is defined by a combination of a [name](https://spec.openapis.org/oas/v3.1.0.html#parameterName) and [location](https://spec.openapis.org/oas/v3.1.0.html#parameterIn). The list can use the [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) to link to parameters that are defined at the [OpenAPI Object’s components/parameters](https://spec.openapis.org/oas/v3.1.0.html#componentsParameters). |
| requestBody | [Request Body Object](https://spec.openapis.org/oas/v3.1.0.html#requestBodyObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) | The request body applicable for this operation. The `requestBody` is fully supported in HTTP methods where the HTTP 1.1 specification \[[RFC7231](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7231)\] has explicitly defined semantics for request bodies. In other cases where the HTTP spec is vague (such as [GET](https://tools.ietf.org/html/rfc7231#section-4.3.1), [HEAD](https://tools.ietf.org/html/rfc7231#section-4.3.2) and [DELETE](https://tools.ietf.org/html/rfc7231#section-4.3.5)), `requestBody` is permitted but does not have well-defined semantics and _SHOULD_ be avoided if possible. |
| responses | [Responses Object](https://spec.openapis.org/oas/v3.1.0.html#responsesObject) | The list of possible responses as they are returned from executing this operation. |
| callbacks | Map\[`string`, [Callback Object](https://spec.openapis.org/oas/v3.1.0.html#callbackObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | A map of possible out-of band callbacks related to the parent operation. The key is a unique identifier for the Callback Object. Each value in the map is a [Callback Object](https://spec.openapis.org/oas/v3.1.0.html#callbackObject) that describes a request that may be initiated by the API provider and the expected responses. |
| deprecated | `boolean` | Declares this operation to be deprecated. Consumers _SHOULD_ refrain from usage of the declared operation. Default value is `false`. |
| security | \[[Security Requirement Object](https://spec.openapis.org/oas/v3.1.0.html#securityRequirementObject)\] | A declaration of which security mechanisms can be used for this operation. The list of values includes alternative security requirement objects that can be used. Only one of the security requirement objects need to be satisfied to authorize a request. To make security optional, an empty security requirement (`{}`) can be included in the array. This definition overrides any declared top-level [`security`](https://spec.openapis.org/oas/v3.1.0.html#oasSecurity). To remove a top-level security declaration, an empty array can be used. |
| servers | \[[Server Object](https://spec.openapis.org/oas/v3.1.0.html#serverObject)\] | An alternative `server` array to service this operation. If an alternative `server` object is specified at the Path Item Object or Root level, it will be overridden by this value. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Operation Object Example

```

{
  "tags": [
    "pet"
  ],
  "summary": "Updates a pet in the store with form data",
  "operationId": "updatePetWithForm",
  "parameters": [
    {
      "name": "petId",
      "in": "path",
      "description": "ID of pet that needs to be updated",
      "required": true,
      "schema": {
        "type": "string"
      }
    }
  ],
  "requestBody": {
    "content": {
      "application/x-www-form-urlencoded": {
        "schema": {
          "type": "object",
          "properties": {
            "name": { 
              "description": "Updated name of the pet",
              "type": "string"
            },
            "status": {
              "description": "Updated status of the pet",
              "type": "string"
            }
          },
          "required": ["status"] 
        }
      }
    }
  },
  "responses": {
    "200": {
      "description": "Pet updated.",
      "content": {
        "application/json": {},
        "application/xml": {}
      }
    },
    "405": {
      "description": "Method Not Allowed",
      "content": {
        "application/json": {},
        "application/xml": {}
      }
    }
  },
  "security": [
    {
      "petstore_auth": [
        "write:pets",
        "read:pets"
      ]
    }
  ]
}
```

```

tags:
- pet
summary: Updates a pet in the store with form data
operationId: updatePetWithForm
parameters:
- name: petId
  in: path
  description: ID of pet that needs to be updated
  required: true
  schema:
    type: string
requestBody:
  content:
    'application/x-www-form-urlencoded':
      schema:
       type: object
       properties:
          name: 
            description: Updated name of the pet
            type: string
          status:
            description: Updated status of the pet
            type: string
       required:
         - status
responses:
  '200':
    description: Pet updated.
    content: 
      'application/json': {}
      'application/xml': {}
  '405':
    description: Method Not Allowed
    content: 
      'application/json': {}
      'application/xml': {}
security:
- petstore_auth:
  - write:pets
  - read:pets
```

### External Documentation Object

Allows referencing an external resource for extended documentation.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| description | `string` | A description of the target documentation. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| url | `string` | **_REQUIRED_**. The URL for the target documentation. This _MUST_ be in the form of a URL. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### External Documentation Object Example

```

{
  "description": "Find more info here",
  "url": "https://example.com"
}
```

```

description: Find more info here
url: https://example.com
```

### Parameter Object

Describes a single operation parameter.

A unique parameter is defined by a combination of a [name](https://spec.openapis.org/oas/v3.1.0.html#parameterName) and [location](https://spec.openapis.org/oas/v3.1.0.html#parameterIn).

#### Parameter Locations

There are four possible parameter locations specified by the `in` field:

-   path - Used together with [Path Templating](https://spec.openapis.org/oas/v3.1.0.html#pathTemplating), where the parameter value is actually part of the operation’s URL. This does not include the host or base path of the API. For example, in `/items/{itemId}`, the path parameter is `itemId`.
-   query - Parameters that are appended to the URL. For example, in `/items?id=###`, the query parameter is `id`.
-   header - Custom headers that are expected as part of the request. Note that \[[RFC7230](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7230)\] states header names are case insensitive.
-   cookie - Used to pass a specific cookie value to the API.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| name | `string` | **_REQUIRED_**. The name of the parameter. Parameter names are _case sensitive_.
-   If [`in`](https://spec.openapis.org/oas/v3.1.0.html#parameterIn) is `"path"`, the `name` field _MUST_ correspond to a template expression occurring within the [path](https://spec.openapis.org/oas/v3.1.0.html#pathsPath) field in the [Paths Object](https://spec.openapis.org/oas/v3.1.0.html#pathsObject). See [Path Templating](https://spec.openapis.org/oas/v3.1.0.html#pathTemplating) for further information.
-   If [`in`](https://spec.openapis.org/oas/v3.1.0.html#parameterIn) is `"header"` and the `name` field is `"Accept"`, `"Content-Type"` or `"Authorization"`, the parameter definition _SHALL_ be ignored.
-   For all other cases, the `name` corresponds to the parameter name used by the [`in`](https://spec.openapis.org/oas/v3.1.0.html#parameterIn) property.

 |
| in | `string` | **_REQUIRED_**. The location of the parameter. Possible values are `"query"`, `"header"`, `"path"` or `"cookie"`. |
| description | `string` | A brief description of the parameter. This could contain examples of use. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| required | `boolean` | Determines whether this parameter is mandatory. If the [parameter location](https://spec.openapis.org/oas/v3.1.0.html#parameterIn) is `"path"`, this property is **_REQUIRED_** and its value _MUST_ be `true`. Otherwise, the property _MAY_ be included and its default value is `false`. |
| deprecated | `boolean` | Specifies that a parameter is deprecated and _SHOULD_ be transitioned out of usage. Default value is `false`. |
| allowEmptyValue | `boolean` | Sets the ability to pass empty-valued parameters. This is valid only for `query` parameters and allows sending a parameter with an empty value. Default value is `false`. If [`style`](https://spec.openapis.org/oas/v3.1.0.html#parameterStyle) is used, and if behavior is `n/a` (cannot be serialized), the value of `allowEmptyValue` _SHALL_ be ignored. Use of this property is _NOT RECOMMENDED_, as it is likely to be removed in a later revision. |

The rules for serialization of the parameter are specified in one of two ways. For simpler scenarios, a [`schema`](https://spec.openapis.org/oas/v3.1.0.html#parameterSchema) and [`style`](https://spec.openapis.org/oas/v3.1.0.html#parameterStyle) can describe the structure and syntax of the parameter.

| Field Name | Type | Description |
| --- | --- | --- |
| style | `string` | Describes how the parameter value will be serialized depending on the type of the parameter value. Default values (based on value of `in`): for `query` - `form`; for `path` - `simple`; for `header` - `simple`; for `cookie` - `form`. |
| explode | `boolean` | When this is true, parameter values of type `array` or `object` generate separate parameters for each value of the array or key-value pair of the map. For other types of parameters this property has no effect. When [`style`](https://spec.openapis.org/oas/v3.1.0.html#parameterStyle) is `form`, the default value is `true`. For all other styles, the default value is `false`. |
| allowReserved | `boolean` | Determines whether the parameter value _SHOULD_ allow reserved characters, as defined by \[[RFC3986](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC3986)\] `:/?#[]@!$&'()*+,;=` to be included without percent-encoding. This property only applies to parameters with an `in` value of `query`. The default value is `false`. |
| schema | [Schema Object](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) | The schema defining the type used for the parameter. |
| example | Any | Example of the parameter’s potential value. The example _SHOULD_ match the specified schema and encoding properties if present. The `example` field is mutually exclusive of the `examples` field. Furthermore, if referencing a `schema` that contains an example, the `example` value _SHALL_ _override_ the example provided by the schema. To represent examples of media types that cannot naturally be represented in JSON or YAML, a string value can contain the example with escaping where necessary. |
| examples | Map\[ `string`, [Example Object](https://spec.openapis.org/oas/v3.1.0.html#exampleObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | Examples of the parameter’s potential value. Each example _SHOULD_ contain a value in the correct format as specified in the parameter encoding. The `examples` field is mutually exclusive of the `example` field. Furthermore, if referencing a `schema` that contains an example, the `examples` value _SHALL_ _override_ the example provided by the schema. |

For more complex scenarios, the [`content`](https://spec.openapis.org/oas/v3.1.0.html#parameterContent) property can define the media type and schema of the parameter. A parameter _MUST_ contain either a `schema` property, or a `content` property, but not both. When `example` or `examples` are provided in conjunction with the `schema` object, the example _MUST_ follow the prescribed serialization strategy for the parameter.

| Field Name | Type | Description |
| --- | --- | --- |
| content | Map\[`string`, [Media Type Object](https://spec.openapis.org/oas/v3.1.0.html#mediaTypeObject)\] | A map containing the representations for the parameter. The key is the media type and the value describes it. The map _MUST_ only contain one entry. |

#### Style Values

In order to support common ways of serializing simple parameters, a set of `style` values are defined.

| `style` | [`type`](https://spec.openapis.org/oas/v3.1.0.html#dataTypes) | `in` | Comments |
| --- | --- | --- | --- |
| matrix | `primitive`, `array`, `object` | `path` | Path-style parameters defined by \[[RFC6570](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6570)\] |
| label | `primitive`, `array`, `object` | `path` | Label style parameters defined by \[[RFC6570](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6570)\] |
| form | `primitive`, `array`, `object` | `query`, `cookie` | Form style parameters defined by \[[RFC6570](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6570)\]. This option replaces `collectionFormat` with a `csv` (when `explode` is false) or `multi` (when `explode` is true) value from OpenAPI 2.0. |
| simple | `array` | `path`, `header` | Simple style parameters defined by \[[RFC6570](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6570)\]. This option replaces `collectionFormat` with a `csv` value from OpenAPI 2.0. |
| spaceDelimited | `array`, `object` | `query` | Space separated array or object values. This option replaces `collectionFormat` equal to `ssv` from OpenAPI 2.0. |
| pipeDelimited | `array`, `object` | `query` | Pipe separated array or object values. This option replaces `collectionFormat` equal to `pipes` from OpenAPI 2.0. |
| deepObject | `object` | `query` | Provides a simple way of rendering nested objects using form parameters. |

#### Style Examples

Assume a parameter named `color` has one of the following values:

```

   string -> "blue"
   array -> ["blue","black","brown"]
   object -> { "R": 100, "G": 200, "B": 150 }
```

The following table shows examples of rendering differences for each value.

| [`style`](https://spec.openapis.org/oas/v3.1.0.html#styleValues) | `explode` | `empty` | `string` | `array` | `object` |
| --- | --- | --- | --- | --- | --- |
| matrix | false | ;color | ;color=blue | ;color=blue,black,brown | ;color=R,100,G,200,B,150 |
| matrix | true | ;color | ;color=blue | ;color=blue;color=black;color=brown | ;R=100;G=200;B=150 |
| label | false | . | .blue | .blue.black.brown | .R.100.G.200.B.150 |
| label | true | . | .blue | .blue.black.brown | .R=100.G=200.B=150 |
| form | false | color= | color=blue | color=blue,black,brown | color=R,100,G,200,B,150 |
| form | true | color= | color=blue | color=blue&color=black&color=brown | R=100&G=200&B=150 |
| simple | false | n/a | blue | blue,black,brown | R,100,G,200,B,150 |
| simple | true | n/a | blue | blue,black,brown | R=100,G=200,B=150 |
| spaceDelimited | false | n/a | n/a | blue%20black%20brown | R%20100%20G%20200%20B%20150 |
| pipeDelimited | false | n/a | n/a | blue|black|brown | R|100|G|200|B|150 |
| deepObject | true | n/a | n/a | n/a | color\[R\]=100&color\[G\]=200&color\[B\]=150 |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Parameter Object Examples

A header parameter with an array of 64 bit integer numbers:

```

{
  "name": "token",
  "in": "header",
  "description": "token to be passed as a header",
  "required": true,
  "schema": {
    "type": "array",
    "items": {
      "type": "integer",
      "format": "int64"
    }
  },
  "style": "simple"
}
```

```

name: token
in: header
description: token to be passed as a header
required: true
schema:
  type: array
  items:
    type: integer
    format: int64
style: simple
```

A path parameter of a string value:

```

{
  "name": "username",
  "in": "path",
  "description": "username to fetch",
  "required": true,
  "schema": {
    "type": "string"
  }
}
```

```

name: username
in: path
description: username to fetch
required: true
schema:
  type: string
```

An optional query parameter of a string value, allowing multiple values by repeating the query parameter:

```

{
  "name": "id",
  "in": "query",
  "description": "ID of the object to fetch",
  "required": false,
  "schema": {
    "type": "array",
    "items": {
      "type": "string"
    }
  },
  "style": "form",
  "explode": true
}
```

```

name: id
in: query
description: ID of the object to fetch
required: false
schema:
  type: array
  items:
    type: string
style: form
explode: true
```

A free-form query parameter, allowing undefined parameters of a specific type:

```

{
  "in": "query",
  "name": "freeForm",
  "schema": {
    "type": "object",
    "additionalProperties": {
      "type": "integer"
    },
  },
  "style": "form"
}
```

```

in: query
name: freeForm
schema:
  type: object
  additionalProperties:
    type: integer
style: form
```

A complex parameter using `content` to define serialization:

```

{
  "in": "query",
  "name": "coordinates",
  "content": {
    "application/json": {
      "schema": {
        "type": "object",
        "required": [
          "lat",
          "long"
        ],
        "properties": {
          "lat": {
            "type": "number"
          },
          "long": {
            "type": "number"
          }
        }
      }
    }
  }
}
```

```

in: query
name: coordinates
content:
  application/json:
    schema:
      type: object
      required:
        - lat
        - long
      properties:
        lat:
          type: number
        long:
          type: number
```

### Request Body Object

Describes a single request body.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| description | `string` | A brief description of the request body. This could contain examples of use. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| content | Map\[`string`, [Media Type Object](https://spec.openapis.org/oas/v3.1.0.html#mediaTypeObject)\] | **_REQUIRED_**. The content of the request body. The key is a media type or [media type range](https://tools.ietf.org/html/rfc7231#appendix-D) and the value describes it. For requests that match multiple keys, only the most specific key is applicable. e.g. text/plain overrides text/\* |
| required | `boolean` | Determines if the request body is required in the request. Defaults to `false`. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Request Body Examples

A request body with a referenced model definition.

```

{
  "description": "user to add to the system",
  "content": {
    "application/json": {
      "schema": {
        "$ref": "#/components/schemas/User"
      },
      "examples": {
          "user" : {
            "summary": "User Example", 
            "externalValue": "https://foo.bar/examples/user-example.json"
          } 
        }
    },
    "application/xml": {
      "schema": {
        "$ref": "#/components/schemas/User"
      },
      "examples": {
          "user" : {
            "summary": "User example in XML",
            "externalValue": "https://foo.bar/examples/user-example.xml"
          }
        }
    },
    "text/plain": {
      "examples": {
        "user" : {
            "summary": "User example in Plain text",
            "externalValue": "https://foo.bar/examples/user-example.txt" 
        }
      } 
    },
    "*/*": {
      "examples": {
        "user" : {
            "summary": "User example in other format",
            "externalValue": "https://foo.bar/examples/user-example.whatever"
        }
      }
    }
  }
}
```

```

description: user to add to the system
content: 
  'application/json':
    schema:
      $ref: '#/components/schemas/User'
    examples:
      user:
        summary: User Example
        externalValue: 'https://foo.bar/examples/user-example.json'
  'application/xml':
    schema:
      $ref: '#/components/schemas/User'
    examples:
      user:
        summary: User example in XML
        externalValue: 'https://foo.bar/examples/user-example.xml'
  'text/plain':
    examples:
      user:
        summary: User example in Plain text
        externalValue: 'https://foo.bar/examples/user-example.txt'
  '*/*':
    examples:
      user: 
        summary: User example in other format
        externalValue: 'https://foo.bar/examples/user-example.whatever'
```

A body parameter that is an array of string values:

```

{
  "description": "user to add to the system",
  "required": true,
  "content": {
    "text/plain": {
      "schema": {
        "type": "array",
        "items": {
          "type": "string"
        }
      }
    }
  }
}
```

```

description: user to add to the system
required: true
content:
  text/plain:
    schema:
      type: array
      items:
        type: string
```

### Media Type Object

Each Media Type Object provides schema and examples for the media type identified by its key.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| schema | [Schema Object](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) | The schema defining the content of the request, response, or parameter. |
| example | Any | Example of the media type. The example object _SHOULD_ be in the correct format as specified by the media type. The `example` field is mutually exclusive of the `examples` field. Furthermore, if referencing a `schema` which contains an example, the `example` value _SHALL_ _override_ the example provided by the schema. |
| examples | Map\[ `string`, [Example Object](https://spec.openapis.org/oas/v3.1.0.html#exampleObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | Examples of the media type. Each example object _SHOULD_ match the media type and specified schema if present. The `examples` field is mutually exclusive of the `example` field. Furthermore, if referencing a `schema` which contains an example, the `examples` value _SHALL_ _override_ the example provided by the schema. |
| encoding | Map\[`string`, [Encoding Object](https://spec.openapis.org/oas/v3.1.0.html#encodingObject)\] | A map between a property name and its encoding information. The key, being the property name, _MUST_ exist in the schema as a property. The encoding object _SHALL_ only apply to `requestBody` objects when the media type is `multipart` or `application/x-www-form-urlencoded`. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Media Type Examples

```

{
  "application/json": {
    "schema": {
         "$ref": "#/components/schemas/Pet"
    },
    "examples": {
      "cat" : {
        "summary": "An example of a cat",
        "value": 
          {
            "name": "Fluffy",
            "petType": "Cat",
            "color": "White",
            "gender": "male",
            "breed": "Persian"
          }
      },
      "dog": {
        "summary": "An example of a dog with a cat's name",
        "value" :  { 
          "name": "Puma",
          "petType": "Dog",
          "color": "Black",
          "gender": "Female",
          "breed": "Mixed"
        },
      "frog": {
          "$ref": "#/components/examples/frog-example"
        }
      }
    }
  }
}
```

```

application/json: 
  schema:
    $ref: "#/components/schemas/Pet"
  examples:
    cat:
      summary: An example of a cat
      value:
        name: Fluffy
        petType: Cat
        color: White
        gender: male
        breed: Persian
    dog:
      summary: An example of a dog with a cat's name
      value:
        name: Puma
        petType: Dog
        color: Black
        gender: Female
        breed: Mixed
    frog:
      $ref: "#/components/examples/frog-example"
```

#### Considerations for File Uploads

In contrast with the 2.0 specification, `file` input/output content in OpenAPI is described with the same semantics as any other schema type.

In contrast with the 3.0 specification, the `format` keyword has no effect on the content-encoding of the schema. JSON Schema offers a `contentEncoding` keyword, which may be used to specify the `Content-Encoding` for the schema. The `contentEncoding` keyword supports all encodings defined in \[[RFC4648](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC4648)\], including “base64” and “base64url”, as well as “quoted-printable” from \[[RFC2045](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC2045)\]. The encoding specified by the `contentEncoding` keyword is independent of an encoding specified by the `Content-Type` header in the request or response or metadata of a multipart body – when both are present, the encoding specified in the `contentEncoding` is applied first and then the encoding specified in the `Content-Type` header.

JSON Schema also offers a `contentMediaType` keyword. However, when the media type is already specified by the Media Type Object’s key, or by the `contentType` field of an [Encoding Object](https://spec.openapis.org/oas/v3.1.0.html#encodingObject), the `contentMediaType` keyword _SHALL_ be ignored if present.

Examples:

Content transferred in binary (octet-stream) _MAY_ omit `schema`:

```

# a PNG image as a binary file:
content:
    image/png: {}
```

```

# an arbitrary binary file:
content:
    application/octet-stream: {}
```

Binary content transferred with base64 encoding:

```

content:
    image/png:
        schema:
            type: string
            contentMediaType: image/png
            contentEncoding: base64
```

Note that the `Content-Type` remains `image/png`, describing the semantics of the payload. The JSON Schema `type` and `contentEncoding` fields explain that the payload is transferred as text. The JSON Schema `contentMediaType` is technically redundant, but can be used by JSON Schema tools that may not be aware of the OpenAPI context.

These examples apply to either input payloads of file uploads or response payloads.

A `requestBody` for submitting a file in a `POST` operation may look like the following example:

```

requestBody:
  content:
    application/octet-stream: {}
```

In addition, specific media types _MAY_ be specified:

```

# multiple, specific media types may be specified:
requestBody:
  content:
    # a binary file of type png or jpeg
    image/jpeg: {}
    image/png: {}
```

To upload multiple files, a `multipart` media type _MUST_ be used:

```

requestBody:
  content:
    multipart/form-data:
      schema:
        properties:
          # The property name 'file' will be used for all files.
          file:
            type: array
            items: {}
```

As seen in the section on `multipart/form-data` below, the empty schema for `items` indicates a media type of `application/octet-stream`.

#### Support for x-www-form-urlencoded Request Bodies

To submit content using form url encoding via \[[RFC1866](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC1866)\], the following definition may be used:

```

requestBody:
  content:
    application/x-www-form-urlencoded:
      schema:
        type: object
        properties:
          id:
            type: string
            format: uuid
          address:
            # complex types are stringified to support RFC 1866
            type: object
            properties: {}
```

In this example, the contents in the `requestBody` _MUST_ be stringified per \[[RFC1866](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC1866)\] when passed to the server. In addition, the `address` field complex object will be stringified.

When passing complex objects in the `application/x-www-form-urlencoded` content type, the default serialization strategy of such properties is described in the [`Encoding Object`](https://spec.openapis.org/oas/v3.1.0.html#encodingObject)’s [`style`](https://spec.openapis.org/oas/v3.1.0.html#encodingStyle) property as `form`.

#### Special Considerations for `multipart` Content

It is common to use `multipart/form-data` as a `Content-Type` when transferring request bodies to operations. In contrast to 2.0, a `schema` is _REQUIRED_ to define the input parameters to the operation when using `multipart` content. This supports complex structures as well as supporting mechanisms for multiple file uploads.

In a `multipart/form-data` request body, each schema property, or each element of a schema array property, takes a section in the payload with an internal header as defined by \[[RFC7578](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7578)\]. The serialization strategy for each property of a `multipart/form-data` request body can be specified in an associated [`Encoding Object`](https://spec.openapis.org/oas/v3.1.0.html#encodingObject).

When passing in `multipart` types, boundaries _MAY_ be used to separate sections of the content being transferred – thus, the following default `Content-Type`s are defined for `multipart`:

-   If the property is a primitive, or an array of primitive values, the default Content-Type is `text/plain`
-   If the property is complex, or an array of complex values, the default Content-Type is `application/json`
-   If the property is a `type: string` with a `contentEncoding`, the default Content-Type is `application/octet-stream`

Per the JSON Schema specification, `contentMediaType` without `contentEncoding` present is treated as if `contentEncoding: identity` were present. While useful for embedding text documents such as `text/html` into JSON strings, it is not useful for a `multipart/form-data` part, as it just causes the document to be treated as `text/plain` instead of its actual media type. Use the Encoding Object without `contentMediaType` if no `contentEncoding` is required.

Examples:

```

requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          id:
            type: string
            format: uuid
          address:
            # default Content-Type for objects is `application/json`
            type: object
            properties: {}
          profileImage:
            # Content-Type for application-level encoded resource is `text/plain`
            type: string
            contentMediaType: image/png
            contentEncoding: base64
          children:
            # default Content-Type for arrays is based on the _inner_ type (`text/plain` here)
            type: array
            items:
              type: string
          addresses:
            # default Content-Type for arrays is based on the _inner_ type (object shown, so `application/json` in this example)
            type: array
            items:
              type: object
              $ref: '#/components/schemas/Address'
```

An `encoding` attribute is introduced to give you control over the serialization of parts of `multipart` request bodies. This attribute is _only_ applicable to `multipart` and `application/x-www-form-urlencoded` request bodies.

### Encoding Object

A single encoding definition applied to a single schema property.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| contentType | `string` | The Content-Type for encoding a specific property. Default value depends on the property type: for `object` - `application/json`; for `array` – the default is defined based on the inner type; for all other cases the default is `application/octet-stream`. The value can be a specific media type (e.g. `application/json`), a wildcard media type (e.g. `image/*`), or a comma-separated list of the two types. |
| headers | Map\[`string`, [Header Object](https://spec.openapis.org/oas/v3.1.0.html#headerObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | A map allowing additional information to be provided as headers, for example `Content-Disposition`. `Content-Type` is described separately and _SHALL_ be ignored in this section. This property _SHALL_ be ignored if the request body media type is not a `multipart`. |
| style | `string` | Describes how a specific property value will be serialized depending on its type. See [Parameter Object](https://spec.openapis.org/oas/v3.1.0.html#parameterObject) for details on the [`style`](https://spec.openapis.org/oas/v3.1.0.html#parameterStyle) property. The behavior follows the same values as `query` parameters, including default values. This property _SHALL_ be ignored if the request body media type is not `application/x-www-form-urlencoded` or `multipart/form-data`. If a value is explicitly defined, then the value of [`contentType`](https://spec.openapis.org/oas/v3.1.0.html#encodingContentType) (implicit or explicit) _SHALL_ be ignored. |
| explode | `boolean` | When this is true, property values of type `array` or `object` generate separate parameters for each value of the array, or key-value-pair of the map. For other types of properties this property has no effect. When [`style`](https://spec.openapis.org/oas/v3.1.0.html#encodingStyle) is `form`, the default value is `true`. For all other styles, the default value is `false`. This property _SHALL_ be ignored if the request body media type is not `application/x-www-form-urlencoded` or `multipart/form-data`. If a value is explicitly defined, then the value of [`contentType`](https://spec.openapis.org/oas/v3.1.0.html#encodingContentType) (implicit or explicit) _SHALL_ be ignored. |
| allowReserved | `boolean` | Determines whether the parameter value _SHOULD_ allow reserved characters, as defined by \[[RFC3986](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC3986)\] `:/?#[]@!$&'()*+,;=` to be included without percent-encoding. The default value is `false`. This property _SHALL_ be ignored if the request body media type is not `application/x-www-form-urlencoded` or `multipart/form-data`. If a value is explicitly defined, then the value of [`contentType`](https://spec.openapis.org/oas/v3.1.0.html#encodingContentType) (implicit or explicit) _SHALL_ be ignored. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Encoding Object Example

```

requestBody:
  content:
    multipart/form-data:
      schema:
        type: object
        properties:
          id:
            # default is text/plain
            type: string
            format: uuid
          address:
            # default is application/json
            type: object
            properties: {}
          historyMetadata:
            # need to declare XML format!
            description: metadata in XML format
            type: object
            properties: {}
          profileImage: {}
      encoding:
        historyMetadata:
          # require XML Content-Type in utf-8 encoding
          contentType: application/xml; charset=utf-8
        profileImage:
          # only accept png/jpeg
          contentType: image/png, image/jpeg
          headers:
            X-Rate-Limit-Limit:
              description: The number of allowed requests in the current period
              schema:
                type: integer
```

### Responses Object

A container for the expected responses of an operation. The container maps a HTTP response code to the expected response.

The documentation is not necessarily expected to cover all possible HTTP response codes because they may not be known in advance. However, documentation is expected to cover a successful operation response and any known errors.

The `default` _MAY_ be used as a default response object for all HTTP codes that are not covered individually by the `Responses Object`.

The `Responses Object` _MUST_ contain at least one response code, and if only one response code is provided it _SHOULD_ be the response for a successful operation call.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| default | [Response Object](https://spec.openapis.org/oas/v3.1.0.html#responseObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) | The documentation of responses other than the ones declared for specific HTTP response codes. Use this field to cover undeclared responses. |

#### Patterned Fields

| Field Pattern | Type | Description |
| --- | --- | --- |
| [HTTP Status Code](https://spec.openapis.org/oas/v3.1.0.html#httpCodes) | [Response Object](https://spec.openapis.org/oas/v3.1.0.html#responseObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) | Any [HTTP status code](https://spec.openapis.org/oas/v3.1.0.html#httpCodes) can be used as the property name, but only one property per code, to describe the expected response for that HTTP status code. This field _MUST_ be enclosed in quotation marks (for example, “200”) for compatibility between JSON and YAML. To define a range of response codes, this field _MAY_ contain the uppercase wildcard character `X`. For example, `2XX` represents all response codes between `[200-299]`. Only the following range definitions are allowed: `1XX`, `2XX`, `3XX`, `4XX`, and `5XX`. If a response is defined using an explicit code, the explicit code definition takes precedence over the range definition for that code. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Responses Object Example

A 200 response for a successful operation and a default response for others (implying an error):

```

{
  "200": {
    "description": "a pet to be returned",
    "content": {
      "application/json": {
        "schema": {
          "$ref": "#/components/schemas/Pet"
        }
      }
    }
  },
  "default": {
    "description": "Unexpected error",
    "content": {
      "application/json": {
        "schema": {
          "$ref": "#/components/schemas/ErrorModel"
        }
      }
    }
  }
}
```

```

'200':
  description: a pet to be returned
  content: 
    application/json:
      schema:
        $ref: '#/components/schemas/Pet'
default:
  description: Unexpected error
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/ErrorModel'
```

### Response Object

Describes a single response from an API Operation, including design-time, static `links` to operations based on the response.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| description | `string` | **_REQUIRED_**. A description of the response. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| headers | Map\[`string`, [Header Object](https://spec.openapis.org/oas/v3.1.0.html#headerObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | Maps a header name to its definition. \[[RFC7230](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7230)\] states header names are case insensitive. If a response header is defined with the name `"Content-Type"`, it _SHALL_ be ignored. |
| content | Map\[`string`, [Media Type Object](https://spec.openapis.org/oas/v3.1.0.html#mediaTypeObject)\] | A map containing descriptions of potential response payloads. The key is a media type or [media type range](https://tools.ietf.org/html/rfc7231#appendix-D) and the value describes it. For responses that match multiple keys, only the most specific key is applicable. e.g. text/plain overrides text/\* |
| links | Map\[`string`, [Link Object](https://spec.openapis.org/oas/v3.1.0.html#linkObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject)\] | A map of operations links that can be followed from the response. The key of the map is a short name for the link, following the naming constraints of the names for [Component Objects](https://spec.openapis.org/oas/v3.1.0.html#componentsObject). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Response Object Examples

Response of an array of a complex type:

```

{
  "description": "A complex object array response",
  "content": {
    "application/json": {
      "schema": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/VeryComplexType"
        }
      }
    }
  }
}
```

```

description: A complex object array response
content: 
  application/json:
    schema: 
      type: array
      items:
        $ref: '#/components/schemas/VeryComplexType'
```

Response with a string type:

```

{
  "description": "A simple string response",
  "content": {
    "text/plain": {
      "schema": {
        "type": "string"
      }
    }
  }

}
```

```

description: A simple string response
content:
  text/plain:
    schema:
      type: string
```

Plain text response with headers:

```

{
  "description": "A simple string response",
  "content": {
    "text/plain": {
      "schema": {
        "type": "string",
        "example": "whoa!"
      }
    }
  },
  "headers": {
    "X-Rate-Limit-Limit": {
      "description": "The number of allowed requests in the current period",
      "schema": {
        "type": "integer"
      }
    },
    "X-Rate-Limit-Remaining": {
      "description": "The number of remaining requests in the current period",
      "schema": {
        "type": "integer"
      }
    },
    "X-Rate-Limit-Reset": {
      "description": "The number of seconds left in the current period",
      "schema": {
        "type": "integer"
      }
    }
  }
}
```

```

description: A simple string response
content:
  text/plain:
    schema:
      type: string
    example: 'whoa!'
headers:
  X-Rate-Limit-Limit:
    description: The number of allowed requests in the current period
    schema:
      type: integer
  X-Rate-Limit-Remaining:
    description: The number of remaining requests in the current period
    schema:
      type: integer
  X-Rate-Limit-Reset:
    description: The number of seconds left in the current period
    schema:
      type: integer
```

Response with no return value:

```

{
  "description": "object created"
}
```

```

description: object created
```

### Callback Object

A map of possible out-of band callbacks related to the parent operation. Each value in the map is a [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) that describes a set of requests that may be initiated by the API provider and the expected responses. The key value used to identify the path item object is an expression, evaluated at runtime, that identifies a URL to use for the callback operation.

To describe incoming requests from the API provider independent from another API call, use the [`webhooks`](https://spec.openapis.org/oas/v3.1.0.html#oasWebhooks) field.

#### Patterned Fields

| Field Pattern | Type | Description |
| --- | --- | --- |
| {expression} | [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) | [Reference Object](https://spec.openapis.org/oas/v3.1.0.html#referenceObject) | A Path Item Object, or a reference to one, used to define a callback request and expected responses. A [complete example](https://github.com/OAI/OpenAPI-Specification/tree/master/examples/v3.0/callback-example.yaml) is available. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Key Expression

The key that identifies the [Path Item Object](https://spec.openapis.org/oas/v3.1.0.html#pathItemObject) is a [runtime expression](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression) that can be evaluated in the context of a runtime HTTP request/response to identify the URL to be used for the callback request. A simple example might be `$request.body#/url`. However, using a [runtime expression](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression) the complete HTTP message can be accessed. This includes accessing any part of a body that a JSON Pointer \[[RFC6901](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6901)\] can reference.

For example, given the following HTTP request:

```

POST /subscribe/myevent?queryUrl=https://clientdomain.com/stillrunning HTTP/1.1
Host: example.org
Content-Type: application/json
Content-Length: 187

{
  "failedUrl" : "https://clientdomain.com/failed",
  "successUrls" : [
    "https://clientdomain.com/fast",
    "https://clientdomain.com/medium",
    "https://clientdomain.com/slow"
  ] 
}

201 Created
Location: https://example.org/subscription/1
```

The following examples show how the various expressions evaluate, assuming the callback operation has a path parameter named `eventType` and a query parameter named `queryUrl`.

| Expression | Value |
| --- | --- |
| $url | [https://example.org/subscribe/myevent?queryUrl=https://clientdomain.com/stillrunning](https://example.org/subscribe/myevent?queryUrl=https://clientdomain.com/stillrunning) |
| $method | POST |
| $request.path.eventType | myevent |
| $request.query.queryUrl | [https://clientdomain.com/stillrunning](https://clientdomain.com/stillrunning) |
| $request.header.content-Type | application/json |
| $request.body#/failedUrl | [https://clientdomain.com/failed](https://clientdomain.com/failed) |
| $request.body#/successUrls/2 | [https://clientdomain.com/medium](https://clientdomain.com/medium) |
| $response.header.Location | [https://example.org/subscription/1](https://example.org/subscription/1) |

#### Callback Object Examples

The following example uses the user provided `queryUrl` query string parameter to define the callback URL. This is an example of how to use a callback object to describe a WebHook callback that goes with the subscription operation to enable registering for the WebHook.

```

myCallback:
  '{$request.query.queryUrl}':
    post:
      requestBody:
        description: Callback payload
        content:
          'application/json':
            schema:
              $ref: '#/components/schemas/SomePayload'
      responses:
        '200':
          description: callback successfully processed
```

The following example shows a callback where the server is hard-coded, but the query string parameters are populated from the `id` and `email` property in the request body.

```

transactionCallback:
  'http://notificationServer.com?transactionId={$request.body#/id}&email={$request.body#/email}':
    post:
      requestBody:
        description: Callback payload
        content:
          'application/json':
            schema:
              $ref: '#/components/schemas/SomePayload'
      responses:
        '200':
          description: callback successfully processed
```

### Example Object

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| summary | `string` | Short description for the example. |
| description | `string` | Long description for the example. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| value | Any | Embedded literal example. The `value` field and `externalValue` field are mutually exclusive. To represent examples of media types that cannot naturally represented in JSON or YAML, use a string value to contain the example, escaping where necessary. |
| externalValue | `string` | A URI that points to the literal example. This provides the capability to reference examples that cannot easily be included in JSON or YAML documents. The `value` field and `externalValue` field are mutually exclusive. See the rules for resolving [Relative References](https://spec.openapis.org/oas/v3.1.0.html#relativeReferencesURI). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

In all cases, the example value is expected to be compatible with the type schema of its associated value. Tooling implementations _MAY_ choose to validate compatibility automatically, and reject the example value(s) if incompatible.

#### Example Object Examples

In a request body:

```

requestBody:
  content:
    'application/json':
      schema:
        $ref: '#/components/schemas/Address'
      examples: 
        foo:
          summary: A foo example
          value: {"foo": "bar"}
        bar:
          summary: A bar example
          value: {"bar": "baz"}
    'application/xml':
      examples: 
        xmlExample:
          summary: This is an example in XML
          externalValue: 'https://example.org/examples/address-example.xml'
    'text/plain':
      examples:
        textExample: 
          summary: This is a text example
          externalValue: 'https://foo.bar/examples/address-example.txt'
```

In a parameter:

```

parameters:
  - name: 'zipCode'
    in: 'query'
    schema:
      type: 'string'
      format: 'zip-code'
    examples:
      zip-example: 
        $ref: '#/components/examples/zip-example'
```

In a response:

```

responses:
  '200':
    description: your car appointment has been booked
    content: 
      application/json:
        schema:
          $ref: '#/components/schemas/SuccessResponse'
        examples:
          confirmation-success:
            $ref: '#/components/examples/confirmation-success'
```

### Link Object

The `Link object` represents a possible design-time link for a response. The presence of a link does not guarantee the caller’s ability to successfully invoke it, rather it provides a known relationship and traversal mechanism between responses and other operations.

Unlike _dynamic_ links (i.e. links provided **in** the response payload), the OAS linking mechanism does not require link information in the runtime response.

For computing links, and providing instructions to execute them, a [runtime expression](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression) is used for accessing values in an operation and using them as parameters while invoking the linked operation.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| operationRef | `string` | A relative or absolute URI reference to an OAS operation. This field is mutually exclusive of the `operationId` field, and _MUST_ point to an [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject). Relative `operationRef` values _MAY_ be used to locate an existing [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject) in the OpenAPI definition. See the rules for resolving [Relative References](https://spec.openapis.org/oas/v3.1.0.html#relativeReferencesURI). |
| operationId | `string` | The name of an _existing_, resolvable OAS operation, as defined with a unique `operationId`. This field is mutually exclusive of the `operationRef` field. |
| parameters | Map\[`string`, Any | [{expression}](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression)\] | A map representing parameters to pass to an operation as specified with `operationId` or identified via `operationRef`. The key is the parameter name to be used, whereas the value can be a constant or an expression to be evaluated and passed to the linked operation. The parameter name can be qualified using the [parameter location](https://spec.openapis.org/oas/v3.1.0.html#parameterIn) `[{in}.]{name}` for operations that use the same parameter name in different locations (e.g. [path.id](http://path.id/)). |
| requestBody | Any | [{expression}](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression) | A literal value or [{expression}](https://spec.openapis.org/oas/v3.1.0.html#runtimeExpression) to use as a request body when calling the target operation. |
| description | `string` | A description of the link. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| server | [Server Object](https://spec.openapis.org/oas/v3.1.0.html#serverObject) | A server object to be used by the target operation. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

A linked operation _MUST_ be identified using either an `operationRef` or `operationId`. In the case of an `operationId`, it _MUST_ be unique and resolved in the scope of the OAS document. Because of the potential for name clashes, the `operationRef` syntax is preferred for OpenAPI documents with external references.

#### Examples

Computing a link from a request operation where the `$request.path.id` is used to pass a request parameter to the linked operation.

```

paths:
  /users/{id}:
    parameters:
    - name: id
      in: path
      required: true
      description: the user identifier, as userId 
      schema:
        type: string
    get:
      responses:
        '200':
          description: the user being returned
          content:
            application/json:
              schema:
                type: object
                properties:
                  uuid: # the unique user id
                    type: string
                    format: uuid
          links:
            address:
              # the target link operationId
              operationId: getUserAddress
              parameters:
                # get the `id` field from the request path parameter named `id`
                userId: $request.path.id
  # the path item of the linked operation
  /users/{userid}/address:
    parameters:
    - name: userid
      in: path
      required: true
      description: the user identifier, as userId 
      schema:
        type: string
    # linked operation
    get:
      operationId: getUserAddress
      responses:
        '200':
          description: the user's address
```

When a runtime expression fails to evaluate, no parameter value is passed to the target operation.

Values from the response body can be used to drive a linked operation.

```

links:
  address:
    operationId: getUserAddressByUUID
    parameters:
      # get the `uuid` field from the `uuid` field in the response body
      userUuid: $response.body#/uuid
```

Clients follow all links at their discretion. Neither permissions, nor the capability to make a successful call to that link, is guaranteed solely by the existence of a relationship.

#### OperationRef Examples

As references to `operationId` _MAY_ NOT be possible (the `operationId` is an optional field in an [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject)), references _MAY_ also be made through a relative `operationRef`:

```

links:
  UserRepositories:
    # returns array of '#/components/schemas/repository'
    operationRef: '#/paths/~12.0~1repositories~1{username}/get'
    parameters:
      username: $response.body#/username
```

or an absolute `operationRef`:

```

links:
  UserRepositories:
    # returns array of '#/components/schemas/repository'
    operationRef: 'https://na2.gigantic-server.com/#/paths/~12.0~1repositories~1{username}/get'
    parameters:
      username: $response.body#/username
```

Note that in the use of `operationRef`, the _escaped forward-slash_ is necessary when using JSON references.

#### Runtime Expressions

Runtime expressions allow defining values based on information that will only be available within the HTTP message in an actual API call. This mechanism is used by [Link Objects](https://spec.openapis.org/oas/v3.1.0.html#linkObject) and [Callback Objects](https://spec.openapis.org/oas/v3.1.0.html#callbackObject).

The runtime expression is defined by the following [ABNF](https://tools.ietf.org/html/rfc5234) syntax

```

      expression = ( "$url" / "$method" / "$statusCode" / "$request." source / "$response." source )
      source = ( header-reference / query-reference / path-reference / body-reference )
      header-reference = "header." token
      query-reference = "query." name  
      path-reference = "path." name
      body-reference = "body" ["#" json-pointer ]
      json-pointer    = *( "/" reference-token )
      reference-token = *( unescaped / escaped )
      unescaped       = %x00-2E / %x30-7D / %x7F-10FFFF
         ; %x2F ('/') and %x7E ('~') are excluded from 'unescaped'
      escaped         = "~" ( "0" / "1" )
        ; representing '~' and '/', respectively
      name = *( CHAR )
      token = 1*tchar
      tchar = "!" / "#" / "$" / "%" / "&" / "'" / "*" / "+" / "-" / "." /
        "^" / "_" / "`" / "|" / "~" / DIGIT / ALPHA
```

Here, `json-pointer` is taken from \[[RFC6901](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6901)\], `char` from \[[RFC7159](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7159)\] and `token` from \[[RFC7230](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7230)\].

The `name` identifier is case-sensitive, whereas `token` is not.

The table below provides examples of runtime expressions and examples of their use in a value:

#### Examples

| Source Location | example expression | notes |
| --- | --- | --- |
| HTTP Method | `$method` | The allowable values for the `$method` will be those for the HTTP operation. |
| Requested media type | `$request.header.accept` |  |
| Request parameter | `$request.path.id` | Request parameters _MUST_ be declared in the `parameters` section of the parent operation or they cannot be evaluated. This includes request headers. |
| Request body property | `$request.body#/user/uuid` | In operations which accept payloads, references may be made to portions of the `requestBody` or the entire body. |
| Request URL | `$url` |  |
| Response value | `$response.body#/status` | In operations which return payloads, references may be made to portions of the response body or the entire body. |
| Response header | `$response.header.Server` | Single header values only are available |

Runtime expressions preserve the type of the referenced value. Expressions can be embedded into string values by surrounding the expression with `{}` curly braces.

The Header Object follows the structure of the [Parameter Object](https://spec.openapis.org/oas/v3.1.0.html#parameterObject) with the following changes:

1.  `name` _MUST NOT_ be specified, it is given in the corresponding `headers` map.
2.  `in` _MUST NOT_ be specified, it is implicitly in `header`.
3.  All traits that are affected by the location _MUST_ be applicable to a location of `header` (for example, [`style`](https://spec.openapis.org/oas/v3.1.0.html#parameterStyle)).

#### Header Object Example

A simple header of type `integer`:

```

{
  "description": "The number of allowed requests in the current period",
  "schema": {
    "type": "integer"
  }
}
```

```

description: The number of allowed requests in the current period
schema:
  type: integer
```

### Tag Object

Adds metadata to a single tag that is used by the [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject). It is not mandatory to have a Tag Object per tag defined in the Operation Object instances.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| name | `string` | **_REQUIRED_**. The name of the tag. |
| description | `string` | A description for the tag. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| externalDocs | [External Documentation Object](https://spec.openapis.org/oas/v3.1.0.html#externalDocumentationObject) | Additional external documentation for this tag. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Tag Object Example

```

{
"name": "pet",
"description": "Pets operations"
}
```

```

name: pet
description: Pets operations
```

### Reference Object

A simple object to allow referencing other components in the OpenAPI document, internally and externally.

The `$ref` string value contains a URI \[[RFC3986](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC3986)\], which identifies the location of the value being referenced.

See the rules for resolving [Relative References](https://spec.openapis.org/oas/v3.1.0.html#relativeReferencesURI).

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| $ref | `string` | **_REQUIRED_**. The reference identifier. This _MUST_ be in the form of a URI. |
| summary | `string` | A short summary which by default _SHOULD_ override that of the referenced component. If the referenced object-type does not allow a `summary` field, then this field has no effect. |
| description | `string` | A description which by default _SHOULD_ override that of the referenced component. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. If the referenced object-type does not allow a `description` field, then this field has no effect. |

This object cannot be extended with additional properties and any properties added _SHALL_ be ignored.

Note that this restriction on additional properties is a difference between Reference Objects and [`Schema Objects`](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) that contain a `$ref` keyword.

#### Reference Object Example

```

{
"$ref": "#/components/schemas/Pet"
}
```

```

$ref: '#/components/schemas/Pet'
```

#### Relative Schema Document Example

```

{
  "$ref": "Pet.json"
}
```

```

$ref: Pet.yaml
```

#### Relative Documents With Embedded Schema Example

```

{
  "$ref": "definitions.json#/Pet"
}
```

```

$ref: definitions.yaml#/Pet
```

### Schema Object

The Schema Object allows the definition of input and output data types. These types can be objects, but also primitives and arrays. This object is a superset of the [JSON Schema Specification Draft 2020-12](https://tools.ietf.org/html/draft-bhutton-json-schema-00).

For more information about the properties, see [JSON Schema Core](https://tools.ietf.org/html/draft-bhutton-json-schema-00) and [JSON Schema Validation](https://tools.ietf.org/html/draft-bhutton-json-schema-validation-00).

Unless stated otherwise, the property definitions follow those of JSON Schema and do not add any additional semantics. Where JSON Schema indicates that behavior is defined by the application (e.g. for annotations), OAS also defers the definition of semantics to the application consuming the OpenAPI document.

#### Properties

The OpenAPI Schema Object [dialect](https://tools.ietf.org/html/draft-bhutton-json-schema-00#section-4.3.3) is defined as requiring the [OAS base vocabulary](https://spec.openapis.org/oas/v3.1.0.html#baseVocabulary), in addition to the vocabularies as specified in the JSON Schema draft 2020-12 [general purpose meta-schema](https://tools.ietf.org/html/draft-bhutton-json-schema-00#section-8).

The OpenAPI Schema Object dialect for this version of the specification is identified by the URI `https://spec.openapis.org/oas/3.1/dialect/base` (the “OAS dialect schema id”).

The following properties are taken from the JSON Schema specification but their definitions have been extended by the OAS:

-   description - [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation.
-   format - See [Data Type Formats](https://spec.openapis.org/oas/v3.1.0.html#dataTypeFormat) for further details. While relying on JSON Schema’s defined formats, the OAS offers a few additional predefined formats.

In addition to the JSON Schema properties comprising the OAS dialect, the Schema Object supports keywords from any other vocabularies, or entirely arbitrary properties.

The OpenAPI Specification’s base vocabulary is comprised of the following keywords:

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| discriminator | [Discriminator Object](https://spec.openapis.org/oas/v3.1.0.html#discriminatorObject) | Adds support for polymorphism. The discriminator is an object name that is used to differentiate between other schemas which may satisfy the payload description. See [Composition and Inheritance](https://spec.openapis.org/oas/v3.1.0.html#schemaComposition) for more details. |
| xml | [XML Object](https://spec.openapis.org/oas/v3.1.0.html#xmlObject) | This _MAY_ be used only on properties schemas. It has no effect on root schemas. Adds additional metadata to describe the XML representation of this property. |
| externalDocs | [External Documentation Object](https://spec.openapis.org/oas/v3.1.0.html#externalDocumentationObject) | Additional external documentation for this schema. |
| example | Any | A free-form property to include an example of an instance for this schema. To represent examples that cannot be naturally represented in JSON or YAML, a string value can be used to contain the example with escaping where necessary.
**Deprecated:** The `example` property has been deprecated in favor of the JSON Schema `examples` keyword. Use of `example` is discouraged, and later versions of this specification may remove it.

 |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions), though as noted, additional properties _MAY_ omit the `x-` prefix within this object.

##### Composition and Inheritance (Polymorphism)

The OpenAPI Specification allows combining and extending model definitions using the `allOf` property of JSON Schema, in effect offering model composition. `allOf` takes an array of object definitions that are validated _independently_ but together compose a single object.

While composition offers model extensibility, it does not imply a hierarchy between the models. To support polymorphism, the OpenAPI Specification adds the `discriminator` field. When used, the `discriminator` will be the name of the property that decides which schema definition validates the structure of the model. As such, the `discriminator` field _MUST_ be a required field. There are two ways to define the value of a discriminator for an inheriting instance.

-   Use the schema name.
-   Override the schema name by overriding the property with a new value. If a new value exists, this takes precedence over the schema name. As such, inline schema definitions, which do not have a given id, _cannot_ be used in polymorphism.

##### XML Modeling

The [xml](https://spec.openapis.org/oas/v3.1.0.html#schemaXml) property allows extra definitions when translating the JSON definition to XML. The [XML Object](https://spec.openapis.org/oas/v3.1.0.html#xmlObject) contains additional information about the available options.

##### Specifying Schema Dialects

It is important for tooling to be able to determine which dialect or meta-schema any given resource wishes to be processed with: JSON Schema Core, JSON Schema Validation, OpenAPI Schema dialect, or some custom meta-schema.

The `$schema` keyword _MAY_ be present in any root Schema Object, and if present _MUST_ be used to determine which dialect should be used when processing the schema. This allows use of Schema Objects which comply with other drafts of JSON Schema than the default Draft 2020-12 support. Tooling _MUST_ support the [OAS dialect schema id](https://spec.openapis.org/oas/v3.1.0.html#dialectSchemaId), and _MAY_ support additional values of `$schema`.

To allow use of a different default `$schema` value for all Schema Objects contained within an OAS document, a `jsonSchemaDialect` value may be set within the [OpenAPI Object](https://spec.openapis.org/oas/v3.1.0.html#oasObject). If this default is not set, then the OAS dialect schema id _MUST_ be used for these Schema Objects. The value of `$schema` within a Schema Object always overrides any default.

When a Schema Object is referenced from an external resource which is not an OAS document (e.g. a bare JSON Schema resource), then the value of the `$schema` keyword for schemas within that resource _MUST_ follow [JSON Schema rules](https://tools.ietf.org/html/draft-bhutton-json-schema-00#section-8.1.1).

#### Schema Object Examples

##### Primitive Sample

```

{
  "type": "string",
  "format": "email"
}
```

```

type: string
format: email
```

##### Simple Model

```

{
  "type": "object",
  "required": [
    "name"
  ],
  "properties": {
    "name": {
      "type": "string"
    },
    "address": {
      "$ref": "#/components/schemas/Address"
    },
    "age": {
      "type": "integer",
      "format": "int32",
      "minimum": 0
    }
  }
}
```

```

type: object
required:
- name
properties:
  name:
    type: string
  address:
    $ref: '#/components/schemas/Address'
  age:
    type: integer
    format: int32
    minimum: 0
```

##### Model with Map/Dictionary Properties

For a simple string to string mapping:

```

{
  "type": "object",
  "additionalProperties": {
    "type": "string"
  }
}
```

```

type: object
additionalProperties:
  type: string
```

For a string to model mapping:

```

{
  "type": "object",
  "additionalProperties": {
    "$ref": "#/components/schemas/ComplexModel"
  }
}
```

```

type: object
additionalProperties:
  $ref: '#/components/schemas/ComplexModel'
```

##### Model with Example

```

{
  "type": "object",
  "properties": {
    "id": {
      "type": "integer",
      "format": "int64"
    },
    "name": {
      "type": "string"
    }
  },
  "required": [
    "name"
  ],
  "example": {
    "name": "Puma",
    "id": 1
  }
}
```

```

type: object
properties:
  id:
    type: integer
    format: int64
  name:
    type: string
required:
- name
example:
  name: Puma
  id: 1
```

##### Models with Composition

```

{
  "components": {
    "schemas": {
      "ErrorModel": {
        "type": "object",
        "required": [
          "message",
          "code"
        ],
        "properties": {
          "message": {
            "type": "string"
          },
          "code": {
            "type": "integer",
            "minimum": 100,
            "maximum": 600
          }
        }
      },
      "ExtendedErrorModel": {
        "allOf": [
          {
            "$ref": "#/components/schemas/ErrorModel"
          },
          {
            "type": "object",
            "required": [
              "rootCause"
            ],
            "properties": {
              "rootCause": {
                "type": "string"
              }
            }
          }
        ]
      }
    }
  }
}
```

```

components:
  schemas:
    ErrorModel:
      type: object
      required:
      - message
      - code
      properties:
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    ExtendedErrorModel:
      allOf:
      - $ref: '#/components/schemas/ErrorModel'
      - type: object
        required:
        - rootCause
        properties:
          rootCause:
            type: string
```

##### Models with Polymorphism Support

```

{
  "components": {
    "schemas": {
      "Pet": {
        "type": "object",
        "discriminator": {
          "propertyName": "petType"
        },
        "properties": {
          "name": {
            "type": "string"
          },
          "petType": {
            "type": "string"
          }
        },
        "required": [
          "name",
          "petType"
        ]
      },
      "Cat": {
        "description": "A representation of a cat. Note that `Cat` will be used as the discriminator value.",
        "allOf": [
          {
            "$ref": "#/components/schemas/Pet"
          },
          {
            "type": "object",
            "properties": {
              "huntingSkill": {
                "type": "string",
                "description": "The measured skill for hunting",
                "default": "lazy",
                "enum": [
                  "clueless",
                  "lazy",
                  "adventurous",
                  "aggressive"
                ]
              }
            },
            "required": [
              "huntingSkill"
            ]
          }
        ]
      },
      "Dog": {
        "description": "A representation of a dog. Note that `Dog` will be used as the discriminator value.",
        "allOf": [
          {
            "$ref": "#/components/schemas/Pet"
          },
          {
            "type": "object",
            "properties": {
              "packSize": {
                "type": "integer",
                "format": "int32",
                "description": "the size of the pack the dog is from",
                "default": 0,
                "minimum": 0
              }
            },
            "required": [
              "packSize"
            ]
          }
        ]
      }
    }
  }
}
```

```

components:
  schemas:
    Pet:
      type: object
      discriminator:
        propertyName: petType
      properties:
        name:
          type: string
        petType:
          type: string
      required:
      - name
      - petType
    Cat:  ## "Cat" will be used as the discriminator value
      description: A representation of a cat
      allOf:
      - $ref: '#/components/schemas/Pet'
      - type: object
        properties:
          huntingSkill:
            type: string
            description: The measured skill for hunting
            enum:
            - clueless
            - lazy
            - adventurous
            - aggressive
        required:
        - huntingSkill
    Dog:  ## "Dog" will be used as the discriminator value
      description: A representation of a dog
      allOf:
      - $ref: '#/components/schemas/Pet'
      - type: object
        properties:
          packSize:
            type: integer
            format: int32
            description: the size of the pack the dog is from
            default: 0
            minimum: 0
        required:
        - packSize
```

### Discriminator Object

When request bodies or response payloads may be one of a number of different schemas, a `discriminator` object can be used to aid in serialization, deserialization, and validation. The discriminator is a specific object in a schema which is used to inform the consumer of the document of an alternative schema based on the value associated with it.

When using the discriminator, _inline_ schemas will not be considered.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| propertyName | `string` | **_REQUIRED_**. The name of the property in the payload that will hold the discriminator value. |
| mapping | Map\[`string`, `string`\] | An object to hold mappings between payload values and schema names or references. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

The discriminator object is legal only when using one of the composite keywords `oneOf`, `anyOf`, `allOf`.

In OAS 3.0, a response payload _MAY_ be described to be exactly one of any number of types:

```

MyResponseType:
  oneOf:
  - $ref: '#/components/schemas/Cat'
  - $ref: '#/components/schemas/Dog'
  - $ref: '#/components/schemas/Lizard'
```

which means the payload __MUST__, by validation, match exactly one of the schemas described by `Cat`, `Dog`, or `Lizard`. In this case, a discriminator _MAY_ act as a “hint” to shortcut validation and selection of the matching schema which may be a costly operation, depending on the complexity of the schema. We can then describe exactly which field tells us which schema to use:

```

MyResponseType:
  oneOf:
  - $ref: '#/components/schemas/Cat'
  - $ref: '#/components/schemas/Dog'
  - $ref: '#/components/schemas/Lizard'
  discriminator:
    propertyName: petType
```

The expectation now is that a property with name `petType` __MUST__ be present in the response payload, and the value will correspond to the name of a schema defined in the OAS document. Thus the response payload:

```

{
  "id": 12345,
  "petType": "Cat"
}
```

Will indicate that the `Cat` schema be used in conjunction with this payload.

In scenarios where the value of the discriminator field does not match the schema name or implicit mapping is not possible, an optional `mapping` definition _MAY_ be used:

```

MyResponseType:
  oneOf:
  - $ref: '#/components/schemas/Cat'
  - $ref: '#/components/schemas/Dog'
  - $ref: '#/components/schemas/Lizard'
  - $ref: 'https://gigantic-server.com/schemas/Monster/schema.json'
  discriminator:
    propertyName: petType
    mapping:
      dog: '#/components/schemas/Dog'
      monster: 'https://gigantic-server.com/schemas/Monster/schema.json'
```

Here the discriminator _value_ of `dog` will map to the schema `#/components/schemas/Dog`, rather than the default (implicit) value of `Dog`. If the discriminator _value_ does not match an implicit or explicit mapping, no schema can be determined and validation _SHOULD_ fail. Mapping keys _MUST_ be string values, but tooling _MAY_ convert response values to strings for comparison.

When used in conjunction with the `anyOf` construct, the use of the discriminator can avoid ambiguity where multiple schemas may satisfy a single payload.

In both the `oneOf` and `anyOf` use cases, all possible schemas _MUST_ be listed explicitly. To avoid redundancy, the discriminator _MAY_ be added to a parent schema definition, and all schemas comprising the parent schema in an `allOf` construct may be used as an alternate schema.

For example:

```

components:
  schemas:
    Pet:
      type: object
      required:
      - petType
      properties:
        petType:
          type: string
      discriminator:
        propertyName: petType
        mapping:
          dog: Dog
    Cat:
      allOf:
      - $ref: '#/components/schemas/Pet'
      - type: object
        # all other properties specific to a `Cat`
        properties:
          name:
            type: string
    Dog:
      allOf:
      - $ref: '#/components/schemas/Pet'
      - type: object
        # all other properties specific to a `Dog`
        properties:
          bark:
            type: string
    Lizard:
      allOf:
      - $ref: '#/components/schemas/Pet'
      - type: object
        # all other properties specific to a `Lizard`
        properties:
          lovesRocks:
            type: boolean
```

a payload like this:

```

{
  "petType": "Cat",
  "name": "misty"
}
```

will indicate that the `Cat` schema be used. Likewise this schema:

```

{
  "petType": "dog",
  "bark": "soft"
}
```

will map to `Dog` because of the definition in the `mapping` element.

### XML Object

A metadata object that allows for more fine-tuned XML model definitions.

When using arrays, XML element names are _not_ inferred (for singular/plural forms) and the `name` property _SHOULD_ be used to add that information. See examples for expected behavior.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| name | `string` | Replaces the name of the element/attribute used for the described schema property. When defined within `items`, it will affect the name of the individual XML elements within the list. When defined alongside `type` being `array` (outside the `items`), it will affect the wrapping element and only if `wrapped` is `true`. If `wrapped` is `false`, it will be ignored. |
| namespace | `string` | The URI of the namespace definition. This _MUST_ be in the form of an absolute URI. |
| prefix | `string` | The prefix to be used for the [name](https://spec.openapis.org/oas/v3.1.0.html#xmlName). |
| attribute | `boolean` | Declares whether the property definition translates to an attribute instead of an element. Default value is `false`. |
| wrapped | `boolean` | _MAY_ be used only for an array definition. Signifies whether the array is wrapped (for example, `<books><book/><book/></books>`) or unwrapped (`<book/><book/>`). Default value is `false`. The definition takes effect only when defined alongside `type` being `array` (outside the `items`). |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### XML Object Examples

The examples of the XML object definitions are included inside a property definition of a [Schema Object](https://spec.openapis.org/oas/v3.1.0.html#schemaObject) with a sample of the XML representation of it.

##### No XML Element

Basic string property:

```

{
    "animals": {
        "type": "string"
    }
}
```

```

animals:
  type: string
```

```

<animals>...</animals>
```

Basic string array property ([`wrapped`](https://spec.openapis.org/oas/v3.1.0.html#xmlWrapped) is `false` by default):

```

{
    "animals": {
        "type": "array",
        "items": {
            "type": "string"
        }
    }
}
```

```

animals:
  type: array
  items:
    type: string
```

```

<animals>...</animals>
<animals>...</animals>
<animals>...</animals>
```

##### XML Name Replacement

```

{
  "animals": {
    "type": "string",
    "xml": {
      "name": "animal"
    }
  }
}
```

```

animals:
  type: string
  xml:
    name: animal
```

```

<animal>...</animal>
```

##### XML Attribute, Prefix and Namespace

In this example, a full model definition is shown.

```

{
  "Person": {
    "type": "object",
    "properties": {
      "id": {
        "type": "integer",
        "format": "int32",
        "xml": {
          "attribute": true
        }
      },
      "name": {
        "type": "string",
        "xml": {
          "namespace": "https://example.com/schema/sample",
          "prefix": "sample"
        }
      }
    }
  }
}
```

```

Person:
  type: object
  properties:
    id:
      type: integer
      format: int32
      xml:
        attribute: true
    name:
      type: string
      xml:
        namespace: https://example.com/schema/sample
        prefix: sample
```

```

<Person id="123">
    <sample:name xmlns:sample="https://example.com/schema/sample">example</sample:name>
</Person>
```

##### XML Arrays

Changing the element names:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string",
      "xml": {
        "name": "animal"
      }
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
    xml:
      name: animal
```

```

<animal>value</animal>
<animal>value</animal>
```

The external `name` property has no effect on the XML:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string",
      "xml": {
        "name": "animal"
      }
    },
    "xml": {
      "name": "aliens"
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
    xml:
      name: animal
  xml:
    name: aliens
```

```

<animal>value</animal>
<animal>value</animal>
```

Even when the array is wrapped, if a name is not explicitly defined, the same name will be used both internally and externally:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string"
    },
    "xml": {
      "wrapped": true
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
  xml:
    wrapped: true
```

```

<animals>
  <animals>value</animals>
  <animals>value</animals>
</animals>
```

To overcome the naming problem in the example above, the following definition can be used:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string",
      "xml": {
        "name": "animal"
      }
    },
    "xml": {
      "wrapped": true
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
    xml:
      name: animal
  xml:
    wrapped: true
```

```

<animals>
  <animal>value</animal>
  <animal>value</animal>
</animals>
```

Affecting both internal and external names:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string",
      "xml": {
        "name": "animal"
      }
    },
    "xml": {
      "name": "aliens",
      "wrapped": true
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
    xml:
      name: animal
  xml:
    name: aliens
    wrapped: true
```

```

<aliens>
  <animal>value</animal>
  <animal>value</animal>
</aliens>
```

If we change the external element but not the internal ones:

```

{
  "animals": {
    "type": "array",
    "items": {
      "type": "string"
    },
    "xml": {
      "name": "aliens",
      "wrapped": true
    }
  }
}
```

```

animals:
  type: array
  items:
    type: string
  xml:
    name: aliens
    wrapped: true
```

```

<aliens>
  <aliens>value</aliens>
  <aliens>value</aliens>
</aliens>
```

### Security Scheme Object

Defines a security scheme that can be used by the operations.

Supported schemes are HTTP authentication, an API key (either as a header, a cookie parameter or as a query parameter), mutual TLS (use of a client certificate), OAuth2’s common flows (implicit, password, client credentials and authorization code) as defined in \[[RFC6749](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC6749)\], and [OpenID Connect Discovery](https://tools.ietf.org/html/draft-ietf-oauth-discovery-06). Please note that as of 2020, the implicit flow is about to be deprecated by [OAuth 2.0 Security Best Current Practice](https://tools.ietf.org/html/draft-ietf-oauth-security-topics). Recommended for most use case is Authorization Code Grant flow with PKCE.

#### Fixed Fields

| Field Name | Type | Applies To | Description |
| --- | --- | --- | --- |
| type | `string` | Any | **_REQUIRED_**. The type of the security scheme. Valid values are `"apiKey"`, `"http"`, `"mutualTLS"`, `"oauth2"`, `"openIdConnect"`. |
| description | `string` | Any | A description for security scheme. [CommonMark syntax](https://spec.commonmark.org/) _MAY_ be used for rich text representation. |
| name | `string` | `apiKey` | **_REQUIRED_**. The name of the header, query or cookie parameter to be used. |
| in | `string` | `apiKey` | **_REQUIRED_**. The location of the API key. Valid values are `"query"`, `"header"` or `"cookie"`. |
| scheme | `string` | `http` | **_REQUIRED_**. The name of the HTTP Authorization scheme to be used in the Authorization header as defined in \[[RFC7235](https://spec.openapis.org/oas/v3.1.0.html#bib-RFC7235)\]. The values used _SHOULD_ be registered in the [IANA Authentication Scheme registry](https://www.iana.org/assignments/http-authschemes/http-authschemes.xhtml). |
| bearerFormat | `string` | `http` (`"bearer"`) | A hint to the client to identify how the bearer token is formatted. Bearer tokens are usually generated by an authorization server, so this information is primarily for documentation purposes. |
| flows | [OAuth Flows Object](https://spec.openapis.org/oas/v3.1.0.html#oauthFlowsObject) | `oauth2` | **_REQUIRED_**. An object containing configuration information for the flow types supported. |
| openIdConnectUrl | `string` | `openIdConnect` | **_REQUIRED_**. OpenId Connect URL to discover OAuth2 configuration values. This _MUST_ be in the form of a URL. The OpenID Connect standard requires the use of TLS. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### Security Scheme Object Example

##### Basic Authentication Sample

```

{
  "type": "http",
  "scheme": "basic"
}
```

```

type: http
scheme: basic
```

##### API Key Sample

```

{
  "type": "apiKey",
  "name": "api_key",
  "in": "header"
}
```

```

type: apiKey
name: api_key
in: header
```

##### JWT Bearer Sample

```

{
  "type": "http",
  "scheme": "bearer",
  "bearerFormat": "JWT",
}
```

```

type: http
scheme: bearer
bearerFormat: JWT
```

##### Implicit OAuth2 Sample

```

{
  "type": "oauth2",
  "flows": {
    "implicit": {
      "authorizationUrl": "https://example.com/api/oauth/dialog",
      "scopes": {
        "write:pets": "modify pets in your account",
        "read:pets": "read your pets"
      }
    }
  }
}
```

```

type: oauth2
flows: 
  implicit:
    authorizationUrl: https://example.com/api/oauth/dialog
    scopes:
      write:pets: modify pets in your account
      read:pets: read your pets
```

### OAuth Flows Object

Allows configuration of the supported OAuth Flows.

#### Fixed Fields

| Field Name | Type | Description |
| --- | --- | --- |
| implicit | [OAuth Flow Object](https://spec.openapis.org/oas/v3.1.0.html#oauthFlowObject) | Configuration for the OAuth Implicit flow |
| password | [OAuth Flow Object](https://spec.openapis.org/oas/v3.1.0.html#oauthFlowObject) | Configuration for the OAuth Resource Owner Password flow |
| clientCredentials | [OAuth Flow Object](https://spec.openapis.org/oas/v3.1.0.html#oauthFlowObject) | Configuration for the OAuth Client Credentials flow. Previously called `application` in OpenAPI 2.0. |
| authorizationCode | [OAuth Flow Object](https://spec.openapis.org/oas/v3.1.0.html#oauthFlowObject) | Configuration for the OAuth Authorization Code flow. Previously called `accessCode` in OpenAPI 2.0. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

### OAuth Flow Object

Configuration details for a supported OAuth Flow

#### Fixed Fields

| Field Name | Type | Applies To | Description |
| --- | --- | --- | --- |
| authorizationUrl | `string` | `oauth2` (`"implicit"`, `"authorizationCode"`) | **_REQUIRED_**. The authorization URL to be used for this flow. This _MUST_ be in the form of a URL. The OAuth2 standard requires the use of TLS. |
| tokenUrl | `string` | `oauth2` (`"password"`, `"clientCredentials"`, `"authorizationCode"`) | **_REQUIRED_**. The token URL to be used for this flow. This _MUST_ be in the form of a URL. The OAuth2 standard requires the use of TLS. |
| refreshUrl | `string` | `oauth2` | The URL to be used for obtaining refresh tokens. This _MUST_ be in the form of a URL. The OAuth2 standard requires the use of TLS. |
| scopes | Map\[`string`, `string`\] | `oauth2` | **_REQUIRED_**. The available scopes for the OAuth2 security scheme. A map between the scope name and a short description for it. The map _MAY_ be empty. |

This object _MAY_ be extended with [Specification Extensions](https://spec.openapis.org/oas/v3.1.0.html#specificationExtensions).

#### OAuth Flow Object Examples

```

{
  "type": "oauth2",
  "flows": {
    "implicit": {
      "authorizationUrl": "https://example.com/api/oauth/dialog",
      "scopes": {
        "write:pets": "modify pets in your account",
        "read:pets": "read your pets"
      }
    },
    "authorizationCode": {
      "authorizationUrl": "https://example.com/api/oauth/dialog",
      "tokenUrl": "https://example.com/api/oauth/token",
      "scopes": {
        "write:pets": "modify pets in your account",
        "read:pets": "read your pets"
      }
    }
  }
}
```

```

type: oauth2
flows: 
  implicit:
    authorizationUrl: https://example.com/api/oauth/dialog
    scopes:
      write:pets: modify pets in your account
      read:pets: read your pets
  authorizationCode:
    authorizationUrl: https://example.com/api/oauth/dialog
    tokenUrl: https://example.com/api/oauth/token
    scopes:
      write:pets: modify pets in your account
      read:pets: read your pets 
```

### Security Requirement Object

Lists the required security schemes to execute this operation. The name used for each property _MUST_ correspond to a security scheme declared in the [Security Schemes](https://spec.openapis.org/oas/v3.1.0.html#componentsSecuritySchemes) under the [Components Object](https://spec.openapis.org/oas/v3.1.0.html#componentsObject).

Security Requirement Objects that contain multiple schemes require that all schemes _MUST_ be satisfied for a request to be authorized. This enables support for scenarios where multiple query parameters or HTTP headers are required to convey security information.

When a list of Security Requirement Objects is defined on the [OpenAPI Object](https://spec.openapis.org/oas/v3.1.0.html#oasObject) or [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operationObject), only one of the Security Requirement Objects in the list needs to be satisfied to authorize the request.

#### Patterned Fields

| Field Pattern | Type | Description |
| --- | --- | --- |
| {name} | \[`string`\] | Each name _MUST_ correspond to a security scheme which is declared in the [Security Schemes](https://spec.openapis.org/oas/v3.1.0.html#componentsSecuritySchemes) under the [Components Object](https://spec.openapis.org/oas/v3.1.0.html#componentsObject). If the security scheme is of type `"oauth2"` or `"openIdConnect"`, then the value is a list of scope names required for the execution, and the list _MAY_ be empty if authorization does not require a specified scope. For other security scheme types, the array _MAY_ contain a list of role names which are required for the execution, but are not otherwise defined or exchanged in-band. |

#### Security Requirement Object Examples

##### Non-OAuth2 Security Requirement

```

{
  "api_key": []
}
```

```

api_key: []
```

##### OAuth2 Security Requirement

```

{
  "petstore_auth": [
    "write:pets",
    "read:pets"
  ]
}
```

```

petstore_auth:
- write:pets
- read:pets
```

##### Optional OAuth2 Security

Optional OAuth2 security as would be defined in an [OpenAPI Object](https://spec.openapis.org/oas/v3.1.0.html#openapi-object) or an [Operation Object](https://spec.openapis.org/oas/v3.1.0.html#operation-object):

```

{
  "security": [
    {},
    {
      "petstore_auth": [
        "write:pets",
        "read:pets"
      ]
    }
  ]
}
```

```

security:
  - {}
  - petstore_auth:
    - write:pets
    - read:pets
```
