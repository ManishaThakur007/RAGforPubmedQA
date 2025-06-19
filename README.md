**Biomedical RAG Pipeline with PubMedQA:**
This repository showcases a Retrieval-Augmented Generation (RAG) pipeline for biomedical question answering using the PubMedQA dataset. It combines dense retrieval (FAISS), sparse retrieval (BM25), reranking (Cohere), and generation (FLAN-T5) to deliver accurate, domain-specific medical answers.

**Project Overview:**

In high-stakes fields like medicine, generic language models often lack the specificity or updated context needed for accurate responses. This pipeline:

* Integrates hybrid retrieval (dense + sparse).

* Applies domain-aware chunking with LangChain.

* Uses semantic embeddings (BAAI/bge-base-en-v1.5).

* Optionally applies Cohere reranking.

* Generates answers using FLAN-T5 with manually composed prompts.

**Dataset:** PubMedQA, a biomedical QA dataset with yes/no/maybe style questions based on clinical abstracts.

**Features:**

Hybrid Retrieval: FAISS + BM25 for robust document matching.

Semantic Chunking: Uses recursive text splitting to maintain contextual integrity.

Cohere Reranker: Enhances relevance ranking (optional).

Manual Prompt Composition: Transparent and adaptable to any generation model.

Medical QA Focus: Tailored for biomedical fact-based, dosage, and policy questions.

**Setup Instructions:**
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/pubmedqa-rag-pipeline.git
cd pubmedqa-rag-pipeline
2. Install Dependencies
bash
Copy
Edit
pip install -r requirements.txt
Or manually:

bash
Copy
Edit
pip install faiss-cpu sentence-transformers rank_bm25 cohere transformers datasets langchain
⚠️ Ensure you have access to Hugging Face and Cohere APIs (optional) for reranking.

3. Set Environment Variables (Optional)
If using Cohere:

bash
Copy
Edit
export COHERE_API_KEY=your_api_key_here
📚 Dataset Access
This project loads PubMedQA subsets via Hugging Face:

python
Copy
Edit
pqa_labeled = pd.read_parquet("hf://datasets/qiaojin/PubMedQA/pqa_labeled/train-00000-of-00001.parquet")
Ensure Hugging Face datasets access is enabled in your environment.

🚀 Run the Pipeline
python
Copy
Edit

# Run hybrid search and answer generation
generate_answer("What is the mechanism of aspirin in heart attack prevention?")
Sample queries for testing are already included in the script.

Evaluation Categories:
* Mechanism-Based: e.g., “How does aspirin prevent heart attacks?”

* Dosage Guidelines: e.g., “Recommended metformin dosage for type 2 diabetes?”

* Comparative Evidence: e.g., “Is metformin more effective than sulfonylureas?”

* Symptom Understanding: e.g., “What are the signs of a heart attack in women?”

* Policy-Based: e.g., “When should children receive the MMR vaccine?”

⚠**Limitations:**
* Real-time or post-2022 guideline updates not guaranteed.

* Contextual truncation due to token limits.

* Some noisy metadata from abstracts may reduce clarity.

* Highly personalized or image-based medical questions are unsupported.

**Future Work:**
* Biomedical-aware sentence-based chunking.

* Query reformulation using LLMs.

* Multi-hop retrieval for reasoning-heavy questions.

* BioBERT-based reranking.

* Fine-tuning on PubMedQA final answers.

🤝 **Contributing**
We welcome contributions! You can:

Open issues for bugs, suggestions, or ideas.

Submit pull requests with improvements to retrieval, chunking, or generation logic.

**License:**
This project is licensed under the MIT License.

🧬 **Acknowledgements**
PubMedQA

Hugging Face Transformers

SentenceTransformers

LangChain

Cohere Rerank

