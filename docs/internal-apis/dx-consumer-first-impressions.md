# First impressions

The first time a developer learns of a new internal API is often through a presentation, an internal slack message, referal from a colleague or at the request of a product owner. 
In general, developers are from the offset somewhat skeptical of consuming new internal APIs as it's a new dependency against another team with different priorities and from experience the maturity of internal API varies alot. 

## Gather information
The first step will be to gather information on the internal API. There are three major sources: 

1. API Portal (hopefully the company has one common one where OpenAPI contracts are published)
2. Enterprise search - Search engines covering internal material in the company such as presentations or work documents etc. Also includes searches on microblogging platforms such as slack and yammer. All this information may be outdated
3. Code search - Search for code repositories internally in the organisation (typically github)

As you can see from the above sources there are several challenges: 

1. API Portal usually leads the developer directly into the OpenAPI contracts without any additional context. Most internal APIs will have a barebone OpenAPI contract not describing the business context, but just listing individual endpoints
2. Enterprise search may lead you to outdated information or irrelevant information (for example it's not unusual that two APIs have almost the same name)
3. Code search have you start at the lowest possible level and it will be hard to understand the big picture on what the API supports

If the information is insufficient, the next step for the developer will be to identify if they know someone who works with the API or at least knows someone who does. If the company does not have a vibrant developer community or has organsiational silos, the developer may give up and report back to the product owner. In this case, the product owner needs to go through the line organisation and request the responsible team to setup a workshope with his team.

## Action: Strengthen the API portal
The key to improving the situation, is to strenghten the API portal beyond the OpenAPI contract. 
It needs to provide business context information for APIs in a consistent manner and the expectations on the level of quality of the information in the OpenAPI contract must be raised.

Grouping of APIs should be done over both business processes and source systems.

[Mercedes-benz developer experience](https://developer.mercedes-benz.com/products) can be an inspiration (even though it's not an internal API portal)
![image](https://user-images.githubusercontent.com/1133607/120652083-b61a4e00-c47f-11eb-9094-46fb35513a5b.png)

![image](https://user-images.githubusercontent.com/1133607/120652302-f11c8180-c47f-11eb-8cf3-b15605e7d65d.png)


"Leveraging API Docs and Tools at Mercedes-Benz developers" presentation is useful to better understand their concept.
<div align="center">
  <a href="https://www.youtube.com/watch?v=aTg7BCXZQMQ"><img src="https://img.youtube.com/vi/aTg7BCXZQMQ/0.jpg" alt="IMAGE ALT TEXT"></a>
</div>

## Technical details
The most mature API projects with the highest potential of reuse should be involved and help get an improved API portal in place. 

The content itself needs to be easily maintained by API producers (with possibility for API consumers to contribute). To facilitate this, using markdown and github respoitory as content store is a good choice. 

The developer experience of the API portal will evolve over time, and I believe the company should control it themselves on top of an open-source stack. 
I would prefer a static site generator (such as Jekyll or Mkdocs) publishing to Github pages. This architecture would need a customized build tool which queries the API portal software through APIs for all published OpenAPI contracts. Github actions is a good fit for this responsibility. This step will ensure APIs under development with no custom content in markdown are also represented in the overall API portal.
