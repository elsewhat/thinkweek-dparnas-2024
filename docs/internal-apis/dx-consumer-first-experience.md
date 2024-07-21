# First experience
We define the first experience as the steps required in order to perform the first call of the internal API. 

## Minimize setup required
In general, we want to minimize the steps required for setting up. 
For an internal API the following steps might be required: 

1. Get a subscription/API key from the API Portal
2. OAuth2 authentication setup - Create client app registration and add internal API dependency
3. OAuth2 authentication approval from admin
4. Apply for authorization roles in back-end system
5. Apply for authorization roles in API
6. Execute the first request in your prefered tool such as postman or curl

If possible, simplify this setup.

The full process, start to finish, should be described in the API portal (regardless of the fact that the API DevOps team is not responsible for authorization roles in the backend system or OAuth2 authentication setup approval. 

Note that this process for internal APIs will in many cases be identical for several APIs so the content describing it can be shared.

## Getting started
Getting started guide is essential to streamline the process of onboarding new API consumers.

Make sure you keep it focused and to the point, the getting started guide is not an owners manual. 

An analogy to this is if you buy a new car. The car salesperson will use a few minutes with you to explain the core features of the car.
The salesperson does not however hand you the owner's manual and tell you to study it before you drive out from the dealership.
![image](https://user-images.githubusercontent.com/1133607/120671103-59c02a00-c491-11eb-92e2-69c75d7513bc.png)
