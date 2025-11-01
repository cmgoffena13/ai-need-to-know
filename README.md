# AI Need to Know

A doc I created to help organize and simplify this "AI" Boom. The key part of "Artificial Intelligence" is the artificial part. It's not real.

LLMs are built from the work of Data Science/Machine Learning Engineering.

Building on LLMs does not require Machine Learning experience, but rather an understanding of fundamental concepts detailed below.

## Table of Contents

- [LLM](#llm)
  - [Introduction](#introduction)
  - [Popular LLMs](#popular-llms)
  - [Interacting with an LLM](#interacting-with-an-llm)
- [Beyond LLMs](#beyond-llms)
  - [RAG Modeling](#rag-modeling)
  - [Vector Databases](#vector-databases)
    - [Popular Vector Databases](#popular-vector-databases)
  - [AI Agents](#ai-agents)
    - [Popular Agents](#popular-agents)
    - [How an Agent is different from an LLM](#how-an-agent-is-different-from-an-llm)
    - [Context Injection](#context-injection)
  - [MCP Servers & MCP Clients](#mcp-servers--mcp-clients)
    - [Developing an MCP Server](#developing-an-mcp-server)
  - [Important Agent Modeling Concepts](#important-agent-modeling-concepts)
    - [Natural Language Understanding (NLU)](#natural-language-understanding-nlu)
    - [Context Engineering](#context-engineering)
    - [Prompt Engineering](#prompt-engineering)
    - [Task Orchestration](#task-orchestration)
- [Important LLM Understandings](#important-llm-understandings)
  - [LLMs Predict](#llms-predict)
  - [LLM Context Determines Agent Effectiveness](#llm-context-determines-agent-effectiveness)
  - [LLMs are Trained on Past Data](#llms-are-trained-on-past-data)
  - [LLMs are Fundamentally Stateless](#llms-are-fundamentally-stateless)
  - [LLMs Context has Limits](#llms-context-has-limits)
  - [LLMs Present Major Security/Privacy Concerns](#llms-present-major-securityprivacy-concerns)

# LLM

## Introduction

A Large Language Model is built using an incredibly large Neural Network. These models **predict** what to **say** based upon extremely large training datasets and statistical relationships between words and phrases. This means its **success** is determined by its ability to generate **high-quality, relevant, and coherent text** that **aligns** with human-like language patterns. Its process is fundamentally about **probability prediction**, not true understanding, intent, or even alignment with reality; What someone would **probably** say in response to your input.

Language is the fundamental building block of humanity. Without it, we likely would not even recognize another sentient being. Language does not accurately represent anything, it is simply a way for us to **agree** on a representation. Language is not true, it is just an agreement. Food for thought. Anyway.

## Popular LLMs
 - [ChatGPT](https://chat.openai.com)
    - Provider: OpenAI
 - [Gemini](https://ai.google/research/)
    - Provider: Google
 - [DeepSeek](https://deepseek.ai)
    - Provider: DeepSeek
 - [Llama](https://www.llama.com) (Open Source - not hosted on the internet)
    - Provider: Meta
 - [Claude](https://claude.ai)
    - Provider: Anthropic
 - [BLOOM](https://huggingface.co/bigscience/bloom) (Open Source - not hosted on the internet)
    - Provider: HuggingFace
 - [Grok](https://x.ai/grok)
    - Provider: xAI
 - [Lumo](https://proton.me/lumo)
    - Provider: Proton

## Interacting with an LLM

This is a really important section. There are **TWO** inputs to an LLM:
- Context
    - Additional information that can be **injected** to help inform the LLM of **what it knows**
- Prompt
    - The immediate question/command

The ability to provide further **context** to an LLM introduced  sophisticated ways of interacting with an LLM to help it perform better and to dynamically change its prediction.

# Beyond LLMs

## RAG Modeling

With the ability to **inject contextual information** with a prompt to an LLM, Retrieval-Augmented Generation (RAG) Modeling was created. This normally involves:
 - The storage of relevant contextual information utilizing a *Vector* database.
 - Middleware that **injects the contextual information** alongside a question/command

Basic workflow looks like this:  
 - User inputs a question/command
 - Middleware intercepts question/command
    - Parses the question/command and queries the *Vector* database to grab relevant contextual info surrounding question/command
 - Middleware **injects** relevant contextual info as **context** to the LLM in addition to the User's prompt
 - Middleware returns LLM's response

Rough Example:  
1. User inputs prompt in web page: 
`"Who do I talk to about getting reimbused for my travel meal?"`
2. Middleware takes prompt and searches *Vector* Database. Gets back info: `"Reimbursement Doc: Please contact John in Accounting for any reimburesement requests"`
3. Middleware **injects contextual information** alongside prompt to an LLM:  

Context:
```
Relevant Info:
"Reimbursement Doc: Please contact John in Accounting for any reimburesement requests"
```
Prompt:
```
"Who do I talk to about getting reimbused for my travel meal?"
```
4. LLM Outputs a better **prediction**  

Output:
```
You're absolutely right! It is incredibly important to get reimbursed for expenses made while on the job. 
You should contact John in Accounting for any reimbursement requests!
```

## Vector Databases

Vector Databases store and organize information in a similar way to LLMs, utilizing numerical representations (high-dimensional vectors) to represent **how likely information relates together**. When you query a *Vector* database, you provide information (such as text) and the database engine returns the closest vectors (the most relevant/relatable information). 

> **Note:** For those from the regular database world:  
> 1. A Vector is a record
> 2. A Vector contains a chunk of text that is relevant/related to your input query

### Popular Vector Databases

Vector databases have been around for a much longer period of time so a lot of options are available.

Stand-Alone

 - [Pinecone](https://www.pinecone.io)
 - [Milvus](https://milvus.io)
 - [Chroma](https://www.trychroma.com)

Platform/Product Specific
 - MongoDB Atlas Vector Search
 - Databricks Vector Database
 - ElasticSearch -  with vector enabled
 - Postgres -  `pgvector` extension

Cloud Specific
 - Azure: Azure Cognitive Search
 - AWS: Amazon Bedrock or Opensearch
 - GCP: Vertex AI Matching Engine

## AI Agents

With the great success of LLMs, providing a more accessible way of accessing agreed upon information (through their massive training datasets, sourced from the internet), introduced a new building block for software applications. LLMs' complex "reasoning" abilities could then be "directed" through **context injection**, similiar to someone trying to lead an elephant (if you think that sounds difficult, its because it is). This led to the development of **AI Agents**, which is a fancy way of saying software built on LLMs and utilizing LLMs. AI Agents are RAG Modeling on STEROIDS.

### Popular Agents

Because LLMs are language-based, utilizing LLMs within software systems has broad applications. Most Agents are very specific to enable better goal achievement, but we are seeing the rise of **general-purpose** Agents as well. To be clear, these **general-purpose** Agents are a combination of smaller agents to enable access to broader functionality.

General Purpose Agents
 - [ChatGTP Agent Mode](https://openai.com/index/introducing-chatgpt-agent/)
    - Combination of Agents that interact with your Operating System

Specific Agents
 - Search Agents
    - [Perplexity](https://www.perplexity.ai)
 - Code Agents
    - [Copilot](https://github.com/features/copilot)
    - [Cursor](https://cursor.com)
 - Customer Service Agents
 - Creative Agents

### How an Agent is different from an LLM

A limitation of LLMs is an inability to hold long-term "memory". LLMs have context within a conversation, but do not link conversations together and do not "learn" based upon interactions. A creation of an Agent normally involves **augmenting** an LLM by **injecting relevant contextual information** such as:
 - Previous Interactions and a success score
 - Additional information relevant to help it achieve a better success score

Behind the scenes of Agents is advanced context injection to help the LLM perform a specific task. Agents enable LLMs to be stateful and goal-driven through advanced context injection.

### Context Injection

The ability to inject contextual information into an LLM allows Agents to provide very specific information that an LLM "knows", rough conceptual example below:

Context:
```
You have access to a database, here are the tables: Table1, Table2, ... 
To see the results of a table, output this format

SELECT
*
FROM Table1
```
The LLM can then output **text** like this:
```
SELECT
*
FROM Table1
```
And then the output is **parsed** by the Agent, an actual query is ran on a database and then another prompt is issued to the LLM like this: 

Context:
```
You have access to a database, here are the tables: Table1, Table2, ... 
To see the results of a table, output this format

SELECT
*
FROM Table1

You queried Table1 in our last interaction, here are results:

blah blah blah
```

This gives the LLM relevant contextual information, and "empowers" it to interact with systems and make better predictions by **injecting** live data and very specific, relevant, contextual information.

>Note: [LangChain](https://github.com/langchain-ai/langchain) is an Open Source AI Agent Development Framework that is a popular choice in empowering the development for these context injection processes.

## MCP Servers & MCP Clients

Model Context Protocol (MCP) is a programmtic way to control *what* tools an LLM can use and *how* they can use them. 
 - A MCP Server is responsible for receiving commands from the MCP Client, executing those commands (i.e., invoking the tools), and sending the results back to the client.

 - A MCP Client is responsible for injecting the available tools and commands into the LLM’s context, interpreting when the LLM issues a command intended for the MCP Server, and sending the command to the server on the LLM’s behalf. It also injects the MCP Server’s results back into the LLM's input context for further processing.

>[LlamaIndex](https://github.com/run-llama/llama_index) is a popular open source library that helps developers easily create MCP Client code.

This design creates a feedback loop between real-world applications and the LLM, making it a fundamental component of AI agent development. It empowers the LLM to trigger commands that execute within software systems and receive results in real time! This continuous interaction gives the LLM relevant context to make better *predictions*.

> Note: It is important to recognize that an LLM has absolutely NO IDEA what triggering a command through an MCP server will do except what is provided to it. It makes a **prediction** of what someone would **probably** do given the language context. That is all.

### Developing an MCP Server

MCP Servers utilize the [JSON-RPC 2.0](https://www.jsonrpc.org/specification) specification as its core messaging protocol. From my perspective, this is what I'd use:

MCP Server
 - [fastapi-mcp](https://github.com/tadata-org/fastapi_mcp)  

MCP Client
 - [llamaindex](https://github.com/run-llama/llama_index)

## Important Agent Modeling Concepts

To simplify and summarize, an AI Agent:
1. Intakes a prompt
2. Parses the prompt for important contextual information
3. Utilizes the gathered information to:
   1. Gather long-term relevant contextual information by:
      1. Triggering commands on the MCP Server
      2. Querying a Vector Database
      3. etc.
4. Injects relevant long-term contextual information to the LLM alongside a new prompt to get a better *prediction*
5. Loops through until a solution is provided/confirmed by the system

### Natural Language Understanding (NLU)

It is important to correctly interpret a User's input to provide the best contextual information to the Agent. This requires implementation of Machine Learning to better understand the meaning of the input by identifying intents, entities, sentiment, and context. Good NLU enables the Agent to understand user goals and conditions accurately and empowers the entire process.

### Context Engineering

To empower the LLM to make better *predictions*, we need to provide accurate, structured, and simple contextual information to the LLM through a context **injection**. This can include a lot of information, but needs to be condensed down to respect the LLM's token limit.


### Prompt Engineering

 This involves properly breaking complex tasks down into sub tasks, setting guardrails, embedding external MCP Server tool invocation instructions, etc. This also involves re-structuring the **prompt** to enable the LLM to make a better *prediction*.

### Task Orchestration

Once we interpret a User's input, the Agent needs to orchestrate the movement and retrieval of contextual data to empower the LLM to complete its goal. There should also be data pipelines that are constantly updating the data sources that provide contextual information for the Agent to access and provide to the LLM.

# Important LLM Understandings

## LLMs Predict

LLMs predict the next token (word) to output based upon statistical relationships developed from language data. The success of their prediction is not based upon fundamental truth or alignment with reality. Because of this fact, LLMs can generate plausible but factually incorrect or fabricated information.

## LLM Context Determines Agent Effectiveness

An AI Agent is only as good as the context that is injected into the LLM with the prompt. MCP servers help, but only if accurate contextual information is provided in how to correctly utilize the MCP server, what actions have already been tried, etc. This also means if relevant information is not provided, destructive actions or inadequate solutions could easily occur. 

## LLMs are Trained on Past Data

Since LLMs are trained on past data, this also incorporates any bias and inaccuracies within the data (such as fundamental or toxic misunderstandings that are culturally widespread). LLMs also do not know current information unless specifically trained on the data (like the current date and context).

## LLMs are Fundamentally Stateless

LLMs do not have long-term memory. They are inherently stateless. Which means an LLM **cannot learn** without proper contextual feedback provided to it and that context must provided to it OVER and OVER again to maintain continuity. 

## LLMs Context has Limits

There are limits on the context that can be **injected** into an LLM. This directly immpacts the ability of an LLM to be effective in highly complex environments & situations. This is a key constraint in the current AI Engineering landscape.

## LLMs Present Major Security/Privacy Concerns

LLMs are trained on MASSIVE datasets sourced from the internet AND most LLMs record and store the prompts given to it. This prompt data *can* also be utilized to better train the LLM model, which could expose prompt data inadvertently. Since LLMs change their prediction based upon **context injection**, this exposes a way to maliciously expose sensitive information.