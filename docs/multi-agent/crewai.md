## My code repository
[elsewhat/multi-agent-crewai-experiments](https://github.com/elsewhat/multi-agent-crewai-experiments)

## Thoughts
CrewAI+ product is a central part of there offering and in many ways it's not a traditional open-source project. 
Nothing wrong necessarily with this, but worth being aware of. 

## Local models
[Ollama support](https://docs.crewai.com/how-to/LLM-Connections/?h=ollama#ollama-integration) with local models is in place.

[Memory](https://docs.crewai.com/core-concepts/Memory/?h=memory#how-memory-systems-empower-agents) by default uses OpenAI Embeddings by default and requires an OpenAI API key. 

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
crewAI automatically collects telemetry and this is currently not possible to turn off. The main reason for this is likely commercial related to their paid version.

The telemetry is sent to `https://telemetry.crewai.com:4319`. [telemetry.py](https://github.com/crewAIInc/crewAI/blob/4da5cc97789177a493eeaff90e3e8908fb81b022/src/crewai/telemetry/telemetry.py#L22) is the class implementing the telemtry. 

A pull request to [enable telemtry opt-out](https://github.com/crewAIInc/crewAI/pull/402), but I don't believe it will ever be merged.