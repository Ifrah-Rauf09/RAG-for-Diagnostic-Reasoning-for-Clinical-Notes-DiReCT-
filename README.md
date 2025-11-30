**Clinical RAG System – DiReCT (MIMIC-IV)**

A Retrieval-Augmented Generation (RAG) pipeline built using the MIMIC-IV-Ext Direct dataset.
The system retrieves clinically relevant evidence from patient notes and generates grounded answers using transformer models.
Includes a full Streamlit Frontend, Colab-friendly setup, and evaluation suite.

**Project Structure**
├── app.py                    # Streamlit Frontend
├── DiReCT_rag_eval.py       # Full RAG backend (retrieval + generation + evaluation)
├── data/
│   └── samples_extracted/   # Extracted JSON files from samples.rar
├── README.md                # Project documentation

**Features**
End-to-end RAG pipeline
BM25 + embedding hybrid retrieval
Transformer-based answer generation
Automatic evaluation (precision, recall, BLEU, coherence)
Streamlit UI for interactive querying
Fully modular and documented
Works perfectly on Google Colab

**Requirements**
Install dependencies:
pip install streamlit rank_bm25 sentence-transformers rarfile tqdm numpy torch
If using Colab, also:
sudo apt-get install unrar

**Dataset Setup**
Upload the provided ZIP file to Google Drive.
The backend automatically:
mounts Google Drive
extracts the ZIP
extracts samples.rar
loads JSON files

**Running the Streamlit App**
streamlit run app.py
The UI will open in the browser.

**How It Works**
1. Retrieval
Uses:
BM25 lexical scores
Embedding cosine similarities
Hybrid ranking

2. Generation
The top-k retrieved chunks are combined with the user query and provided to the LLM.

3. Evaluation
Includes:
BLEU
Precision & Recall
Coherence
Manual inspection tools

**Example Query**
What symptoms are commonly associated with acute heart failure?
The app will display:
Retrieved evidence documents
The model-generated final answer

**Inline Documentation**
Each major function in the backend contains:
descriptive docstrings
comments explaining logic
clear variable names

**Author**
Ifrah Rauf and Eman Fatima
7th-Semester Computer Science
**Linkedin**
https://www.linkedin.com/in/eman-fatima-145a86282/
https://www.linkedin.com/in/ifrah-rauf-686633351/
**GitHub**
https://github.com/Eman123123
https://github.com/Ifrah-Rauf09


