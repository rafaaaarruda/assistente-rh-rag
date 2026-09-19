[🇧🇷 Português](README.md) | 🇺🇸 English

# 🤖 RAG-Based HR Assistant

Virtual Human Resources assistant developed during the **Oracle + Alura AI Agents Immersion**, using a low-code approach to integrate Generative AI, RAG, databases, and workflow automation.

The project simulates an internal HR assistant capable of answering questions about a fictional company and retrieving specific employee information through Telegram.

> This repository works as a case study of the project. The original environment used during development is no longer available and, as a result, the original workflows could no longer be recovered.

---

## 📌 About the project

The goal of the project was to build an AI agent capable of handling different types of Human Resources-related requests.

Through a Telegram conversation, the user could ask questions about general company information, such as:

- work models;
- vacation policy;
- internal rules and corporate information.

In addition, the agent could also query structured employee data stored in a MySQL database.

This allowed the solution to combine information retrieved through **RAG (Retrieval-Augmented Generation)** with structured database queries.

---

## ⚙️ How the solution works

The main flow was built in **n8n**, which was responsible for orchestrating the different components of the solution.

A message sent through Telegram triggered the agent, which interpreted the request and used different information sources depending on the context of the question.

### Simplified flow

```text
User
  ↓
Telegram
  ↓
n8n
  ↓
AI Agent
   ├── Cohere Chat Model
   ├── Memory
   ├── Vector Store / RAG
   └── MySQL
  ↓
Telegram
  ↓
Response to the user
```

The agent could retrieve information through vector-based context or query structured data from the database, depending on the type of request.

---

## 🤖 Main agent workflow

The main workflow connects Telegram to the AI agent and to the different tools used during execution.

The components included:

- Cohere language model;
- conversation memory;
- vector storage;
- embeddings;
- MySQL queries;
- Telegram integration.

![Main agent workflow](assets/agent-workflow.png)

---

## 🧠 RAG and context retrieval

Part of the information used by the agent was prepared in a separate workflow.

In this process, an external source was accessed through an HTTP request and its data was loaded for processing.

Cohere was used to generate **embeddings**, vector representations of the content that later allowed similarity-based searches.

These data were stored in a **Vector Store**, allowing the agent to retrieve relevant information during conversations.

### Simplified data preparation flow

```text
Data source
    ↓
HTTP Request
    ↓
Data Loader
    ↓
Cohere Embeddings
    ↓
Vector Store
    ↓
Context retrieval by the agent
```

### Data preparation workflow

![RAG ingestion workflow](assets/rag-ingestion-workflow.png)

---

## 💬 Interaction examples

### General company information

The agent could answer questions about institutional information stored in its knowledge base.

In the example below, the user asks about the work models offered by the fictional company used in the project.

<p align="center">
  <img src="assets/company-info-demo.jpeg" alt="Response about work models" width="280">
</p>

---

### Vacation policy

The context retrieval mechanism also allowed the agent to answer questions about internal policies.

In the example below, the agent retrieves information related to the company’s vacation rules and returns the response directly through Telegram.

<p align="center">
  <img src="assets/vacation-policy-demo.jpeg" alt="Response about vacation policy" width="280">
</p>

---

### Employee-specific data lookup

In addition to retrieving general information, the agent could also query structured data stored in a **MySQL** database.

For requests related to individual information, such as vacation balance, the agent used the provided name to search for a matching record in the database.

During testing, the name **"Eric Renné"** was initially provided.

Because this name did not match any record in the project database, the agent reported that no information could be found for that employee.

Then, **"Eric Monné"** was provided, which matched an existing record in the dataset. The agent was then able to correctly retrieve the corresponding vacation balance.

<p align="center">
  <img src="assets/employee-lookup-demo.jpeg" alt="Employee database lookup" width="280">
</p>

This behavior demonstrates the integration between the AI agent and a structured data source, ensuring that the response depended on records actually available in the database.

> The names, companies, and data shown in the demonstrations belong to the fictional scenario used in the project and do not represent real employee information.

---

## 🛠️ Technologies used

- **n8n** — workflow building and orchestration;
- **Cohere Chat Model** — language model used by the agent;
- **Cohere Embeddings** — generation of vector representations;
- **MySQL** — storage and querying of structured data;
- **Telegram Bot** — interface used for interaction with the agent;
- **Simple Vector Store** — vector data storage.

---

## 📚 Concepts and learnings

This project represented my first hands-on experience with several concepts related to Generative AI, AI agents, and automation.

During the immersion, I was able to explore in practice:

- how AI agents work;
- RAG (Retrieval-Augmented Generation);
- embeddings and vector storage;
- context retrieval;
- memory in AI agents;
- integration between LLMs and external sources;
- integration with relational databases;
- workflow automation with n8n;
- integration between different services;
- use of Telegram as the agent interface;
- low-code development;
- workflow testing and troubleshooting.

More than learning each technology individually, the project helped me understand how these components can be connected within a single solution capable of interpreting requests, retrieving information from different sources, querying structured data, and generating contextualized responses.

---

## ⚠️ About this repository

Some of the platforms used had limited free access. After this access period ended, the environment used for the project was no longer available and the original workflows could no longer be recovered.

For this reason, this repository aims to document the solution through its architecture, technologies, screenshots, and the main learnings obtained during development.

Therefore, it **does not represent a currently executable implementation**, but instead documents the development and behavior of the solution built during the experience.
