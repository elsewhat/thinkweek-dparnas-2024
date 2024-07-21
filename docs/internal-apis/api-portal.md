# API portal ideas

Start page with all internal APIs and filtering on the left hand side

![20210604_132744](https://user-images.githubusercontent.com/1133607/120797447-56ce4380-c53c-11eb-8234-aef337ec74d7.jpg)

Detail page of a single internal API

![20210604_134442](https://user-images.githubusercontent.com/1133607/120797574-82e9c480-c53c-11eb-85fb-9f4c9a173972.jpg)


## Automated generation of the API portal based on OpenAPI contract
Let's see how well we could automatically generate this based on the OpenAPI contract. 
[OpenAPI specification 3.1.0](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md) is available in Github and defines the fields available

### API card
```
API name = info.title
API elevator statement = info.summary
last update needs to come from API portal update timestamp
```

### API details
```
API name = info.title
API elevator statement = info.summary
API description = info.description <= Structured through markdown
API version = info.version
```

### API contact details
```
API contact = contact.name
API contact email = contact.email
Contact points = externalDocs.description + externalDocumentationObject.url (which can link to a slack channel)
```

### API resources overview
API resources comes from tags. Redoc has an [extension x-tagGroups](https://github.com/Redocly/redoc/blob/master/docs/redoc-vendor-extensions.md#x-taggroups) and similar patternt is been [investigated for OpenAPI specification](https://github.com/OAI/OpenAPI-Specification/issues/1367).

```
//If x-tagGroups exist perhaps only use the highest level?
API resource name = tag.name
API resource short description = tag.description
tag.externalDocs also exist and could point to url with more information
```

### Releases
Release notes must be maintained outside of OpenAPI specification.
Planned / ongoing releases likely also needs to be maintenance in a different manner. 

### Report issue
Report issue is likely maintained outside of OpenAPI specification (though in theory [specification extensions](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#specificationExtensions) are allowed).
Should lead the user into the service management portal of the company and in addition the contact points of the API
