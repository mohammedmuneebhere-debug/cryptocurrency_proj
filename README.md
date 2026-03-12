# CryptoVista

CryptoVista is a modern cryptocurrency dashboard providing live tracking, historical charting, automated price prediction, and AI-powered market insights.

## Project Architecture

This project is a full-stack application composed of distinct services:

1. **Frontend (`/frontend`)**
   - Built with **React** (Vite), **TailwindCSS**, and **Recharts**.
   - Handles real-time dashboard UI, charting, and user interactions.
   - Configured for deployment via Vercel (`vercel.json`).

2. **Backend (`/backend`)**
   - Built with **Python** & **FastAPI**.
   - Serves cryptocurrency data, price prediction endpoints, and Server-Sent Events (SSE) for live streaming updates.
   - Includes LLM integration for generating coin summaries (`/llm`).
   - Configured for deployment via Render (`render.yaml`).

3. **Machine Learning (`/ml`)**
   - Contains feature engineering (`features.py`) and predictive modeling modules (`model.py`, `run_inference.py`) to forecast price movements.

4. **Data Worker (`/worker`)**
   - Handles background jobs and data pipelines.
   - Integrates with Coinbase API (`coinbase_client.py`), running scheduled tasks (`scheduler.py`) to continuously ingest and process market data (`pipeline.py`).

## Tech Stack
- **Frontend**: React 19, Vite, TailwindCSS (v3.4), Recharts, Axios, Supabase.
- **Backend**: Python 3.11, FastAPI, Uvicorn, SSE-Starlette.

## Getting Started

### Prerequisites
- Node.js
- Python 3.11+

### Running the Backend Local Server
1. Navigate to the `backend` directory:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   # On Windows:
   .venv\Scripts\activate
   # On macOS/Linux:
   source .venv/bin/activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Start the FastAPI server (it will run on port 8000 by default):
   ```bash
   uvicorn app:app --host 0.0.0.0 --port 8000 --reload
   ```

### Running the Frontend Local Server
1. Navigate to the `frontend` directory:
   ```bash
   cd frontend
   ```
2. Install dependencies (if this is the first time):
   ```bash
   npm install
   ```
3. Start the Vite development server:
   ```bash
   npm run dev
   ```

## Main API Endpoints
- `GET /{coin}/chart` - Returns historical chart data for the selected coin.
- `GET /{coin}/prediction` - Returns a price prediction for the selected coin.
- `GET /llm/{coin}-summary` - Provides an AI-generated insight summary.
- `GET /api/stream/{coin}` - SSE endpoint for streaming live price updates.

## Deployment Notes
- **Backend:** Designed to be deployed on Render. The configuration is present in `render.yaml` at the project root.
- **Frontend:** Includes basic configuration setting it up for deployment on Vercel (`vercel.json`).
