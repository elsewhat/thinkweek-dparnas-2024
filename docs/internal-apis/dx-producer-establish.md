# Establish internal API

Establishing a new API and performing a successful end-to-end call can be a daunting task the first time it's performed. 
Here are a few of the steps typically involved: 

- Create OpenAPI contract
- Upload OpenAPI contract to API portal
- Define policies in API portal
- Create API implementation as docker container
- Host API docker container
- Network architecture for communicating with back-end database/system from API docker container host
- Authentication
  - OAuth2 authentication setup - Create client app registration and add internal API dependency
  - OAuth2 authentication approval from admin
- Get a subscription/API key from the API portal

## Scaffolding
The establish phase is not executed very regularly executed by a single team and these kinds of process are typically not well documented end-to-end. 
However, multiple teams in your company will do the exact thing and typically will have to go through the same learning experience. 

To allieviate this: 

- Encourage the use of scaffolding tools such as Yeoman
- Document the end-to-end process (well suited for a video)
- Facilitate contact between teams of different API experience level

## Don't forget the API consumer
The definition of done for establishing an internal API is usually I can execute a request and get a response. 
But remember to cater for current and potential API consumers. Ensure the API producer take pride in their entry in the API portal and take the effort to describe the information an API consumer would be interested in.
