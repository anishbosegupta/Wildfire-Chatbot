# Wildfire AI Assistant
An intelligent, multi-modal chatbot designed to provide real-time wildfire risk assessment, safety guidance, and general information using RAG (Retrieval-Augmented Generation) and machine learning. This assistant enhances community preparedness by empowering residents with tailored safety measures and supporting first responders during emergencies.

🚀 Features
1. Smart Intent Classification
Uses a zero-shot classifier (facebook/bart-large-mnli) to determine the user's intent, distinguishing between general inquiries and specific location-based risk predictions.
2. Retrieval-Augmented Generation (RAG)
   * Context-Aware Answers: Delivers informed answers on topics like defensible space, prescribed burns, and emergency supplies using a vector database.
   * Data Sources: Populated with wildfire data from FEMA’s Wildland-Urban Interface Fire program, the New Jersey Wildfire Risk Assessment Portal, and other official safety documents.
   * Tech Stack: LangChain for conversation management, FAISS (Facebook AI Similarity Search) for efficient vector search, and Mistral-7B-Instruct hosted via Hugging Face.
3. Area-Specific Risk Prediction
When a user mentions a location, the system performs a multi-step analysis:

   * NER (Named Entity Recognition): Extracts location names from text.
   * Real-Time Data Integration: Integrates meteorological data from NOAA and active alerts from the weather.gov API.
   * NASA FIRMS Integration: Checks for NRT (Near Real-Time) satellite thermal anomalies (active fire points) within a 20-mile radius.
   * Custom ML Model: While Logistic Regression and Gradient Boosting were considered, the system utilizes a fine-tuned Gradient Boosting Classification model to predict risk levels.
4. Interactive Streamlit UI
A web-based conversational interface built with Python and Streamlit, maintaining session history and presenting data through intuitive tables and markdown.

🛠️ Project Structure
   * app.py: The main Streamlit application hub.
   * RAG_LLM.py: Document ingestion and LangChain QA logic.
   * custom_model_weather_classification.py: Training and prediction logic for the Gradient Boosting model.
   * thermal_anomaly.py: NASA FIRMS API integration and distance calculations.
   * weather_data.py & weather_api_alerts.py: Interfaces for meteorological and alert data.

⚖️ Ethical AI & Principles
The system is developed with a commitment to human-centered AI principles and ethical AI design, ensuring that safety information is grounded in verified context and designed to assist rather than replace emergency services.

🔧 Setup & Requirements

Environment Variables

The app expects the following keys in the Google Colab Userdata:

  * token1studio: Your Hugging Face Hub token.
  * NASAfirms: Your NASA FIRMS API key.
  * ngrok_auth: Your Ngrok authentication token.

📖 How to Run
1. Install dependencies listed in the notebook.
2. Execute all module cells to generate the required .py files.
3. Run the Streamlit execution cell to launch the public interface via Ngrok.


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
