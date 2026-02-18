# Mini Retrieval-Augmented Generation (RAG) Chatbot
## Project Overview
This project implements a Retrieval-Augmented Generation (RAG) based Question Answering system that allows users to upload multiple PDF or text documents and ask questions based on their content.
The system retrieves relevant document chunks using vector similarity search and generates context-aware answers using a Large Language Model (LLM). It combines semantic search with generative AI to provide accurate, document-grounded responses.
The key objective of this project is to demonstrate understanding of embeddings, vector databases, retrieval pipelines, prompt engineering, and clean modular system design.

## System Architecture
The system follows a standard RAG pipeline:
1. Document Ingestion
Multiple PDF and text documents are uploaded through the user interface.
2. Text Chunking
Documents are split into manageable chunks to improve semantic retrieval accuracy.
3. Embedding Generation
Each chunk is converted into a dense vector representation using a SentenceTransformer embedding model.
4. Vector Storage
The embeddings are stored in a FAISS vector index for efficient similarity search.
5. Query Processing
When a user submits a question:
* The query is converted into an embedding.
* FAISS retrieves the top-k most relevant chunks.
* Retrieved chunks are combined as context.
6. Answer Generation
The LLM generates an answer using only the retrieved context.
This architecture ensures that responses are grounded in the uploaded documents rather than relying solely on the model’s internal knowledge.

## Setup Instructions
### 1. Install Dependencies
install requirements.txt file or else,
install manually:
pip install langchain
pip install langchain_community
pip install sentence-transformers
pip install faiss-cpu
pip install transformers
pip install gradio

## Model Explanation
### Embedding Model
The project uses a SentenceTransformer model to convert text chunks and user queries into dense vector embeddings. These embeddings capture semantic meaning, allowing similar content to be retrieved even if exact keywords do not match.
The embedding model maps text into a fixed-dimensional vector space, enabling similarity comparison using distance metrics such as L2 or cosine similarity.
pip install gradio

### Vector Database (FAISS)
FAISS (Facebook AI Similarity Search) is used to store and search embeddings efficiently. It allows fast nearest-neighbor search, even for large collections of vectors.
When a query embedding is generated, FAISS retrieves the top-k most similar chunk embeddings based on vector distance.

### Language Model
A pre-trained sequence-to-sequence transformer model is used to generate answers from the retrieved context.
The prompt is designed to:
* Restrict the model to use only the retrieved context
* Reduce hallucination
* Provide structured and concise answers
* Return a fallback response if the answer is not present in the context

## User Workflow
1. Upload multiple PDF or text documents.
2. The system processes and indexes the documents.
3. Enter a question in the interface.
4. The system retrieves relevant chunks and generates a contextual answer.

## Output Description
The interface displays:
* The generated answer based on retrieved context.
* The system internally retrieves top-k relevant chunks before generation.
* Slight wording variations may occur since the model generates semantically equivalent responses rather than copying text verbatim.

## Performance and Observations
* The system demonstrates strong retrieval-based answering.
* Accuracy depends on chunk size, value of k, and the strength of the language model.
* Slight paraphrasing differences are expected due to generative output.

## Limitations
* Performance depends on embedding model quality.
* Small language models may occasionally paraphrase inaccurately.
* Retrieval quality is affected by chunk size and overlap settings.
* The system does not currently include reranking or advanced retrieval strategies.
