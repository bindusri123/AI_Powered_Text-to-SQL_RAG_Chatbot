# F1InsightAI

> **AI-Powered Formula 1 Text-to-SQL RAG Chatbot**  
> Ask Formula 1 questions in natural language and get accurate answers from structured database data.

---

## 📌 Project Overview

F1InsightAI is an intelligent chatbot designed to make Formula 1 data exploration simple for both technical and non-technical users.  
Instead of writing SQL queries manually, users can ask questions like:

- Who has the most race wins?
- Compare Hamilton and Verstappen.
- Show the 2023 race calendar.
- Average pit stop time by team.

The system retrieves the most relevant database schema using **RAG (Retrieval-Augmented Generation)**, generates SQL safely, executes it on the database, validates the result, and returns a human-friendly answer with charts, tables, SQL, and follow-up suggestions.

---

## ✨ Features

| Feature | Description |
|---|---|
| Natural language search | Ask Formula 1 questions in plain English. |
| Schema-aware RAG | Retrieves only relevant tables and columns before SQL generation. |
| LangGraph agent pipeline | Handles classification, retrieval, SQL generation, execution, reflection, retry, and response generation. |
| Multi-turn conversation | Uses chat history for follow-up questions and context. |
| Read-only execution | Prevents destructive database queries. |
| Auto-generated charts | Visualizes results using intelligent chart selection. |
| Interactive UI | Displays answer, SQL, table data, and agent steps in bento-style cards. |
| Conversation management | Supports rename, pin, delete, and persistent chat history. |
| Cloud deployment | Uses TiDB Cloud and Groq API for scalable performance. |

---

## 🧠 Project Idea

Formula 1 has decades of race data, driver statistics, constructor standings, lap times, pit stops, and qualifying results.  
This makes it a rich but complex dataset.

The main challenge is that users usually do not know SQL, and sending the entire database schema to an LLM wastes tokens and reduces accuracy.  
F1InsightAI solves this by combining:

1. **Schema retrieval with FAISS**
2. **SQL generation with an LLM**
3. **Agent-based reasoning with LangGraph**
4. **A polished frontend for interactive exploration**

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Backend | Flask (Python 3.11) | API handling and orchestration |
| Agent Framework | LangGraph | Multi-step intelligent workflow |
| LLM | Groq API with Llama 3.3 70B | Fast SQL and answer generation |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) | Schema and query embeddings |
| Vector Store | FAISS | Fast similarity search |
| Database | TiDB Cloud | MySQL-compatible database hosting |
| Frontend | HTML, CSS, JavaScript | Custom interactive interface |
| Charts | Chart.js | Result visualization |
| Deployment | Docker, Docker Compose | Portable deployment setup |

---

## 🗄️ Database Design

### Main F1 Tables

| Table | Description | Key Columns |
|---|---|---|
| circuits | Stores race circuit details | name, location, country |
| constructors | Stores Formula 1 teams | name, nationality |
| drivers | Stores driver profiles | forename, surname, nationality, dob |
| races | Stores every race from 1950–2024 | name, date, year, round, circuitId |
| results | Stores race results | position, points, laps, time, fastestLap |
| qualifying | Stores qualifying session data | position, q1, q2, q3 |
| driver_standings | Stores driver championship standings | points, position, wins |
| constructor_standings | Stores constructor championship standings | points, position, wins |
| lap_times | Stores lap-level timing data | lap, position, time, milliseconds |
| pit_stops | Stores pit stop records | stop, lap, duration, milliseconds |
| sprint_results | Stores sprint race results | position, points, laps |
| seasons | Stores season metadata | year, url |
| status | Stores result status codes | status |
| constructor_results | Stores team race results | points, status |

### Chat Storage Tables

| Table | Purpose |
|---|---|
| conversations | Stores conversation titles, pin status, and timestamps |
| messages | Stores user and assistant messages with metadata |

---

