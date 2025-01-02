# simplelocalrag - PDF Q&A with LlamaIndex and Ollama

## Overview
This repository provides a minimal example of how to perform question-answering on a PDF document using **LlamaIndex** and **Ollama**. I rely on:
- **mxbai-embed-large** as the local embedding model and
- **llama3.2** as the local generation model

Simply provide a PDF, open the Jupyter Notebook and start the code, then ask natural-language questions to get context-aware answers.

## Requirements

- Python 3.8+  
- [Ollama](https://github.com/jmorganca/ollama) installed and running locally on `http://localhost:11411`  
  - Make sure you have the models **mxbai-embed-large** (for embeddings) and **llama3.2** (for text generation) available in Ollama.
- Required Python packages (install via `pip`):
  ```bash
pip install llama-index llama-index-llms-ollama llama-index-embeddings-ollama  requests
```

## Quickstart
1. Start Ollama
Launch Ollama so it serves on the default port (11411). Confirm you have the models:

ollama run mxbai-embed-large
ollama run llama3.2
(These commands just verify that the models are recognized. Then stop them if needed.)

2. Place Your PDF
Copy your PDF file (e.g., test.pdf) into the working directory.

Open the Jupyter Notebook and start the code (maybe install the requirements first or just start if already done).

3. Ask a Question

When prompted, type your natural language question.
The system will use mxbai-embed-large to find the most relevant PDF chunks from ChromaDB and then call llama3.2 to generate a final answer.


## Features
Automatic Chunking: The PDF is automatically split into manageable text segments.
Local Embeddings & Generation: Uses mxbai-embed-large for embeddings and llama3.2 for text generation via Ollama—no external API required.
Interactive Q&A: Simply enter your question, and the relevant PDF context plus a generated answer appear in your console.

## How It Works
Load and Chunk: SimpleDirectoryReader extracts text from your PDF and splits it into nodes/chunks.
Embed Chunks: Chunks are embedded locally with mxbai-embed-large via Ollama.
User Query: On each question, the query is also embedded with mxbai-embed-large.
Similarity Search: VectorStoreIndex finds the most relevant chunks.
Answer Generation: The final prompt + context is sent to llama3.2 to produce a human-readable answer.


## Credits
This example was created with LlamaIndex and Ollama. It showcases how to combine local embedding and generation models for a streamlined, privacy-friendly PDF Q&A experience.
