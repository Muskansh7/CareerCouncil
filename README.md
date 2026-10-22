# 🎯 Career Council — AI Placement Advisor Platform

An AI-powered career guidance platform designed to help students prepare for placements, improve technical skills, practice interviews, optimize resumes, and make informed career decisions.

Career Council combines a **React + Vite frontend** with a **FastAPI backend**, powered by **LangChain, LangGraph, Gemini, and OpenAI**. It offers specialized AI advisors and a collaborative AI Council that brings multiple perspectives together to provide practical recommendations.

## ✨ Features

- 🤖 **Multiple AI Advisors** — Get specialized guidance based on your needs.
- 👥 **AI Council Mode** — Bring multiple advisors together for a consolidated recommendation.
- 🎯 **Single Advisor Mode** — Receive focused guidance from one selected advisor.
- 🛠️ **Custom Advisor** — Create a personalized advisor using custom instructions.
- 🔄 **Multiple LLM Providers** — Switch between supported Google Gemini and OpenAI models.
- 🌐 **Web Search Integration** — Use Tavily search for questions that require current information.
- 💻 **Coding & DSA Guidance** — Learn programming, algorithms, debugging, and system design.
- 📄 **Resume & Career Guidance** — Get resume feedback, placement strategies, and career roadmaps.
- 🎤 **Interview Preparation** — Practice technical interviews and receive structured feedback.
- 🔬 **Research Assistance** — Explore technical concepts, compare technologies, and understand research.
- 💰 **Financial Guidance** — Learn about budgeting, saving, investing concepts, and financial planning.
- ⚡ **FastAPI Backend** — Handle requests through a structured REST API.
- ⚛️ **Modern Frontend** — Built using React and Vite.

## 🧑‍🏫 Available AI Advisors

| Advisor | Purpose |
|---|---|
| Coding Mentor | Programming, DSA, algorithms, debugging, and system design |
| Career Coach | Resume reviews, ATS feedback, internships, and placement strategy |
| Interview Coach | Technical interview practice, answer evaluation, and improvement plans |
| Research Assistant | Technical research, technology comparisons, and learning resources |
| Financial Advisor | Budgeting, savings, investment concepts, and financial planning |
| Friend | Friendly conversations, motivation, and placement preparation support |
| Custom Advisor | Personalized guidance using custom instructions |

## 🛠️ Tech Stack

**Frontend**
- React
- Vite
- JavaScript
- Axios

**Backend**
- Python
- FastAPI
- Pydantic
- Uvicorn

**AI & Agent Frameworks**
- LangChain
- LangGraph
- Google Gemini
- OpenAI

**Tools & Integrations**
- Tavily Search
- Python dotenv
- REST API

## 🏗️ System Architecture

```text
              React + Vite Frontend
                       |
                       | HTTP Request
                       v
                FastAPI Backend
                       |
              Request Validation
                       |
             Advisor Selection Logic
                       |
             +---------+---------+
             |                   |
             v                   v
       Single Advisor         AI Council
             |                   |
             +---------+---------+
                       |
                       v
              LangGraph ReAct Agent
                       |
             +---------+---------+
             |                   |
             v                   v
       Gemini / OpenAI       Tavily Search
             |                   |
             +---------+---------+
                       |
                       v
             Structured AI Response
                       |
                       v
              React + Vite UI
```

## ⚙️ How It Works

### 1. Single Advisor Mode

Users select an advisor, choose a supported AI model, and submit a question. The backend loads the corresponding advisor instructions and generates a response using the configured language model.

### 2. AI Council Mode

Users select multiple advisors. Career Council combines their instructions into a shared council prompt, allowing the AI agent to generate a consolidated response with a practical recommendation.

### 3. Custom Advisor

Users can provide custom instructions to define an advisor for a particular task or area of expertise.

### 4. Web Search

When enabled, the Tavily search tool can help the agent retrieve information for questions that require current or external information.

## 📂 Project Structure

```text
Career-Council/
├── frontend/                 # React + Vite frontend
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.js
│
├── backend/                  # FastAPI backend
│   ├── backend.py
│   ├── ai_agent.py
│   ├── advisor_prompts.py
│   ├── response_format.py
│   └── requirements.txt
│
├── .env.example
├── .gitignore
└── README.md
```

*Note: Adjust the folder tree above if your actual repository uses different paths or filenames.*

## 🚀 Getting Started

### Prerequisites

Make sure you have installed:

