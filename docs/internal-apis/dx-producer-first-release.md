# First release
The first release of an internal API is always an important milestone.
In this process, it's easy to lose focus on the API consumer(s) in this process and what they need in order to create value for the business based on the API.

## API consumer focus
Do not finalize the release before the API consumer has the information they need.
Test your documentation by having someone in the team setup a API consumer using only the information they find in the documentation. 

## Release notes
Create release notes for the first release and focus on what functionality is available to business consumers.

Drive adoption by making these release notes available inside your company and not just for the intended API consumer. 
API portal could have a feed showing the latest release with corresponding release notes. 

## Monitoring
After going live, monitor the request/response log based on the activity of the API consumers. 
In many cases, you will discover they use the endpoint in a different manner than you expected or perhaps you will find edge cases where request have failed for example due to missing encoding of special characters in parameters. 

Over time, you'll want to automate this process. For example, you could have a batch job running in the morning reporting all failed requests into a slack channel monitored by the DevOps team.