## 🏗️ System Architecture

| Component | Role |
|---|---|
| Frontend | Collects user input and renders charts, tables, SQL, and responses |
| Flask Backend | Handles API requests and orchestrates the workflow |
| LangGraph Agent | Controls the reasoning and execution steps |
| RAG Layer | Retrieves relevant schema context using embeddings and FAISS |
| LLM Layer | Generates SQL queries and natural language answers |
| TiDB Cloud | Stores the Formula 1 database and conversation data |

### Data Flow

| Step | Description |
|---|---|
| 1 | The user enters a Formula 1 question in the chat UI. |
| 2 | Flask receives the request through `/api/chat`. |
| 3 | LangGraph classifies the question. |
| 4 | RAG retrieves relevant schema tables. |
| 5 | The LLM generates SQL using only the retrieved schema. |
| 6 | SQL is executed on TiDB Cloud. |
| 7 | The result is reflected and validated. |
| 8 | The final answer is formatted and returned to the frontend. |
| 9 | The frontend displays the answer with charts, tables, and suggestions. |

---

## 🔍 RAG Pipeline

| Stage | Description |
|---|---|
| Schema extraction | Reads table metadata from the database at startup. |
| Document creation | Converts each table into a rich schema document. |
| Embedding generation | Uses all-MiniLM-L6-v2 to build embeddings. |
| FAISS indexing | Stores embeddings for fast similarity search. |
| Query embedding | Converts the user question into the same vector space. |
| Retrieval | Finds the most relevant tables. |
| Context enrichment | Adds related tables using co-occurrence rules. |
| Prompt augmentation | Injects schema context into the LLM prompt. |
| SQL generation | Produces SQL with relevant schema only. |

### Why RAG Is Important

| Benefit | Impact |
|---|---|
| Less token usage | The full schema is not passed every time. |
| Better accuracy | The model focuses on the right tables. |
| Fewer hallucinations | Reduces invented table or column names. |
| Easy scaling | New tables can be added without retraining. |

---

## 🤖 LangGraph Agent Flow

| Node | Purpose |
|---|---|
| classify | Detects whether the question needs SQL or a direct reply. |
| direct_answer | Handles general conversational questions. |
| retrieve_schema | Retrieves schema context using RAG. |
| generate_sql | Creates SQL based on the schema and question. |
| execute_sql | Runs the SQL safely on TiDB Cloud. |
| reflect | Checks whether the result is valid. |
| retry_sql | Fixes SQL errors and tries again. |
| generate_answer | Converts SQL results into readable language. |
| generate_follow_ups | Suggests related follow-up questions. |

### Routing Logic

| Condition | Action |
|---|---|
| Conversational question | Go to `direct_answer` |
| Database question | Go to `retrieve_schema` |
| SQL execution failure | Go to `retry_sql` |
| Successful execution | Go to `generate_answer` |

---

## 🎨 Frontend Experience

| Section | Description |
|---|---|
| Hero Search Bar | Centered input that becomes a bottom dock after results appear. |
| Bento Grid | Displays answer, chart, SQL, agent steps, and follow-up suggestions. |
| Glassmorphism Cards | Frosted-glass style modern UI. |
| Animated Background | Particle effects and spotlight visuals. |
| SQL Viewer | Syntax-highlighted SQL with copy support. |
| Chart Panel | Automatically renders bar, pie, or line charts. |
| Chat History | Rename, pin, delete, and manage conversations. |

### Visual Effects

| Effect | Purpose |
|---|---|
| Mouse-following spotlight | Adds an immersive high-tech feel. |
| Telemetry grid overlay | Creates an F1 cockpit look. |
| Rotating conic border | Gives the input a premium glowing effect. |
| 3D card tilt | Adds interactivity to result cards. |
| Animated title | Improves visual polish. |
| Particle network | Creates a dynamic Formula 1 atmosphere. |

---

## 📊 Example Queries

