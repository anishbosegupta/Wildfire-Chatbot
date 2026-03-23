📊 Model Evaluation (Wildfire_Model_Evaluation.ipynb)

**What it does:**
Evaluates RAG (Retrieval-Augmented Generation) model outputs using three complementary evaluation metrics:
- **ROUGE-L** - Measures longest common subsequence overlap between predictions and references
- **BERTScore** - Measures semantic similarity using contextual embeddings (F1 scores)
- **LLM-as-Judge** - Uses Llama-2-7B model to provide expert evaluation scores (1-5 scale)

**How to Run:**
1. Ensure dependencies are installed (see below)
2. Prepare a CSV file (qa_judge_inputs.csv) with columns: context, question, prediction, reference
3. For LLM-as-Judge evaluation:
   - Login to Hugging Face: `huggingface-cli login`
   - Configure git credentials: `git config --global credential.helper store`
   - Note: Requires GPU (Colab T4 GPU recommended)
4. Execute all cells in the notebook to generate evaluation metrics and visualizations

**Dependencies:**
- evaluate==0.4.0
- rouge_score
- bert_score
- transformers
- pandas
- matplotlib
- bitsandbytes==0.39.1
- torch (GPU support required for LLM-as-Judge)

**Project Workflow Integration:**
The notebook fits into the **validation and quality assurance phase** of the pipeline. It runs **after** the main RAG system and custom ML model have generated predictions. It helps identify model performance bottlenecks and areas for improvement, with outputs including comparison metrics and visualizations to guide model optimization.
