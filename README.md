# Agentic AI Chatbot

A conversational AI chatbot built with **LangGraph** and **Streamlit**, designed to explore the core concepts behind stateful and agentic AI applications.

The project is being developed incrementally, with a focus on understanding how modern LLM applications manage conversation state, persistence, streaming, and eventually agentic workflows.

## 🚀 Current Features

* 💬 Interactive chatbot interface using Streamlit
* 🧠 Conversation management using LangGraph
* 🔄 Multiple independent conversation threads
* 💾 Persistent conversation storage
* ▶️ Resume previous conversations
* ⚡ Streaming LLM responses with a typewriter-style effect
* 🆔 Thread-based conversation management
* 🔐 Environment variable support for API keys

## 🏗️ Architecture

The current application follows a simple LangGraph-based architecture:

```text
                    Streamlit UI
                         │
                         ▼
                  User Message
                         │
                         ▼
                    LangGraph
                         │
                         ▼
                    Chat Node
                         │
                         ▼
                    Chat Model
                         │
                         ▼
                 Updated State
                         │
                         ▼
                Persistent Storage
                         │
                         ▼
                  Streamlit UI
```

Each conversation is associated with a unique `thread_id`.

```text
Conversation 1
    └── thread_id: abc123
        └── message history

Conversation 2
    └── thread_id: xyz789
        └── message history
```

This allows multiple conversations to exist independently and be resumed later.

## 🧩 Tech Stack

* **Python**
* **LangGraph** – graph-based orchestration and state management
* **LangChain** – LLM and message abstractions
* **Streamlit** – chatbot frontend
* **OpenAI** – LLM
* **SQLite / Persistent Checkpointer** – conversation persistence
* **python-dotenv** – environment variable management

## 📁 Project Structure

```text
agentic-ai-chatbot/
│
├── langgraph_backend.py    # LangGraph workflow and chatbot logic
├── frontend.py             # Streamlit chatbot interface
├── .env                    # API keys and environment variables
├── .gitignore
├── requirements.txt
└── README.md
```

> File names may change as the project evolves.

## ⚙️ Setup

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd agentic-ai-chatbot
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key
```

Do **not** commit your `.env` file to GitHub.

Make sure it is included in `.gitignore`:

```text
.env
venv/
__pycache__/
```

### 5. Run the application

```bash
streamlit run frontend.py
```

The application will open in your browser.

## 💾 Conversation Persistence

The chatbot uses LangGraph's checkpointing mechanism to maintain conversation state.

Each conversation is identified using a unique `thread_id`:

```python
config = {
    "configurable": {
        "thread_id": thread_id
    }
}
```

The checkpointer associates the conversation state with this ID.

This enables the application to:

1. Create a new conversation.
2. Store its message history.
3. Create additional independent conversations.
4. Switch between conversations.
5. Resume an existing conversation.

Unlike an in-memory checkpointer, the current persistent storage approach allows conversation data to survive application restarts.

## ⚡ Streaming

The chatbot uses LangGraph's streaming capabilities to display LLM responses incrementally.

Instead of waiting for the complete response:

```text
Generate entire response
        ↓
Display response
```

the application receives chunks as they are generated:

```text
Generate chunk
      ↓
Display chunk
      ↓
Generate chunk
      ↓
Display chunk
      ↓
...
```

This provides a more responsive chatbot experience.

## 🧠 Concepts Explored

This project is primarily being used to understand and implement the following concepts:

* LangGraph state
* StateGraph
* Nodes and edges
* Message reducers
* Checkpointing
* Thread IDs
* Persistent state
* Conversation history
* Streaming
* Python generators
* Streamlit session state
* Stateful chatbot architectures

## 🛣️ Roadmap

The project will gradually evolve from a simple stateful chatbot into a more capable **Agentic AI system**.

Planned areas include:

* [ ] Tool calling
* [ ] Agent workflows
* [ ] ReAct-style agents
* [ ] Human-in-the-loop workflows
* [ ] Retrieval-Augmented Generation (RAG)
* [ ] Advanced RAG
* [ ] Agentic RAG
* [ ] Multiple tools and tool routing
* [ ] Long-term memory
* [ ] RAG evaluation
* [ ] Agent evaluation
* [ ] Production-oriented architecture

## 🎯 Project Goal

The goal of this project is not simply to build a chatbot, but to progressively understand how **stateful, retrieval-based, and agentic AI systems are designed and implemented**.

The project will evolve incrementally as new concepts are learned and implemented.

## 📌 Current Status

**Phase 1 – Stateful Chatbot**

Currently implemented:

```text
Streamlit
    ↓
LangGraph
    ↓
Chat Model
    ↓
Thread-based State
    ↓
Persistent Conversation Storage
    ↓
Resume Conversations
```

The next stage is to introduce **tools and agentic workflows** and gradually build toward an Agentic RAG system.

## 📄 License

This project is primarily intended for learning and experimentation.
