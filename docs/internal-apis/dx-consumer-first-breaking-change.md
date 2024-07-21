# First breaking change

The general trend for REST APIs and versioning is to use [API evolution](https://apisyouwonthate.com/blog/api-evolution-for-rest-http-apis).


## Deprecation through releases
API consumers should be made aware of deprecation:

1. When deprecation is planned, the API producer team should analyse which API consumers are currently using the endpoints which will be affected by deprecation and inform contact persons
1. Through API release notes
1. Through their own monitoring of API requests returning a `Sunset` HTTP header


API producers are encourage to not remove deprecated features before all API consumers have moved to the now recommended alternative.