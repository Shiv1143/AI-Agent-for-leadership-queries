## AI Leadership Insight Agent

This is a Retrieval-Augmented Generation (RAG) system built in a Google Colab notebook that acts as an AI-powered analyst for company leadership.
You feed it internal company documents — annual reports, quarterly earnings, strategy notes, operational updates — and it lets executives ask plain-English questions like “Which departments are underperforming?” or “What were the key risks last quarter?” and get back concise, factual answers that cite the exact source documents.
Under the hood, it chunks the documents into passages, converts them into vector embeddings using a sentence-transformer model, stores them in a FAISS index, and at query time retrieves the most relevant passages and passes them to Claude to generate a grounded answer. It ships with four realistic sample company documents so it runs immediately out of the box, plus a Gradio chat UI for live Q&A.
The core guarantee: the agent only answers from what’s in your documents — it won’t hallucinate facts it doesn’t have.​​​​​​​​​​​​​​​​

### Features

	∙	Natural language Q&A — ask questions the way you’d ask a senior analyst
	∙	Grounded answers — every claim is traced back to a source document
	∙	Multi-format ingestion — supports PDF, DOCX, and TXT files
	∙	Semantic search — finds relevant context even when exact keywords differ
	∙	Interactive UI — Gradio chat interface with example questions included
	∙	Zero infrastructure — runs entirely inside Google Colab, no servers needed
	∙	Plug-and-play — ships with realistic sample documents; works immediately

Quickstart
1. Open the notebook
Upload AI_Leadership_Insight_Agent.ipynb to Google Colab or click Open in Colab if hosted on GitHub.
https://colab.research.google.com/drive/19kHRI6mEY9bmydpq0J6jGMdhz_ej54Ko?usp=sharing

3. Get an Open AI API key

4. Run all cells
The notebook will prompt you to enter your API key securely, then:
	∙	Install all dependencies automatically
	∙	Load the built-in sample documents
	∙	Build the vector index
	∙	Launch the Gradio chat UI
5. Ask questions
Use the chat interface or run individual question cells


### Configuration
All key parameters are set in one place at the top of the notebook:
CONFIG = {
    "model":           "gpt-4o-mini",  # LLM to use
    "max_tokens":      1024,                          # Max length of each answer
    "chunk_size":      800,                           # Characters per text chunk
    "chunk_overlap":   150,                           # Overlap between chunks
    "top_k":           5,                             # Chunks retrieved per query
    "embedding_model": "all-MiniLM-L6-v2",            # Sentence-transformer model
}

### Project Structure

AI_Leadership_Insight_Agent.ipynb
│
├── Step 1  — Install dependencies
├── Step 2  — Configuration & API key
├── Step 3  — Document ingestion (PDF / DOCX / TXT loaders + sample docs)
├── Step 4  — Chunking & embedding (FAISS index build)
├── Step 5  — Retrieval & generation (ask_agent function)
├── Step 6  — Pre-loaded leadership questions (6 examples)
├── Step 7  — Gradio interactive chat UI
├── Step 8  — Retrieval quality evaluator
└── Step 9  — Upload your own documents

### Requirements
	∙	Python 3.9+
	∙	Google Colab (free tier is sufficient)
	∙	Open AI API key 
	∙	Internet connection (for package install and API calls)
All Python dependencies are installed as per required within the notebook:
langchain, 
langchain-text-splitters,  
faiss-cpu, 
sentence-transformers, 
pypdf, 
python-docx, 
gradio, 
tiktoken, 
openai

### Limitations
	Context window — very long documents may exceed what fits in a single LLM call; chunking mitigates this but very niche facts buried deep in large files may not surface
	In-memory index — the FAISS index is rebuilt each session; for persistence across sessions, swap to ChromaDB or Pinecone
 




