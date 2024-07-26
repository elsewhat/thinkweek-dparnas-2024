
## Running local LLM models
I already have experience with running local LLM through [Ollama](https://ollama.com/). 

The PC used for the ThinkWeek has a Nvidia 4090 GPU with 24GB which comfortably runs open LLM model in the size range up to 25B parameters.

Ollama is running on windows and exposes its API interface through port 11434. I set environment variable `OLLAMA_DEBUG=1` to increase Ollama logging.

The actual code used for experimenting is running through docker [devcontainers](https://containers.dev/). This allowed me to easily control dependencies directly from VS Code. 
This is an overview of the code experiements performed using local models: 

- AutoGen [elsewhat/multi-agent-autogen-experiments](https://github.com/elsewhat/multi-agent-autogen-experiments)
- CrewAI [elsewhat/multi-agent-crewai-experiments](https://github.com/elsewhat/multi-agent-crewai-experiments)
- LangChain [elsewhat/multi-agent-langgraph-experiments](https://github.com/elsewhat/multi-agent-langgraph-experiments)

To connect to Ollama from a docker container, it's important to use [host.docker.internal](https://docs.docker.com/desktop/networking/#i-want-to-connect-from-a-container-to-a-service-on-the-host) instead of localhost or 127.0.0.1. For LangChain when using ChatOllama class, I also had to add environment variable for Ollama called `OLLAMA_ORIGINS=http://host.docker.internal:11434` for it not to get a `[Errno 101] Network is unreachable)`.

I used [Edgeshark](https://edgeshark.siemens.io/) in order to do network tracing.

## Context window
Learned that the context window for Ollama is usually 2K/8K regardless of what the actual model supported. 

Created a [Ollama Modelfile](https://github.com/ollama/ollama/blob/main/docs/modelfile.md) for llama3.1 for 128K context window.
```
FROM llama3.1:8b-instruct-q8_0
PARAMETER num_ctx 131072
```

The memory usage of the model in Ollama increased with ~16GB. Turns out the size of the KV part of the model inference grows at O(n^2).

## Ollama model variants 
Ollama provides some standard conversion of the Huggingface models before making them available. 

The default model is with Q4 quantization, which is generally weaker than the original one from the model provider.  
The Q8 model should be preferred if it's fits in GPU memory. 

Some models have K_M and K_S postfixes, such as `llama3.1:8b-instruct-q5_K_M`. The K_M will [normally be preferred](https://github.com/ggerganov/llama.cpp/pull/1684#issuecomment-1579252501).

## Open vs closed models
[Open Source AI Is the Path Forward](https://about.fb.com/news/2024/07/open-source-ai-is-the-path-forward/) is the title of Mark Zuckerbergs letter attached to the [Llama 3.1 release](https://ai.meta.com/blog/meta-llama-3-1/). He expands on this in [this interview](https://x.com/rowancheung/status/1815763595197616155) with Rowan Cheung.

In this, he's very transparent on Meta's strategy around AI and what they believe is the way forward.

He fires some shots towards vendor controlled ecosystem and it's clear they want to avoid this for AI.
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

## Open models
I did not focus on comparing and evaluating different local LLM models and their licenses. 

From before, I had gathered a list of some relevant models and their license: 

- [Phi3 from Microsoft](https://huggingface.co/collections/microsoft/phi-3-6626e15e9585a200d2d761e3) - [MIT license](https://huggingface.co/microsoft/Phi-3-mini-128k-instruct#license)
- [Granite from IBM](https://huggingface.co/ibm-granite) - [Apache 2.0 license](https://github.com/ibm-granite/granite-code-models/tree/main)
- [Gemma from Google](https://huggingface.co/google/gemma-7b) - [Apache 2.0 license](https://github.com/google-deepmind/gemma/blob/main/LICENSE) with [Gemma Terms of Use](https://ai.google.dev/gemma/terms) (includes prohibited use clausul)
- [Mixtral from Mistral](https://huggingface.co/mistralai) - [Apache 2.0 license](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2) (I used its successor Mistral Nemo mistral-nemo-32kb:12b-instruct-2407-q8_0 quite a bit)
- [Llama3 from Meta](https://github.com/meta-llama/llama3/blob/main/MODEL_CARD.md) - [Meta llama3 community license](https://llama.meta.com/llama3/license/)
- [NorLLM from NorwAI ](https://www.universitetsavisa.no/406796)- Apache 2.0, but must also follow the underlying base model
