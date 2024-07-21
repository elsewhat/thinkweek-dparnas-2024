# First use case
Once the first success is achieved, the developer likely wants to chain several API requests in order to achieve a business outcome. In many cases, the developer is not a domain expert and has only gotten vague input from product owner on what the goal is. 

## Provide business context
The API portal description should provide business context. For example, describe the difference between a corrective-work-order and preventive-work-order resource.

This may be challenging for the API producer DevOps team to create, so ensure the product owner dimension is involved. 

## Low bar for reaching out
Provide a slack channel for your API, where developers can ask informal questions for example how they best can achieve their wanted business outcomes. Do not force them to register a support ticket or similar as developers will postpone this untill they have exhausted all other options. 

Have the slack channel become the home of a community of API consumers and the API producer DevOps team. More often than not, you will see API consumers helping each other out. 

## Provide tools for grouping API request
Encourage the use of tools like postman, where developers can setup a collection of API request they need to achieve their wanted business outcome. 

The API producer DevOps team should be responsible for maintaining a reference postman collection of typically API request grouped in a natural manner (as a golden rule, one request pr example of an endpoint in the OpenAPI contract).