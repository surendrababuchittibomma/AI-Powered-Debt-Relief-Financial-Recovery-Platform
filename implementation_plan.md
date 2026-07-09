# Implementation Plan: FinRelief AI Full-Stack Application

This implementation plan details the setup, development, and integration of the **FinRelief AI** platform, an AI-powered debt relief and financial recovery tool.

The database schema aligns exactly with the 5-entity model designed in [er_diagram_analysis.md](file:///C:/Users/LENOVO/.gemini/antigravity/brain/796a8454-722f-4c18-a920-e35089d8fbc8/er_diagram_analysis.md).

---

## Workspace Recommendation

We will initialize the project in the following subdirectory:
`C:\Users\LENOVO\.gemini\antigravity\scratch\finrelief-ai`

> [!TIP]
> We recommend setting `C:\Users\LENOVO\.gemini\antigravity\scratch\finrelief-ai` as your active workspace in the IDE once setup begins.

---

## Proposed Project Directory Structure

We will organize the project as a clean monorepo:

```text
finrelief-ai/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                # FastAPI app initialization & routing
│   │   ├── config.py              # Configuration & env variables
│   │   ├── database.py            # SQLite session and engine setup
│   │   ├── models.py              # SQLAlchemy database models (5 Entities)
│   │   ├── schemas.py             # Pydantic data validation schemas
│   │   ├── crud.py                # CRUD queries for Users, Loans, Profiles, etc.
│   │   ├── engine/
│   │   │   ├── __init__.py
│   │   │   ├── financial.py       # Financial health & metrics calculator
│   │   │   ├── prediction.py      # Settlement probability/amount logic
│   │   │   └── advisor.py         # AI negotiation strategy and letter generation
│   │   └── security.py            # Password hashing & JWT helper utilities
│   ├── tests/
│   │   ├── __init__.py
│   │   └── test_engine.py         # Pytest for core modules
│   ├── requirements.txt           # Python dependency declarations
│   └── .env                       # Local configurations
├── frontend/
│   ├── src/
│   │   ├── components/            # UI components (Layout, Cards, Alerts)
│   │   ├── views/                 # View pages (Login, Dashboard, Profile, AI-Advisor)
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css              # Custom styling definitions
│   ├── package.json
│   └── vite.config.js
└── README.md
```

---

## Detailed Step-by-Step Execution Plan

### Phase 1: Environment & Project Setup (Epic 1)
1. Create the `finrelief-ai` workspace directory, creating `backend/` and `frontend/` folders.
2. Initialize the Python virtual environment in `backend/` and install required dependencies.
3. Scaffold the frontend application using `vite` with React in the `frontend/` directory.

### Phase 2: Database Schema & Core Models (Epic 3)
1. Write `backend/app/database.py` using SQLAlchemy with SQLite (local file database).
2. Define the 5 SQLAlchemy models in `backend/app/models.py` matching our approved ER design:
   - `User` (`user_id`, `name`, `email`, `password`, `created_at`)
   - `Loan` (`loan_id`, `user_id`, `loan_type`, `loan_amount`, `outstanding_amount`, `interest_rate`, `due_date`)
   - `FinancialProfile` (`profile_id`, `user_id`, `monthly_income`, `monthly_expenses`, `existing_debts`, `financial_health_score`)
   - `SettlementRecord` (`settlement_id`, `user_id`, `loan_id`, `settlement_prediction`, `recommended_amount`, `priority_level`, `created_at`)
   - `AIHistory` (`history_id`, `user_id`, `negotiation_strategy`, `settlement_letter`, `ai_response`, `generated_at`)
3. Write `backend/app/schemas.py` using Pydantic for validation.
4. Implement data read/write interfaces in `backend/app/crud.py`.

### Phase 3: AI Integration & Financial Engine (Epic 2)
1. **Financial Engine (`app/engine/financial.py`)**: Computes debt-to-income (DTI) ratio and calculates a `financial_health_score` (0-100) based on income, expenses, and liabilities.
2. **Settlement Predictor (`app/engine/prediction.py`)**: Uses rules to estimate settlement likelihood (e.g. comparing debt age, interest rates, and financial score) and calculates a `recommended_amount` (payoff target, e.g. 40-60% of outstanding balance).
3. **AI Advisor (`app/engine/advisor.py`)**: Generates negotiation strategies and custom settlement letters. Integrates an LLM helper (mocked by default with template fallback if no OpenAI/Gemini API key is configured).
4. **FastAPI Endpoints (`app/main.py`)**: Exposes REST interfaces:
   - `/api/auth/register` & `/api/auth/login` (JWT-based token issuance)
   - `/api/profile` (CRUD financial profile, triggers recalculation)
   - `/api/loans` (CRUD for managing user loans)
   - `/api/settlements` (Evaluates and retrieves prediction history)
   - `/api/negotiate` (Triggers AI negotiation strategy & letter generation)

### Phase 4: Frontend Development & Integration (Epic 4)
1. Construct a premium dark-themed UI system in `frontend/src/index.css` using modern gradients and subtle borders.
2. Create views:
   - **Auth Screen**: Clean login/register portal.
   - **Dashboard**: High-level financial overview containing:
     - Metrics display (Monthly Income, Monthly Expenses, Total Debt).
     - Financial Health progress gauge.
     - Charts showing income vs expense split and debt distribution by loan type.
   - **Loans Manager**: Add and manage outstanding loans.
   - **AI Negotiation Center**: A clean workspace to run evaluations, view predicted payoffs, read the AI-generated strategy, and copy/download the custom settlement letter.
3. Configure Axios calls to integrate with FastAPI.

### Phase 5: Optimization & Finalization (Epics 5 & 6)
1. Add custom backend exception handlers for invalid API inputs and token validation failures.
2. Draft a suite of automated unit tests in `backend/tests/` to verify calculations.
3. Prepare production readiness config (Vite production builds and Uvicorn deployment steps).

---

## Verification Plan

### Automated Tests
- Run `pytest` inside the backend virtual environment to check:
  - Financial health score calculation correctness.
  - Settlement predictor outcomes.
  - JWT creation and authentication lifecycle.

### Manual Verification
- Launch the FastAPI development server and Vite dev server.
- Walk through user registration, creating a financial profile, adding two different loans, triggering an AI settlement assessment, and verifying that the negotiation letter renders correctly.
