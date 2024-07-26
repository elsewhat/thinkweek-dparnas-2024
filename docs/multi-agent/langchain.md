
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
(otherwise your will get error `[Errno 101] Network is unreachable`)

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