# AI_Powered_Text-to-SQL_RAG_Chatbot
F1InsightAI is an AI-powered Formula 1 Text-to-SQL chatbot built using Flask, LangGraph, RAG, FAISS, and Groq LLMs. It converts natural language questions into SQL queries, retrieves relevant F1 data, and presents interactive visual insights with charts, tables, and a cinematic UI experience.
🚀 F1InsightAI — AI-Powered Formula 1 Text-to-SQL RAG Chatbot

F1InsightAI is an AI-powered chatbot that allows users to explore Formula 1 data using natural language instead of writing SQL queries manually. The system converts user questions into optimized SQL queries using a Retrieval-Augmented Generation (RAG) pipeline and a LangGraph-based multi-agent workflow.

The project combines Large Language Models (LLMs), vector search, Text-to-SQL generation, and interactive data visualization to create a cinematic Formula 1 analytics experience.

✨ Features
🔍 Natural Language to SQL conversion
🧠 RAG-based schema retrieval using FAISS
🤖 LangGraph multi-agent pipeline
⚡ Groq + Llama 3.3 70B integration
📊 Auto-generated charts and tables
💬 Multi-turn conversation support
🎨 Cinematic F1-inspired UI
📁 Conversation history management
🔄 Automatic SQL retry & correction
🛡️ Read-only SQL enforcement
🛠️ Tech Stack
Backend
Flask (Python)
LangGraph
LangChain
MySQL / TiDB Cloud
AI & RAG
Groq API
Llama 3.3 70B
Sentence Transformers
FAISS Vector Store
Frontend
HTML
CSS
JavaScript
Chart.js
tsParticles
📂 Project Structure
Project/
├── app.py
├── config.py
├── requirements.txt
├── agent/
├── database/
├── rag/
├── llm/
├── templates/
├── static/
├── Dockerfile
└── docker-compose.yml
⚙️ Installation
Clone Repository
git clone <your-repo-link>
cd F1InsightAI
Create Virtual Environment
python -m venv venv
Activate Environment
venv\Scripts\activate
Install Dependencies
pip install -r requirements.txt
🔑 Environment Variables

Create a .env file:

MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=your_password
MYSQL_DATABASE=f1db
MYSQL_SSL=false

GROQ_API_KEY=your_groq_api_key
GROQ_MODEL=llama-3.3-70b-versatile

FLASK_SECRET_KEY=abc123
FLASK_DEBUG=True
▶️ Run the Project
python app.py

Open in browser:

http://127.0.0.1:5000
📊 Database

The system uses a Formula 1 database containing:

Drivers
Constructors
Circuits
Race Results
Pit Stops
Lap Times
Qualifying Data
Championship Standings
🧠 Architecture

The system follows a 9-node LangGraph pipeline:

Intent Classification
Schema Retrieval (RAG)
SQL Generation
SQL Execution
Reflection & Validation
Retry Mechanism
Answer Generation
Follow-up Suggestions
Response Rendering
📸 Sample Queries
“Who has the most race wins?”
“Compare Hamilton vs Verstappen”
“Show 2023 race calendar”
“Average pit stop duration by team”
“Schumacher wins at Spa”
🚀 Future Improvements
Persistent FAISS indexing
Voice input support
Advanced data visualizations
Authentication system
Query caching
PDF report export
👨‍💻 Author

Developed as a B.Tech CSE (Hons.) project focused on AI-powered Text-to-SQL systems, RAG pipelines, and Formula 1 analytics.
