# 🧠 AI Crew Generator using Gemini + FastAPI

This project is a **multi-agent AI system** that dynamically generates and runs specialized AI agents using **Google Gemini**, **MongoDB**, and **FastAPI**. The agents collaborate to respond to user prompts, and similar past prompts are reused using vector similarity search.
<img width="758" height="386" alt="image" src="https://github.com/user-attachments/assets/62d3e591-5401-4343-ba2d-a6e0ee9abfde" />


## 🚀 Features

- 🔍 **Prompt similarity search** using MongoDB Atlas Vector Search
- 🧠 **Agent generation** using Gemini (Google Generative AI)
- 📄 **Auto YAML generation** for agents and tasks
- 🤖 **Crew AI agent orchestration** using [CrewAI](https://docs.crewai.com/)
- 🧪 Built with **FastAPI** for easy deployment and testing
- 🗃️ **MongoDB integration** for prompt persistence and vector search

## 📂 Project Structure

```
.
├── main.py               # FastAPI server with endpoints
├── db.py                 # MongoDB logic for saving/fetching prompts
├── gemini_client.py      # Connects to Gemini and generates agents
├── crew_generator.py     # Generates YAML for agents and tasks
├── crew_runner.py        # Loads and runs AI agents as a crew
├── .env                  # API keys and MongoDB URI
└── data/crews/           # Auto-generated folders for each crew
```

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-crew-generator.git
cd ai-crew-generator
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Up Environment Variables

Create a `.env` file:

```env
GEMINI_API_KEY=your_gemini_api_key
MONGODB_URI=your_mongodb_uri
OPENAI_API_KEY=dummy
```

## ▶️ Running the App

Start the FastAPI server:

```bash
uvicorn main:app --reload
```

Access docs at: [http://localhost:8000/docs](http://localhost:8000/docs)

## 📡 API Endpoints

### POST `/generate_agents`

Generate a new crew or reuse an existing one.

**Request Body:**

```json
{
  "prompt": "Build a web scraper for e-commerce websites"
}
```

**Response:**

```json
{
  "crew_id": "1234-uuid",
  "status": "new",
  "output": "Final agent response..."
}
```

### GET `/agents/{crew_id}`

Retrieve the `agents.yaml` file content for a specific crew.

### DELETE `/agents/{crew_id}`

Delete a crew from both file storage and MongoDB.

## 🧠 How It Works

1. Takes a user prompt.
2. Searches MongoDB for similar prompts using vector embeddings.
3. If similar prompt is found, reuses the crew and runs it.
4. If not, calls Gemini to generate agents in YAML format.
5. Stores the new crew data and runs the task using CrewAI.

## 🛡️ Notes

- Ensure MongoDB Atlas has vector search enabled.
- Your Gemini API key must support `gemini-2.0-flash`.
- Agents and tasks are stored as YAML in `data/crews/{crew_id}/`.

## 📜 License

MIT License
