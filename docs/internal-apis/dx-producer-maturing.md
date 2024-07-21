# Maturing features
In order to fullfil a business outcome, there is likely a set of endpoints and resource models in the OpenAPI contract to be defined.

To do this it's essential to understand:  

- The flow in the first API consumer application
- How the resources are represented in the data model of the back-end
- Business process context the API consumer application and the back-end relate to

## Involve API consumer
Involve the API consumer in the maturing. Understand how the API endpoints will be used and what kind of data the front-end has available at that point of time. 

Create a branch of the OpenAPI contract for maturing the feature. 
As early as possible, use a mock server or a dev instance of the API portal to have the new planned endpoints return mock data for testing by the API consumer.
Generate documentation for the new planned endpoints of OpenAPI contract as this is more understandable than the raw OpenAPI file for many API consumers. 

In most cases, the internal funding for the implementation comes from the API consumer side.

## Who to involve in the maturing?
This is an area where there are many different elements which must be balanced. 

Usually there is 1-2 persons in a DevOps team which are the drivers for the structures and principles of the OpenAPI contract. 
The DevOps team is typically mid-sprint when the maturing is natural to perform, and their minds are focused on the deliverables of the current sprint and not on potential future needs. The product owner from the business typically has broad base of domain knowledge and has access to specialist for concrete cases. However, they are typically not the drivers for the details in the OpenAPI specification. 

In my experience, meetings with 3+ participants where the goal is create an OpenAPI contract definition from scratch for a new feature rarely are efficient.
It's better to have a draft be created in advanced and then this can be presented and adjusted after discussions. However, this approach makes the process dependant on individual persons and if they are away it may stop maturing process. To mitigate this, it's important to involve the whole DevOps team in the code review of the OpenAPI specification and ensure they know the necessary tooling for updating it.

## Domain knowledge
Seek out business process description and governing documents for the area. 
Use precise terminolgy and prefer naming taken from international standard where appropriate


## OpenAPI contract source when code is implemented
TBD
