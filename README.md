# RAG-Powered Document Search System

A production-ready Retrieval-Augmented Generation (RAG) application that enables intelligent document search and question-answering using FAISS vector database, LangChain, and Groq LLM.

## 🚀 Features

- **Multi-Format Document Support**: Load and process PDF, TXT, CSV, Excel, Word, and JSON files
- **Intelligent Document Chunking**: Automatic text splitting with configurable chunk size and overlap
- **Vector Embeddings**: Generate embeddings using SentenceTransformer models
- **FAISS Vector Store**: Fast similarity search with persistent storage
- **Typesense Integration**: Alternative vector database support
- **LLM Integration**: Answer questions using Groq's language models
- **Modular Architecture**: Clean, maintainable code structure

## 📁 Project Structure

```
RAG/
├── src/
│   ├── data_loader.py       # Document loading from multiple formats
│   ├── embedding.py          # Text chunking and embedding generation
│   ├── vectorstore.py        # FAISS vector store management
│   └── search.py             # RAG search and LLM integration
├── data/                     # Document storage directory
├── notebook/
│   └── pdf_loader.ipynb      # Jupyter notebook for experimentation
├── faiss_store/              # Persisted FAISS index and metadata
├── app.py                    # Simple example application
├── main.py                   # Main application entry point
├── typesense.ipynb           # Typesense integration examples
├── requirements.txt          # Project dependencies
├── pyproject.toml            # UV project configuration
└── .env                      # Environment variables (API keys)
```

## 🛠️ Installation

### Prerequisites
- Python 3.13 or higher
- UV package manager (recommended) or pip

### Setup

1. **Clone the repository:**
```bash
git clone <your-repo-url>
cd RAG
```

2. **Create virtual environment and install dependencies:**

Using UV (recommended):
```bash
uv venv
.venv\Scripts\activate  # Windows
uv pip install -r requirements.txt
```

Using pip:
```bash
python -m venv .venv
.venv\Scripts\activate  # Windows
pip install -r requirements.txt
```

3. **Set up environment variables:**
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here
TYPESENSE_API_KEY=your_typesense_api_key_here  # Optional
```

4. **Add your documents:**
Place your PDF, TXT, or other supported files in the `data/` directory.

## 📖 Usage

### Basic Usage

```python
from src.data_loader import load_all_documents
from src.embedding import EmbeddingPipeline
from src.vectorstore import FaissVectorStore

# Load documents
docs = load_all_documents("data")

# Initialize and build vector store
vectorstore = FaissVectorStore(persist_dir="faiss_store")
vectorstore.build_from_documents(docs)

# Query the vector store
results = vectorstore.query("What is machine learning?", top_k=5)
```

### Using RAG Search with LLM

```python
from src.search import RAGSearch

# Initialize RAG search
rag = RAGSearch(
    persist_dir="faiss_store",
    embedding_model="all-MiniLM-L6-v2",
    llm_model="llama-3.3-70b-versatile"
)

# Ask questions
answer = rag.search_and_summarize(
    "Explain the concept of attention mechanism in neural networks",
    top_k=5
)
print(answer)
```

### Run the Application

```bash
python app.py
```

## 🔧 Configuration

### Embedding Models
Change the embedding model in initialization:
```python
EmbeddingPipeline(model_name="all-MiniLM-L6-v2")
# Other options: "all-mpnet-base-v2", "multi-qa-MiniLM-L6-cos-v1"
```

### Chunk Size and Overlap
```python
EmbeddingPipeline(chunk_size=1000, chunk_overlap=200)
```

### LLM Models (Groq)
Available models:
- `llama-3.3-70b-versatile`
- `mixtral-8x7b-32768`
- `gemma2-9b-it`

## 📦 Dependencies

Core dependencies:
- `langchain` - Framework for LLM applications
- `langchain-community` - Community integrations
- `langchain-groq` - Groq LLM integration
- `langchain-huggingface` - HuggingFace embeddings
- `sentence-transformers` - Embedding models
- `faiss-cpu` - Vector similarity search
- `pypdf` - PDF processing
- `python-dotenv` - Environment variable management

## 🎯 Key Components

### 1. Data Loader (`data_loader.py`)
- Loads documents from multiple formats (PDF, TXT, CSV, Excel, Word, JSON)
- Recursively scans directories
- Handles errors gracefully

### 2. Embedding Pipeline (`embedding.py`)
- Chunks documents using RecursiveCharacterTextSplitter
- Generates embeddings with SentenceTransformer
- Configurable chunk size and overlap

### 3. Vector Store (`vectorstore.py`)
- FAISS-based vector storage
- Persistent storage (save/load functionality)
- Fast similarity search
- Metadata tracking

### 4. RAG Search (`search.py`)
- Combines vector search with LLM
- Context-aware question answering
- Automatic vector store building/loading

## 🔬 Jupyter Notebooks

### `notebook/pdf_loader.ipynb`
Complete RAG pipeline demonstration:
- Document loading and processing
- Text splitting and chunking
- Embedding generation
- Vector store creation (ChromaDB)
- RAG retrieval and querying
- LLM integration with streaming
- Advanced features (citations, history, summarization)

### `typesense.ipynb`
Typesense vector database integration:
- Alternative to FAISS
- Cloud-based vector search
- Real-time indexing

## 🚧 Troubleshooting

### Python Version Issues
If using Python 3.14 with LangChain:
```bash
# Downgrade to Python 3.13
uv python install 3.13
uv python pin 3.13
# Recreate virtual environment
```

### Import Errors
Make sure all dependencies are installed:
```bash
uv pip install -r requirements.txt
```

### UV Not Recognized
Add Python Scripts to PATH:
```powershell
$env:PATH += ";C:\Users\<YourUsername>\AppData\Roaming\Python\Python313\Scripts"
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) for the RAG framework
- [FAISS](https://github.com/facebookresearch/faiss) for vector search
- [Sentence-Transformers](https://www.sbert.net/) for embeddings
- [Groq](https://groq.com/) for fast LLM inference

## 📧 Contact

For questions or feedback, please open an issue on GitHub.