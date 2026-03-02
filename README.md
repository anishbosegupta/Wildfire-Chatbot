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
