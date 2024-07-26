## My code repository
[elsewhat/multi-agent-langgraph-experiments](https://github.com/elsewhat/multi-agent-langgraph-experiments)


# Thoughts
LangChain was an early framework in this space and therefore is experienced as more mature than the others.
It has a relatively high barrier for entry, but the deeplearning.ai courses [Functions, Tools and Agents with LangChain](https://www.deeplearning.ai/short-courses/functions-tools-agents-langchain/) and [AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) mitigate this. 

There has been some restructuring lately, for example moving components to langchain_community and langchain-experimental.


The use cases I am most interested are categorized by: 

- Combination of open and closed LLMs (fit for purpose and cost)
- Well-defined workflows setup as cyclic graphs with intermediate output in both structured and unstructered form
- Require tools to verify the validity and quality of the output (such as [spectral-cli](https://github.com/stoplightio/spectral) ) included in the cyclic graphs
- Agentic patterns emerging from research such as [ReAct - Synergizing reasoning and acting in language models](https://arxiv.org/abs/2210.03629), [Self-Refine: Iterative refinement with self-feedback ](https://arxiv.org/abs/2303.17651) and [Code Generation with AlphaCodium: From Prompt Engineering to Flow Engineering](https://arxiv.org/abs/2401.08500)

In my opinion, [LangChain](multi-agent/langchain.md) with it's [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain Expression Language (LCEL)](https://python.langchain.com/v0.1/docs/expression_language/) have strong support for this. Open source ethos appears to be relatively strong in their deliveries, but they do have some enterprise products which may distract. 

As a consequence instead of using [LangSmith](https://www.langchain.com/langsmith) for tracing, it might be better to use more open solutions such as [LangFuse](https://github.com/langfuse/langfuse).

## LangGraph
"Langraph is a library for building stateful, multi-actor applications with LLMs, used to create agent and multi-agent workflows. Compared to other LLM frameworks, it offers these core benefits: cycles, controllability, and persistence. LangGraph allows you to define flows that involve cycles, essential for most agentic architectures, differentiating it from DAG-based solutions. As a very low-level framework, it provides fine-grained control over both the flow and state of your application, crucial for creating reliable agents. Additionally, LangGraph includes built-in persistence, enabling advanced human-in-the-loop and memory features."

Example of an graph generated via `graph.get_graph().draw_png('graph.png')` (using graphviz)

![alt text](img/graph_ora_tables.png)

In my opinion, this is very relevant abstraction for many use cases and can easily support agentic patterns emerging from research.

## LangChain Expression Language (LCEL)
"LangChain Expression Language, or LCEL, is a declarative way to easily compose chains together. 
[..]
chain = prompt | model | output_parser

The | symbol is similar to a unix pipe operator, which chains together the different components, feeding the output from one component as input into the next component.

In this chain the user input is passed to the prompt template, then the prompt template output is passed to the model, then the model output is passed to the output parser."

In my opinion, this is a good abstraction.

## Ollama setup
In .env add
```
OLLAMA_HOST="host.docker.internal"
```

Make sure environment variable is loaded before you import ChatOllama
```
from dotenv import load_dotenv
load_dotenv()
from langchain_ollama import ChatOllama
```

On desktop where Ollama is running, add environment varible `OLLAMA_ORIGINS` with value `http://host.docker.internal:11434`
(otherwise your will get error `[Errno 101] Network is unreachable` which is triggered from Ollama)

### Alternative setup #1
Use the OpenAI model with a custom path

```
from langchain_openai import ChatOpenAI
model = ChatOpenAI(
    api_key="ollama",
    #model="llama3.1:8b-instruct-q8_0",
    model="mistral-nemo-32kb:12b-instruct-2407-q8_0",
    base_url="http://host.docker.internal:11434/v1",
)
```
### Alternative setup #2
If using for classification/function calling, test out OllamaFunctions
```
from langchain_experimental.llms.ollama_functions import OllamaFunctions
model = OllamaFunctions(
    api_key="ollama",
    model="llama3.1:8b-instruct-q8_0",
    base_url="http://host.docker.internal:11434",
)
```

PS: This does not appear to me to use the expect tool/function calling capabilities in Ollama.