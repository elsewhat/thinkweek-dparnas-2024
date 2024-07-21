# Operational excellency
![image](https://user-images.githubusercontent.com/1133607/120791606-b32d6500-c534-11eb-8d6e-7ca2caef5fb5.png)

The DevOps team should be given the mandate to automate as much of the operational tasks as possible. 

## Uptime monitoring for API consumers
In the API portal, have a common pattern for API uptime monitoring where the focus group is API consumers. For example, each API could have a health endpoint which performs an end-to-end call and has a standard payload. 

Have an uptime status page where all the health statuses are presented.
Overtime, this can be extended to provide alerts based on a publish/subscribe pattern. 

## Uptime monitoring for API producer
Do automated tests at least every hour through a background script and send alerts on failure to the DevOps team (for example through slack)
It should be a clear goal that the DevOps team should be aware of issues and working on resolving them, before it is reported by API consumers.


## Operational issues
Prepare a process for how to handle operational issues which require an emergency change. 
Include responsibilities and stepwise explanation on how to continously inform affected API consumers of the progress.

## Monitoring of users with missing authorization
A very common error in internal APIs, is that the end-user is missing some rights in the back-end system. 
Provide detailed error messages in these cases and work with API consumers on how to reduce the likelihood of such cases.

## Expiring keys and certificates
Have a calendar for expiring keys and certificates and make sure their are update well in advance of the expiry.
