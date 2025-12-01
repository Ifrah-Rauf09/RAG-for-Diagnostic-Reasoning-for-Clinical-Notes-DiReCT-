**Clinical RAG System – DiReCT (MIMIC-IV-Ext Direct)**

A complete Retrieval-Augmented Generation platform for clinical question answering.

****Overview**
DiReCT — Clinical RAG System is a full-pipeline Retrieval-Augmented Generation (RAG) framework designed to work with the MIMIC-IV-Ext Direct dataset.
It retrieves clinically relevant evidence from patient records using sentence-transformer embeddings + FAISS, then generates grounded answers using a Flan-T5 transformer model.

The system includes:

Document ingestion (JSON/TXT/CSV auto-parsing + chunking)
FAISS-based dense retrieval
Transformer-based answer generation (Flan-T5 Large)
Complete evaluation suite
Precision / Recall
BLEU
ROUGE-L
Semantic coherence
Interactive Streamlit app
Colab-friendly scripts for embedding, indexing, generation & evaluation

**Project Structure**
├── direct_app.py                 # Streamlit Frontend (Interactive RAG UI)
├── main_colab_setup.ipynb        # Colab pipeline (embedding, indexing, evaluation)
├── documents.pkl                 # Saved chunked documents
├── faiss_index.index             # FAISS index of embeddings
├── data/
│   ├── mimic-iv-ext-direct-1.0.0.zip
│   └── samples_extracted/        # Extracted JSON/TXT files
├── README.md                     # Project documentation (this file)

**Features**
✓ End-to-End RAG Pipeline
Automatic loading, cleaning, chunking, and embedding of clinical notes
Fast FAISS inner-product retrieval
Grounded generation using Flan-T5 Large

✓ Evaluation Suite
For every generated answer:
Precision & Recall (retrieval quality)
BLEU score
ROUGE-L score
Embedding-based coherence metric

✓ Streamlit Frontend
Clean UI to submit clinical questions
Displays retrieved evidence
Shows grounded LLM answers
Works with ngrok for public sharing via Colab

✓ Colab-Friendly
Automatic dependency installation
Automatic Google Drive mounting
Automatic extraction of .rar and .zip clinical datasets
No manual steps required except uploading your dataset

**Requirements**
Core Libraries
pip install sentence-transformers faiss-cpu transformers accelerate datasets
pip install streamlit pyngrok rouge-score tqdm nltk

If using Google Colab
sudo apt-get install unrar

**Models Used**
Embeddings → sentence-transformers/all-MiniLM-L6-v2
Generator → google/flan-t5-large

**Dataset Setup (MIMIC-IV-Ext Direct)**
1. Upload the dataset to Google Drive
Upload the file:
mimic-iv-ext-direct-1.0.0.zip
to:
MyDrive/
2. Colab Code Automatically:
mounts Google Drive
extracts the ZIP
locates samples.rar
extracts samples_extracted/
recursively scans JSON/TXT/CSV to build documents
chunks, embeds, and indexes everything
No manual extraction required.

**How the System Works**
1️.Preprocessing & Document Chunking
All JSON/TXT/CSV files from samples_extracted/ are scanned
JSON is auto-parsed and flattened
Text is chunked into ~800-word segments
Each chunk receives a UUID and metadata
Purpose: Normalize the dataset for embedding + retrieval.

2️.Embedding & FAISS Index
Uses all-MiniLM-L6-v2 (384-dim embeddings)
All embeddings are normalized (L2)
Stored inside FAISS IndexFlatIP (inner-product for cosine similarity)
Produces:
faiss_index.index
documents.pkl

3️.Dense Retrieval
Example:
retrieve("shortness of breath and fever", k=3)
Returns the top-k most relevant document fragments.
Retrieval score = cosine similarity of embeddings.

4️.Prompt Construction
The RAG prompt includes:
User query
Truncated (350-token) retrieved chunks
Strict grounding:
“Use ONLY the provided context…”

5️.LLM Answer Generation
The system uses:
Flan-T5 Large
Max 256 new tokens
Deterministic (no sampling)

6️.Evaluation Metrics
Retrieval
Precision
Recall
Count of matched keywords
Generation
BLEU
ROUGE-L
Coherence (semantic similarity between reference & prediction)
Automatically generated during rag_chat() mode.

**Running the Streamlit App**
Local Machine
streamlit run direct_app.py
Google Colab (with ngrok)
Your script already automates:
ngrok.set_auth_token()
streamlit run direct_app.py --server.port 6006
ngrok.connect(6006)

This generates a public URL for the app.

**Example Clinical Query**
Query:
What are the current vitals and chief complaint of the patient?

The app will show:
Retrieved documents (with cosine scores & file source)
A grounded final answer
Evaluation metrics (if run via CLI mode)

**Inline Documentation**
All major components include:
✔ Docstrings describing functionality
✔ Inline comments explaining purpose & logic
✔ Clear variable names
✔ Modular architecture for readability

**Components documented include:**
Dataset loading
RAR/ZIP extraction
JSON parsing
Chunking
Embedding
FAISS indexing
Retrieval
Prompt construction
Answer generation
Streamlit UI hooks
Evaluation utilities

**Authors**
Ifrah Rauf
7th-Semester Computer Science
GitHub: https://github.com/Ifrah-Rauf09
LinkedIn: https://www.linkedin.com/in/ifrah-rauf-686633351/

Eman Fatima
7th-Semester Computer Science
GitHub: https://github.com/Eman123123
LinkedIn: https://www.linkedin.com/in/eman-fatima-145a86282/