- Python
- Node.js and npm
- A Google Gemini or OpenAI API key
- A Tavily API key if you want to use web search

### 1. Clone the Repository

```bash
git clone https:https://github.com/Muskansh7
```

Replace the placeholders with your actual GitHub username and repository name.

### 2. Set Up the Backend

Create a Python virtual environment:

**Windows**

```bash
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux**

```bash
python3 -m venv venv
source venv/bin/activate
```

Install the backend dependencies:

```bash
pip install -r backend/requirements.txt
```

If your `requirements.txt` is located elsewhere, adjust the path accordingly.

### 3. Configure Environment Variables

Create a `.env` file in the location where your backend loads environment variables.

```env
GOOGLE_API_KEY=your_google_api_key
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

Add only the credentials required by your configuration.

**Security:** Never commit your `.env` file or publish real API keys on GitHub. Keep `.env` in `.gitignore`. If a key has been exposed, revoke or rotate it.

### 4. Start the FastAPI Backend

If your backend files are inside the `backend/` directory and the FastAPI application is defined as `app` in `backend.py`, run:

```bash
cd backend
uvicorn backend:app --reload
```

The API will generally be available at:

`http://127.0.0.1:8000`

Interactive API documentation:

`http://127.0.0.1:8000/docs`

If your actual module filename or directory layout differs, update the Uvicorn command accordingly.

### 5. Start the React + Vite Frontend

Open a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL displayed in the terminal, commonly:

`http://localhost:5173`

Ensure the frontend is configured to send requests to your running FastAPI backend.

## 🔌 API Reference

### `POST /chat`

Career Council exposes a `/chat` endpoint for interacting with the AI advisors.

**Example request**

```json
{
  "model_name": "gpt-4o",
  "model_provider": "openai",
  "mode": "single",
  "advisor": "Career Coach",
  "advisors": [],
  "custom_prompt": "",
  "messages": [
    "How can I improve my placement preparation?"
  ],
  "allow_search": true
}
```

**Request parameters**

| Parameter | Description |
|---|---|
| `model_name` | Selected language model |
| `model_provider` | `gemini` or `openai` |
| `mode` | `single` or `council` |
| `advisor` | Selected advisor in single mode |
| `advisors` | Selected advisors in council mode |
| `custom_prompt` | Instructions for a custom advisor |
| `messages` | Conversation messages; the backend uses the last item as the current query |
| `allow_search` | Enables or disables Tavily search |

**Example response**

```json
{
  "status": "success",
  "mode": "single",
  "advisor": "Career Coach",
  "provider": "openai",
  "model": "gpt-4o",
  "search_enabled": true,
  "response": "Your AI advisor response appears here."
}
```

The application validates the selected model provider, model, mode, and advisor inputs before generating a response.

## 🖼️ Screenshots

<img width="1908" height="927" alt="image" src="https://github.com/user-attachments/assets/bc83f0f7-d0e0-4cea-8cb5-706730869d0b" />

<img width="1917" height="913" alt="image" src="https://github.com/user-attachments/assets/799700be-89bb-45d2-9f8e-7d4794c43421" />



## 🌍 Deployment

The application can be deployed using separate frontend and backend services.

- **Frontend:** Build and deploy the React + Vite application to a static hosting provider.
- **Backend:** Deploy the FastAPI application to a Python-compatible hosting provider.
- **CORS:** Configure the backend to allow requests from your deployed frontend URL.
- **Environment Variables:** Add API credentials through your hosting provider's secrets manager.
- **API Configuration:** Update the frontend's API URL to point to the deployed backend.

Ensure that the backend is accessible and the configured frontend origin is allowed by FastAPI's CORS middleware.

## 🔐 Security Best Practices

- Keep API keys out of source code.
- Never commit `.env` files.
- Store backend credentials in environment variables.
- Never expose private API keys in React/Vite client-side variables.
- Configure CORS for trusted frontend origins in production.
- Avoid logging sensitive information in production.

## 🚧 Future Enhancements

Potential improvements for future versions include:

- Persistent conversation history
- User authentication and personalized profiles
- Resume upload and detailed analysis workflows
- Career roadmap generation
- More advisor specializations
- Improved conversation memory
- Usage tracking and response feedback

## 👩‍💻 Author

**Muskan Sharma**

---

⭐ If you find Career Council useful, consider starring the repository!

*Career Council — Your AI-powered companion for smarter career decisions and placement preparation.*
