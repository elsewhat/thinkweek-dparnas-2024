## My code repository
[elsewhat/multi-agent-autogen-experiments](https://github.com/elsewhat/multi-agent-autogen-experiments)


## Thoughts
Autogen is an opinionated framework which has choosen chats as the main collaboration entity. 
When our use case is more focus on tasks to be solved, this can create unnecessary complexity.

Example of this can be found how nested chats towards a proxy are require in order to perform tool use.
```
player_white.register_nested_chats(
    trigger=player_black,
    chat_queue=[
        {
            "sender": board_proxy,
            "recipient": player_white,
            "summary_method": "last_msg",
        }
    ],
)
```

AutoGen was the first framework I experiemented with and ideally I should have had enough time to return to it validate my initial findings.

## Languages
Python is the primary language, but unlike the other frameworks there is also a [AutoGen for dotnet](https://microsoft.github.io/autogen-for-net/) which could ease enterprise adoption.

## Local models
Autogen supports [integration with non-OpenAI models](https://microsoft.github.io/autogen/docs/topics/non-openai-models/about-using-nonopenai-models), but it appears somewhat limited and not core functionality.

It'll require one of:

- Usage of a proxy server such as LiteLLM which supports OpenAIs API on top of Ollama
- Creating a [CustomModel class](https://microsoft.github.io/autogen/blog/2024/01/26/Custom-Models/)
- Use draft [pull request #3056 for Autogen Ollama]( https://github.com/microsoft/autogen/pull/3056)


Closed models from Anthropic is supported via [oai.anthropic package](https://microsoft.github.io/autogen/docs/reference/oai/anthropic/).

## Training

[Deeplearning.AI - AI agentic design patterns with AutoGen](https://www.deeplearning.ai/short-courses/ai-agentic-design-patterns-with-autogen/)


## Human in the loop
Human in the loop input is well designed. 

For example the below agent which is generating code to be executed locally, will always require a human in the loop to continue.

```
code_executor_agent = ConversableAgent(
    name="code_executor_agent",
    llm_config=False,
    code_execution_config={"executor": executor},
    human_input_mode="ALWAYS",
    default_auto_reply=
    "Please continue. If everything is done, reply 'TERMINATE'.",
)
```


## Tool use
Powerful [capabilities](https://microsoft.github.io/autogen/docs/tutorial/tool-use/) to execute local code and retrieve the output.

## Termination condition
```
joe = ConversableAgent(
    name="joe",
    system_message=
    "Your name is Joe and you are a stand-up comedian. "
    "When you're ready to end the conversation, say 'I gotta go'.",
    llm_config=llm_config,
    human_input_mode="NEVER",
    is_termination_msg=lambda msg: "I gotta go" in msg["content"] or "Goodbye" in msg["content"],
)
```

Feels unnatural to have this on the agent side instead of on the chat/task side.