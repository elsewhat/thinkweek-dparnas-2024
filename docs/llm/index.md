

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
One of my formative experiences has been building our services constrained by what Apple will let us build on their platforms. Between the way they tax developers, the arbitrary rules they apply, and all the product innovations they block from shipping, it’s clear that Meta and many other companies would be freed up to build much better services for people if we could build the best versions of our products and competitors were not able to constrain what we could build. On a philosophical level, this is a major reason why I believe so strongly in building open ecosystems in AI and AR/VR for the next generation of computing.
```