| User Query | Expected Output |
|---|---|
| Who has the most race wins? | Top drivers with counts and chart |
| Compare Hamilton and Verstappen | Side-by-side comparison |
| Show the 2023 race calendar | Race list with circuits and dates |
| Average pit stop duration by team | Aggregated team-wise pit stop analysis |
| What is DRS? | Direct conversational answer |

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Serves the chat UI |
| POST | `/api/chat` | Sends a question and returns answer, SQL, and results |
| GET | `/api/health` | Checks database, RAG, and LLM status |
| GET | `/api/stats` | Returns database statistics |
| GET | `/api/tables` | Lists available tables |
| GET | `/api/conversations` | Lists all conversations |
| POST | `/api/conversations` | Creates a new conversation |
| DELETE | `/api/conversations/<id>` | Deletes a conversation |
| PATCH | `/api/conversations/<id>/rename` | Renames a conversation |
| PATCH | `/api/conversations/<id>/pin` | Pins or unpins a conversation |

---

## ✅ Testing Results

| Metric | Value |
|---|---|
| Total queries tested | 20 |
| SQL accuracy on first attempt | 83.3% |
| Average response time | 21.66 seconds |
| Minimum response time | 5.97 seconds |
| Maximum response time | 48.20 seconds |
| Database size | 16 tables, 701,530 rows |

### Category Performance

| Category | Result |
|---|---|
| Driver stats | Excellent |
| Race queries | Strong, with minor naming edge cases |
| Circuit queries | Accurate when names matched well |
| Pit stop queries | Good aggregation support |
| Lap time queries | Good performance |
| Conversational queries | Correctly handled without SQL |

---

## ⚠️ Challenges and Fixes

| Challenge | Cause | Fix |
|---|---|---|
| Connection timeouts | TiDB Cloud dropped idle pooled connections | Added fresh connection fallback |
| Old chat parsing errors | Frontend tried to parse plain text as JSON | Fixed message loading logic |
| Spa queries returned no rows | Exact matching missed official circuit names | Used flexible LIKE matching |
| Brazilian GP mismatch | Race renamed to São Paulo Grand Prix | Added domain knowledge to prompt |
| Unreadable charts | Same color palette used for all series | Added distinct colors and filtered ID columns |
| Chart layout issue | Cards shared the same grid space | Separated chart and reasoning cards |
| Pin toggle bug | State update logic was incorrect | Read current state before updating |
| Rename input issue | Parent click handler intercepted clicks | Added event propagation control |

---

## 🚧 Limitations

| Limitation | Details |
|---|---|
| API rate limits | Groq free tier has token limits. |
| LLM variability | Answers may vary slightly between runs. |
| FAISS persistence | The vector index is rebuilt at startup. |
| Edge cases | Some renamed or accented F1 terms still need prompt tuning. |

---

## 🔮 Future Scope

| Improvement | Benefit |
|---|---|
| Persist FAISS index | Faster startup and better reuse |
| Add caching | Lower latency for repeated queries |
| Improve domain knowledge | Better handling of renamed races and circuits |
| Expand charts | Richer visual analytics |
| Add export options | Save results as CSV or PDF |
| Support more domains | Reuse the same architecture for other sports datasets |

---

## 🏁 Conclusion

F1InsightAI shows how Retrieval-Augmented Generation and agentic workflows can make complex relational databases accessible through plain English.  
It combines accurate SQL generation, automatic validation, conversation memory, and visual analytics into one Formula 1 assistant.

---

## 👨‍🎓 Credits

| Role | Name |
|---|---|
| Student | Venkateswara Sahu (12204893) |
| Supervisor | Mr. Madhav Dubey (UID: 65167) |
| Institution | Lovely Professional University, Phagwara, Punjab |

---

## 🏷️ Tags

`formula-1` `text-to-sql` `rag` `langgraph` `flask` `faiss` `groq` `tidb` `chatbot` `ai`
