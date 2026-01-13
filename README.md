# arxiv-two-stage-retrieval
Semantic Search for Scientific Papers (arXiv)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.1-orange)
![Status](https://img.shields.io/badge/Status-Educational_Project-green)

This project implements a high-performance semantic search engine capable of retrieving relevant scientific papers based on natural language queries. 
The system utilizes a Two-Stage Retrieval pipeline to achieve high accuracy (MRR@5 = 0.938) while maintaining low latency.

🚀 Project Overview

The goal of this project was to build a search system that indexes scientific articles (from the arXiv dataset) and matches them with user queries. 
Unlike keyword-based search (e.g., BM25), this system uses dense vector embeddings to understand the semantic meaning of the text. 


⚙️Key Features
- Semantic Understanding: Matches queries to documents based on meaning, not just keyword overlap.
- Two-Stage Pipeline: Combines fast retrieval with precise re-ranking.
- High Accuracy: Achieved a Mean Reciprocal Rank (MRR@5) of 0.938.
- Performance Profiling: Includes detailed latency analysis of system components.

🛠️ Tech Stack
- Python 3.10+
- LangChain: For orchestration and document loading.
- FAISS: For efficient similarity search and vector indexing.
- Sentence-Transformers: For state-of-the-art embedding models.
- Pandas / NumPy: For data manipulation and metric calculation.


⚙️ Architecture & Pipeline
The system processes data by concatenating the paper's title and abstract. The search pipeline consists of two distinct stages:
1. Retrieval (Candidate Generation)
   - Model: BAAI/bge-large-en-v1.5 (Bi-Encoder).
   - Index: FAISS (FlatL2).
   - Process: The system converts the query into a vector and retrieves the top-20 most similar documents from the index.
   - Role: Fast filtering of the entire corpus.
2. Re-ranking (Precision Refinement)
   - Model: cross-encoder/ms-marco-MiniLM-L-6-v2.
   - Process: The Cross-Encoder takes the query and the top-20 candidates, "reads" them as pairs, and assigns a relevance score. The results are re-sorted, and the top-5 are returned.
   - Role: Maximizing accuracy by analyzing context deeply.

📊 Performance & Results

The system was evaluated on a test dataset of 1,000 queries.

<img width="572" height="121" alt="image" src="https://github.com/user-attachments/assets/4355c6c2-d05e-461c-b827-c28e68978a40" />
<img width="796" height="494" alt="image" src="https://github.com/user-attachments/assets/b2e0931b-e217-4369-9d56-22d94baaf331" />



📊 Latency Profiling

We analyzed the time distribution for a single query:
- Retrieval Phase: ~40% (63ms)
- Re-ranking Phase: ~60% (94ms)
While the Re-ranking step introduces additional latency, it provides a crucial boost in retrieval quality.
<img width="764" height="383" alt="image" src="https://github.com/user-attachments/assets/d2e20fdb-4f33-4eef-a0d9-748bac55c118" />

