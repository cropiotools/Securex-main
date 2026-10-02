# SecureX — AI-Powered Alternative Credit Intelligence

[![Live Demo](https://img.shields.io/badge/Demo-Live%20App-00C7B7?style=for-the-badge&logo=railway&logoColor=white)](https://securex.up.railway.app)
[![API Docs](https://img.shields.io/badge/API-Swagger%20Docs-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://securex-main-production.up.railway.app/docs)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/cropiotools/Securex-main)

> **Explainable AI for smarter, fairer, and more inclusive credit assessment.**

SecureX is a full-stack AI-powered credit intelligence platform that evaluates borrower creditworthiness by combining traditional credit indicators with alternative digital financial behaviour.

Instead of relying solely on conventional credit bureau records, SecureX incorporates **UPI transaction behaviour** and **bank statements** to compute dynamic credit scores, risk classifications, default probabilities, personalized loan recommendations, and transparent **SHAP Explainable AI** insights.

---

## 🔗 Live Deployments

| Service | Platform | URL | Status |
| :--- | :--- | :--- | :--- |
| **Frontend Web App** | Railway | [https://securex.up.railway.app](https://securex.up.railway.app) | 🟢 Live |
| **Backend FastAPI** | Railway | [https://securex-main-production.up.railway.app](https://securex-main-production.up.railway.app) | 🟢 Live |
| **Interactive API Docs** | Swagger / OpenAPI | [https://securex-main-production.up.railway.app/docs](https://securex-main-production.up.railway.app/docs) | 🟢 Live |

---

## ✨ Why SecureX?

Traditional credit scoring systems often penalize individuals with thin credit files or young borrowers. SecureX bridges this gap by evaluating:

- **Traditional Credit Indicators:** Revolving utilization, debt-to-income ratio, past-due delinquency buckets, open credit lines, real estate loans, dependents.
- **Digital Payment Behaviour (UPI):** Transaction frequency, total debit/credit flows, and credit-to-debit stability ratios.
- **Explainable Machine Learning:** Real-time SHAP (SHapley Additive exPlanations) values displaying exact positive and negative drivers of each credit decision.

---

## 🚀 Key Features

### 🤖 AI Credit Risk Prediction
A Random Forest Classifier trained on delinquency datasets predicts the probability of serious financial delinquency (`SeriousDlqin2yrs`).

### 📊 Dynamic Credit Score (300 – 850)
The base default probability is mapped to an industry-standard credit score (300 to 850) and dynamically adjusted using the **UPI Behaviour Score** (up to +50 points bonus/penalty adjustment).

### 💳 UPI Behavioural Analysis
Users upload a UPI transaction CSV to automatically extract:

| Metric | Description |
| :--- | :--- |
| **Transaction Count** | Total count of successful transactions |
| **Total Transaction Volume** | Cumulative transaction amount (₹) |
| **Average Ticket Size** | Average expenditure per transaction |
| **Total Credits vs Debits** | Inflows vs Outflows analysis |
| **Credit / Debit Ratio** | Cash flow sustainability index |
| **UPI Behaviour Score** | Algorithmic financial health score (0 – 50) |

### ⚠️ Risk Classification & Terms

| Credit Score | Risk Level | Est. Interest Rate |
| :--- | :--- | :--- |
| **740 – 850** | 🟢 Low Risk | 9.5% – 11.5% |
| **670 – 739** | 🟡 Medium Risk | 11.5% – 14.0% |
| **300 – 669** | 🔴 High Risk | 14.0% – 17.0% |

### 🧠 Explainable AI (SHAP)
SecureX breaks the "black box" by showing exact feature impacts for every prediction:
- 🔺 Factors increasing delinquency risk (e.g. high credit utilization, 30-59 days past due)
- 🔻 Factors decreasing delinquency risk (e.g. older age, steady income, balanced UPI debit/credit)

---

## 🏗️ System Architecture

```text
                    ┌─────────────────────────┐
                    │       User Input        │
                    │   Credit + UPI Data     │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │    Next.js Frontend     │
                    │   React 19 + TypeScript │
                    │     Tailwind CSS v4     │
                    └────────────┬────────────┘
                                 │
                           REST API Calls
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │     FastAPI Backend     │
                    │         Python          │
                    └────────────┬────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
                 ▼                               ▼
       ┌───────────────────┐           ┌───────────────────┐
       │  Credit ML Model  │           │  UPI Processing   │
       │   Random Forest   │           │   Pandas Engine   │
       └─────────┬─────────┘           └─────────┬─────────┘
                 │                               │
                 └───────────────┬───────────────┘
                                 ▼
                    ┌─────────────────────────┐
                    │   Combined Assessment   │
                    └────────────┬────────────┘
                                 │
               ┌─────────────────┼─────────────────┐
               ▼                 ▼                 ▼
          Credit Score      Risk Level        Loan Amount
               │
               ▼
        ┌──────────────────┐
        │  Explainable AI  │
        │ SHAP Values Tree │
        └──────────────────┘
```

---

## 📁 Project Structure

```text
Securex/
├── backend/
│   ├── app.py                # FastAPI server, endpoints & ML inference
│   ├── cs-training.csv       # Delinquency training dataset
│   ├── imputer.pkl           # Pretrained SimpleImputer model
│   ├── Procfile              # Railway deployment start command
│   ├── requirements.txt      # Python dependencies
│   ├── train_model.py        # Model training and export script
│   └── utils.py              # Helper functions
│
├── frontend/
│   ├── app/
│   │   ├── admin/            # Underwriting portal for loan officers
│   │   ├── api/
│   │   │   └── predict/      # Fallback Next.js API scoring route
│   │   ├── assessment/       # Credit & UPI document upload form
│   │   ├── dashboard/        # Borrower analytics dashboard
│   │   ├── profile/          # User profile and linked accounts
│   │   ├── results/          # Full credit assessment & XAI report
│   │   ├── globals.css       # Tailwind CSS & theme tokens
│   │   ├── layout.tsx        # Global layout & metadata
│   │   └── page.tsx          # Landing page
│   ├── components/
│   │   ├── assessment/
│   │   │   └── UploadCard.tsx
│   │   ├── ui/               # Reusable UI primitives (Button, Card, etc.)
│   │   ├── credit-score-gauge.tsx
│   │   ├── dashboard-stats.tsx
│   │   ├── glass-card.tsx
│   │   ├── gradient-button.tsx
│   │   └── navbar.tsx
│   ├── lib/
│   │   ├── mock-data.ts
│   │   └── utils.ts
│   ├── public/               # Logos, icons and static assets
│   ├── package.json          # Node dependencies and scripts
│   └── tsconfig.json         # TypeScript configuration
│
├── .gitignore                # Production ignore rules
└── README.md                 # Project documentation
```

> **Note on Model Storage:** The primary trained model weights (`credit_model.pkl`) are hosted on Hugging Face and automatically fetched on container startup to stay within Git file-size limits.

---

## 🔌 API Endpoints

### 1. `POST /upload`
Accepts financial documents (Bank Statement PDF and UPI transaction CSV) and extracts transaction metrics.

**Sample Response:**
```json
{
  "message": "Financial data extracted successfully",
  "bank_statement": {
    "filename": "bank_statement.pdf",
    "size": 104230
  },
  "upi_features": {
    "transaction_count": 9,
    "total_transaction_amount": 33849.0,
    "average_transaction_amount": 3761.0,
    "total_debit": 23349.0,
    "total_credit": 10500.0,
    "credit_debit_ratio": 2.22,
    "upi_behaviour_score": 40
  }
}
```

### 2. `POST /predict`
Processes applicant credit factors and computed UPI behaviour score to generate full assessment.

**Sample Request:**
```json
{
  "revolvingUtilization": 0.25,
  "age": 30,
  "late30to59": 0,
  "debtRatio": 0.35,
  "monthlyIncome": 50000,
  "openCreditLines": 8,
  "late90": 0,
  "realEstateLoans": 1,
  "late60to89": 0,
  "dependents": 2,
  "upiBehaviourScore": 40
}
```

**Sample Response:**
```json
{
  "score": 752,
  "risk": "Low Risk",
  "confidence": 91.24,
  "recommendation": 400000,
  "interest_rate": 9.5,
  "default_probability": 0.0482,
  "model_prediction": 0,
  "feature_importance": [
    { "feature": "Credit Utilization", "importance": 0.2451 },
    { "feature": "Debt Ratio", "importance": 0.1873 }
  ],
  "shap_explanation": [
    { "feature": "Credit Utilization", "impact": -0.0421 },
    { "feature": "Monthly Income", "impact": -0.0315 }
  ]
}
```

---

## 🛠️ Technology Stack

- **Frontend:** Next.js 16 (App Router), React 19, TypeScript, Tailwind CSS v4, Framer Motion, Recharts, Lucide Icons.
- **Backend:** Python 3.13, FastAPI, Uvicorn, Scikit-learn, Pandas, NumPy, SHAP (TreeExplainer), Joblib.
- **Deployment & Cloud:** Railway (Multi-service container orchestration), Hugging Face Model Hub.

---

## ▶️ Running Locally

### 1. Clone the Repository
```bash
git clone https://github.com/cropiotools/Securex-main.git
cd Securex-main
```

### 2. Backend Setup
```bash
cd backend
python -m venv venv

# Windows:
venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate

pip install -r requirements.txt
uvicorn app:app --reload --port 8000
```
Backend runs at `http://127.0.0.1:8000` (Docs at `http://127.0.0.1:8000/docs`).

### 3. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```
Frontend runs at `http://localhost:3000`.

---

## 🚀 Railway Deployment Guide

This project is deployed on Railway using a **2-service monorepo structure**:

1. **Backend Service:**
   - **Root Directory:** `/backend`
   - **Start Command:** Detected automatically from `Procfile` (`uvicorn app:app --host 0.0.0.0 --port $PORT`)
   - **Target Port:** `8000` / `$PORT`

2. **Frontend Service:**
   - **Root Directory:** `/frontend`
   - **Target Port:** `3000`
   - **Environment Variables:**
     - `PORT` = `3000`
     - `HOSTNAME` = `0.0.0.0`
     - `NEXT_PUBLIC_API_URL` = `https://securex-main-production.up.railway.app`

---

## ⚠️ Disclaimer
SecureX is a prototype developed for demonstrating machine learning, financial data processing, explainable AI, and full-stack architecture. The outputs generated should not be considered formal financial or lending advice.

---

⭐ If you find this project interesting, consider starring the repository!