# Introduction
After a successful [ThinkWeek in 2021](https://elsewhat.com/thinkweek-dparnas-2024/), I decided to do it again. 

This year's focus has been AI and how it will impact my work as an architect spanning technical, solution and enterprise architecture. 

Key areas: 

- State of open models
- Hands-on experience with AI frameworks for agentic and multi-agent execution
    - [AutoGen](multi-agent/autogen.md)
    - [crewAI](multi-agent/crewai.md)
    - [LangChain](multi-agent/langchain.md)
- Modernizing enterprise solutions with LLMs

# Key findings

## Pace of innovation

The pace of innovation is extremely high as a consequence of technical breakthroughs and massive investments. To examplify this, the following happened in AI during my ThinkWeek:

- [Meta released LLama 3.1 405B](https://ai.meta.com/blog/meta-llama-3-1/) - The first large open model competing with the closed ones and with a clear open-source strategy from Meta to back it
- [Meta release updated version of smaller models llama3.1 8B and 70B](https://llama.meta.com/) - Context window increased to 128KB and now supporting "tool/function" calling
- [Ollama 0.30 relased](https://ollama.com/blog/tool-support) - Now with official "tool/function" calling
- [Mistral release their flagship model Mistral Large 2](https://mistral.ai/news/mistral-large-2407/) - An open 128B model, following up their release of Mistral NeMo 12B last week
- [OpenAI releases SearchGPT ](https://openai.com/index/searchgpt-prototype/) - Having the potential to transform the way we do search. Accessible through [waitlist system](https://chatgpt.com/search)

## Closed vs Open AI
AI's future form of deployment is a constant tug of war between the large tech companies.
My personal impression is that there are enough forces pushing towards open models and there are enough resources and motivation for it. 

[Open Source AI Is the Path Forward](https://about.fb.com/news/2024/07/open-source-ai-is-the-path-forward/) is the title of Mark Zuckerbergs letter attached to the Llama 3.1 405B release. In this letter, he's very transparent on Meta's strategy around AI and what they believe is the way forward. He "fires some shots" towards vendor controlled ecosystems and it's clear Meta want to avoid this for AI.
```
One of my formative experiences has been building our services constrained 
by what Apple will let us build on their platforms. 
Between the way they tax developers, the arbitrary rules they apply,
 and all the product innovations they block from shipping,
it’s clear that Meta and many other companies would be 
freed up to build much better services for people if we could build 
the best versions of our products and competitors were not 
able to constrain what we could build. On a philosophical level, 
this is a major reason why I believe so strongly in 
uilding open ecosystems in AI and AR/VR for the next generation of computing.
```

My main concern around AI is that research and government insititutions do not have enough resources to be relevant and that the top talents are recruited by private section. 

Whilst not a focus during the ThinkWeek, the geopolitical implactions of AI have started to emerge especially the last year. 
[Situational Awareness ](https://situational-awareness.ai/) from Leopold Aschenbrenner is a must read to understand where we might be heading. 

## AI frameworks for agentic and multi-agent execution
There is a convincing argument to be made that agentic workflows do not need to use a framework. 


- Matt Williams makes this argument in his video [Have You Picked the Wrong AI Agent Framework?](https://youtu.be/jLVl5V8roMU?si=jIrHkeQ4c9EkVTeV)
- Dave Ebbekaar makes the same argument in [Why Agent Frameworks Will Fail (and what to use instead)](https://www.youtube.com/watch?v=KY8n96Erp5Q)

One of their key argument is that you in most cases already know the well-defined workflow to be followed and simplicity is much easier to maintain without a AI agent framework in these cases.

There is plenty of truths to this, but not all of the arguments can be translated directly to an enterprise software setting. 
Here there right frameworks provide additional benefits for how the code is maintained and extended over its lifetime.

## Modernizing enterprise sofware with LLMs
The background for this thought experiment is the renwal of large enterprise solutions with outdated technology and plenty of technical debt. 
Typically, such solutions will take years to modernize with a traditional approach and have high complexity and risk. 

Based on my experiences in the ThinkWeek, I believe it's possible to use LLMs in this modernization process. 
It will require: 

- Combination of open and closed LLMs (fit for purpose and cost)
- Well-defined workflows setup as cyclic graphs with intermediate output in both structured and unstructered form
- Tools to verify the validity and quality of the output (such as [spectral-cli](https://github.com/stoplightio/spectral) ) included in the cyclic graphs
- Agentic patterns emerging from research such as [ReAct - Synergizing reasoning and acting in language models](https://arxiv.org/abs/2210.03629), [Self-Refine: Iterative refinement with self-feedback ](https://arxiv.org/abs/2303.17651) and [Code Generation with AlphaCodium: From Prompt Engineering to Flow Engineering](https://arxiv.org/abs/2401.08500)


Based on the tested framework, [LangChain](multi-agent/langchain.md) with it's [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain Expression Language (LCEL)](https://python.langchain.com/v0.1/docs/expression_language/) appears to be the strongest. Open source ethos appears to be relatively strong in their deliveries, but they do have some enterprise products which may distract. 
As a consequence instead of using [LangSmith](https://www.langchain.com/langsmith), it might be better to use more open solutions such as [LangFuse](https://github.com/langfuse/langfuse).

# What is ThinkWeek
The following figure from [Reservations.com](https://www.reservations.com/blog/resources/think-weeks/) sums up the practical aspects of a Think Week.
![](https://www.reservations.com/blog/wp-content/uploads/2019/06/think-week-03-1.jpg)
