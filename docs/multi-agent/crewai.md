
## Local models
[Ollama support](https://docs.crewai.com/how-to/LLM-Connections/?h=ollama#ollama-integration) with local models is in place.

[Memory](https://docs.crewai.com/core-concepts/Memory/?h=memory#how-memory-systems-empower-agents) by default uses OpenAI Embeddings by default and requires an OpenAI API key, but you can change it by setting embedder to a different model.

## Tools
Tools can be assigned to an agent or to a task.

CrewAI has it's own set of tools, but also supports all [LangChain tools](https://python.langchain.com/v0.2/docs/integrations/tools/).

Predefined tools as of 2024.07.23:

| Tool                        | Description                                                                                   |
| :-------------------------- | :-------------------------------------------------------------------------------------------- |
| **BrowserbaseLoadTool**     | A tool for interacting with and extracting data from web browsers.                            |
| **CodeDocsSearchTool**      | A RAG tool optimized for searching through code documentation and related technical documents. |
| **CodeInterpreterTool**     | A tool for interpreting python code.                                                          |
| **ComposioTool**            | Enables use of Composio tools.                                                                |
| **CSVSearchTool**           | A RAG tool designed for searching within CSV files, tailored to handle structured data.       |
| **DirectorySearchTool**     | A RAG tool for searching within directories, useful for navigating through file systems.      |
| **DOCXSearchTool**          | A RAG tool aimed at searching within DOCX documents, ideal for processing Word files.         |
| **DirectoryReadTool**       | Facilitates reading and processing of directory structures and their contents.                |
| **EXASearchTool**           | A tool designed for performing exhaustive searches across various data sources.               |
| **FileReadTool**            | Enables reading and extracting data from files, supporting various file formats.              |
| **FirecrawlSearchTool**     | A tool to search webpages using Firecrawl and return the results.                             |
| **FirecrawlCrawlWebsiteTool** | A tool for crawling webpages using Firecrawl.                                               |
| **FirecrawlScrapeWebsiteTool** | A tool for scraping webpages url using Firecrawl and returning its contents.               |
| **GithubSearchTool**        | A RAG tool for searching within GitHub repositories, useful for code and documentation search.|
| **SerperDevTool**           | A specialized tool for development purposes, with specific functionalities under development. |
| **TXTSearchTool**           | A RAG tool focused on searching within text (.txt) files, suitable for unstructured data.     |
| **JSONSearchTool**          | A RAG tool designed for searching within JSON files, catering to structured data handling.     |
| **LlamaIndexTool**          | Enables the use of LlamaIndex tools.                                                          |
| **MDXSearchTool**           | A RAG tool tailored for searching within Markdown (MDX) files, useful for documentation.      |
| **PDFSearchTool**           | A RAG tool aimed at searching within PDF documents, ideal for processing scanned documents.    |
| **PGSearchTool**            | A RAG tool optimized for searching within PostgreSQL databases, suitable for database queries. |
| **RagTool**                 | A general-purpose RAG tool capable of handling various data sources and types.                 |
| **ScrapeElementFromWebsiteTool** | Enables scraping specific elements from websites, useful for targeted data extraction.     |
| **ScrapeWebsiteTool**       | Facilitates scraping entire websites, ideal for comprehensive data collection.                 |
| **WebsiteSearchTool**       | A RAG tool for searching website content, optimized for web data extraction.                   |
| **XMLSearchTool**           | A RAG tool designed for searching within XML files, suitable for structured data formats.      |
| **YoutubeChannelSearchTool**| A RAG tool for searching within YouTube channels, useful for video content analysis.           |
| **YoutubeVideoSearchTool**  | A RAG tool aimed at searching within YouTube videos, ideal for video data extraction.          |

## Telemtry
https://telemetry.crewai.com:4319
https://github.com/crewAIInc/crewAI/blob/4da5cc97789177a493eeaff90e3e8908fb81b022/src/crewai/telemetry/telemetry.py#L22

os.environ["OTEL_SDK_DISABLED"] = "true"

etc/hosts
127.0.0.1	telemetry.crewai.com

https://github.com/crewAIInc/crewAI/pull/402

## Install dependencies
Crewai has a very large list of indirect dependencies.
(assume many of them come through langchain_community)
```
Installing collected packages: sortedcontainers, schema, ratelimiter, pytz, pypika, mpmath, monotonic, mmh3, flatbuffers, docx2txt, appdirs, zipp, wrapt, websockets, websocket-client, uvloop, urllib3, tzdata, typing-extensions, tqdm
, tenacity, tabulate, sympy, soupsieve, sniffio, six, shellingham, semver, regex, PyYAML, pytube, python-multipart, python-dotenv, pysocks, pysbd, pyproject_hooks, pypdf, pygments, pyasn1, py, protobuf, portalocker, pluggy, pillow,
parameterized, packaging, overrides, orjson, opentelemetry-util-http, oauthlib, numpy, nodeenv, mypy-extensions, multidict, mdurl, MarkupSafe, jsonref, jsonpointer, json-repair, jmespath, jiter, iniconfig, importlib-resources, idna,
 hyperframe, humanfriendly, httpx-sse, httptools, hpack, h11, grpcio, greenlet, google-crc32c, fsspec, frozenlist, filelock, fastavro, eval-type-backport, docstring-parser, dnspython, distro, decorator, click, charset-normalizer, ce
rtifi, cachetools, bcrypt, backoff, attrs, asgiref, annotated-types, yarl, wsproto, uvicorn, typing-inspect, types-requests, SQLAlchemy, shapely, rsa, retry, requests, python-dateutil, pytest, pyright, pydantic-core, pyasn1-modules,
 pyarrow, pulsar-client, proto-plus, outcome, opentelemetry-proto, marshmallow, markdown-it-py, Mako, jsonpatch, jinja2, importlib-metadata, httpcore, h2, grpcio-tools, googleapis-common-protos, google-resumable-media, email_validat
or, deprecation, deprecated, coloredlogs, chroma-hnswlib, build, beautifulsoup4, anyio, aiosignal, watchfiles, trio, tiktoken, starlette, rich, requests-oauthlib, pylance, pydantic, posthog, pandas, opentelemetry-exporter-otlp-proto
-common, opentelemetry-api, onnxruntime, huggingface-hub, httpx, grpcio-status, gptcache, google-auth, docker, dataclasses-json, botocore, alembic, aiohttp, typer, trio-websocket, tokenizers, s3transfer, opentelemetry-semantic-conve
ntions, opentelemetry-instrumentation, openai, langsmith, lancedb, kubernetes, grpc-google-iam-v1, groq, google-api-core, together, selenium, qdrant-client, opentelemetry-sdk, opentelemetry-instrumentation-asgi, langchain-core, inst
ructor, google-cloud-core, fastapi-cli, boto3, opentelemetry-instrumentation-fastapi, opentelemetry-exporter-otlp-proto-http, opentelemetry-exporter-otlp-proto-grpc, mem0ai, langchain-text-splitters, langchain-openai, google-cloud-s
torage, google-cloud-resource-manager, google-cloud-bigquery, fastapi, cohere, langchain, google-cloud-aiplatform, chromadb, langchain_community, langchain-experimental, langchain-cohere, embedchain, crewai_tools, crewai
```

## Thoughts
CrewAI+ product is a central part of there offering and in many ways it's not a traditional open-source project. 
Nothing wrong necessarily with this, but worth being aware of. 