# 🚗 Car Dealership AI Assistant

An open-source, production-ready AI chatbot for automotive dealerships built with **LangFlow**, **Ollama**, **Google Gemini**, and **ChromaDB**.
<p align="center">
  <img src="https://cdn.simpleicons.org/langflow/4F46E5" height="28" title="LangFlow"/>
  &nbsp;&nbsp;
  <img src="https://cdn.simpleicons.org/googlegemini/4285F4" height="28" title="Gemini"/>
  &nbsp;&nbsp;
  <img src="https://cdn.simpleicons.org/ollama/white" height="28" title="Ollama"/>
  &nbsp;&nbsp;
  <img src="https://www.trychroma.com/_next/static/media/chroma-wordmark.91ab668b.svg" height="28" title="ChromaDB"/>
</p>

<video src="final_sub.mp4" controls width="600">
  Your browser does not support the video tag.
</video>


## 📋 Overview

This project demonstrates how to build intelligent, domain-specific chatbots for any business. Our implementation helps car dealership customers get instant, accurate answers about general queries related to Dealership policies & procedures, financing & leasing options, service info, warranty and much more.


## 🎯 How It Works

### Architecture Overview

```
User Query
    ↓
[Embeddings] → Convert text to vectors
    ↓
[ChromaDB] → Retrieve relevant context documents
    ↓
[Prompt Template] → Combine context + history + query
    ↓
[LLM] → Generate natural language response
    ↓
Response + Memory Storage
```

### Step-by-Step Process

#### 1. **Embedding with Ollama**
- Dealership documents (policies, FAQs, vehicle specs) are split into chunks
- Embedding model generates local vector embeddings for each chunk
- Embeddings are stored in ChromaDB for fast semantic search
- **Benefit**: No data leaves your infrastructure; full privacy control

#### 2. **Retrieval-Augmented Generation (RAG) with ChromaDB**
- User asks a question
- Question is embedded using the same Ollama model
- ChromaDB performs semantic similarity search to find relevant documents
- Top results are retrieved as context for the LLM
- **Benefit**: Responses are grounded in your actual dealership data

#### 3. **Response Generation with LLM**
- Retrieved context + conversation history + user query are formatted into a prompt
- Google Gemini generates a natural, conversational response
- Response is stored in message memory for future context
- **Benefit**: State-of-the-art language understanding and generation


## 🚀 Getting Started

### Prerequisites
- Docker & Docker Compose installed
- Google Gemini API key (get one [here](https://makersuite.google.com/app/apikey))
- Ollama installed locally (optional; can use via container)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/car-dealership-chatbot.git
   cd car-dealership-chatbot
   ```

2. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env and add your Google Gemini API key
   ```

3. **Start services with Docker**
   ```bash
   docker compose up -d
   ```
   This starts:
   - **LangFlow** (UI) → http://localhost:7860
   - **ChromaDB** (Vector Store) → http://localhost:8000
   - **PostgreSQL** (Database) → localhost:5432

4. **Add your dealership data**
   - Place dealership documents (`.txt`, `.pdf`) in the `./data` folder
   - LangFlow will automatically ingest and embed them

5. **Access the chatbot**
   - Open http://localhost:7860 in your browser
   - Load the `Car_Dealership_Chatbot.json` workflow
   - Start chatting!


## ⚙️ Configuration

### Embedding Model (Ollama)
Change the embedding model in LangFlow:
- **Base URL**: `http://host.docker.internal:11434` (default)
- **Model**: Select any Ollama embedding model (e.g., `nomic-embed-text`)
- **Privacy**: All embeddings stay local

### LLM (Google Gemini)
- Add your API key to `.env`
- Available models: `gemini-pro`, `gemini-1.5-pro`
- Custom instructions can be set in the Prompt Template component

### Vector Store (ChromaDB)
- **Persist Directory**: `./chroma/data`
- **Collection Name**: `dealership`
- **Similarity Search Type**: Similarity (default) or MMR


## 📊 Workflow Components

The LangFlow workflow includes:

| Component | Role |
|-----------|------|
| **File Input** | Upload dealership documents |
| **Split Text** | Chunk documents for embedding |
| **Ollama Embeddings** | Generate vector embeddings |
| **ChromaDB** | Store and retrieve vectors |
| **Chat Input** | Accept user questions |
| **Prompt Template** | Format context + history + query |
| **Google Generative AI** | Generate responses |
| **Chat Output** | Display responses |
| **Message History** | Store conversation memory |

---

## 🧪 Testing the Chatbot

### Test Prompts

1. **Policy Question**
   > "What are your store hours on Saturday?"

2. **Warranty Question**
   > "What's covered under the manufacturer warranty?"

3. **Service Question**
   > "How long does an oil change take?"

4. **Financing Question**
   > "What financing options do you offer for someone with fair credit?"

5. **Vehicle Question**
   > "Tell me about the safety features of your popular models."


## 📁 Project Structure

```
car-dealership-chatbot/
├── Car_Dealership_Chatbot.json    # LangFlow workflow definition
├── dealership.txt                 # Dealership knowledge base
├── docker-compose.yml             # Container orchestration
├── .env.example                   # Environment template
├── data/                          # Documents to embed
│   └── (add your .txt/.pdf files here)
├── chroma/                        # ChromaDB persistence
│   └── data/
└── README.md
```


## 🔄 Deployment

### Local Development
```bash
docker compose up -d
```


## 🤝 Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements.



## 🎓 Learn More

- [LangFlow Documentation](https://docs.langflow.org)
- [Ollama Documentation](https://github.com/ollama/ollama)
- [ChromaDB Documentation](https://docs.trychroma.com)
- [Google Generative AI](https://ai.google.dev)