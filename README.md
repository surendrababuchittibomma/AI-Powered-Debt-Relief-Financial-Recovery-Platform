# FinRelief AI - Full-Stack Debt Relief & Financial Recovery Platform

FinRelief AI is an AI-powered financial advisory system designed to help users evaluate liabilities, predict debt settlement outcomes, analyze financial health metrics, and generate customized negotiation strategies and legal settlement proposal letters.

---

## Technical Stack

*   **Backend**: Python 3.8+, FastAPI, SQLAlchemy (SQLite engine), Pydantic, Pytest, Python-Jose (JWT), Passlib (Bcrypt).
*   **Frontend**: React.js, Vite, Recharts (visualizations), Lucide React (icons), Axios, Custom Glassmorphic HSL styling.

---

## Getting Started

### 1. Backend Setup & Run

Navigate to the `backend` folder:
```bash
cd backend
```

Create a virtual environment and activate it:
```bash
python -m venv venv
# On Windows (PowerShell):
.\venv\Scripts\Activate.ps1
# On macOS/Linux:
source venv/bin/activate
```

Install requirements:
```bash
pip install -r requirements.txt
```

Launch the FastAPI development server:
```bash
uvicorn app.main:app --reload
```
*The API will be available at `http://localhost:8000`. You can inspect the interactive OpenAPI documentation at `http://localhost:8000/docs`.*

### 2. Run Backend Unit Tests

Ensure the virtual environment is active, then run:
```bash
pytest
```

---

### 3. Frontend Setup & Run

Navigate to the `frontend` folder:
```bash
cd ../frontend
```

Install packages:
```bash
npm install
```

Launch the Vite local development server:
```bash
npm run dev
```
*The React user interface will be hosted at `http://localhost:5173`.*

---

## Key Features

1.  **Identity & Authentication**: Secure registration and login using JWT session tokens.
2.  **Financial Profile Assessment**: Evaluates monthly income and living expenses to calculate a dynamic Financial Health Score (0-100).
3.  **Loan Manager**: Add, list, and delete outstanding loans.
4.  **AI Settlement Predictor**: Estimates creditor settlement probability, recommended target payoff sum (e.g. 40-70% discount), and priority urgency.
5.  **AI Negotiation & Letter Builder**: Generates step-by-step negotiation strategies and automatically compiles formal hardship settlement letters with copy-to-clipboard functionality. Uses templates as a fallback in offline or unconfigured environments.
