# HackSecure Hackathon 2025
### Detecting and analysing potentially coordinated hostile narratives in public digital content

HackSecure is a demonstration platform for analysing **publicly available text** for configured terms and sentiment patterns. It combines a FastAPI backend, React dashboard, and a lightweight Java CSV utility.

> **Responsible use:** This is an analytical aid, not a truth detector. A keyword match or negative sentiment does not prove that content is false, coordinated, malicious, or anti-national. Results require human review and context. Process only data you are authorised to use; do not profile private individuals or groups.

## Features
- Single-text and CSV batch analysis
- Explainable, configurable keyword matching
- Sentiment estimation (VADER, with a simple fallback)
- Review-priority score and matched-term explanations
- Dashboard summaries, search, filters, and CSV export
- Sample CSV and optional Java CSV preview utility

## Repository structure
```text
Hacksecure_2025/
├── Backend/app/       # FastAPI API and analysis logic
├── Backend/tests/     # Unit tests
├── Frontend/src/      # React + Vite dashboard
├── WebSS/             # Add your actual website screenshot
├── data/              # Demo CSV
├── docs/              # Workflow and API documentation
├── SimpleCSV.java
├── Workflow.png
├── file.csv
├── LICENSE
└── README.md
```

## Requirements
- Python 3.10+
- Node.js 18+ and npm
- Java 11+ (optional CSV utility)

## Run the project

### Backend
```bash
cd Backend
python -m venv .venv
# Windows PowerShell: .venv\\Scripts\\Activate.ps1
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```
API docs: http://127.0.0.1:8000/docs

### Frontend (new terminal)
```bash
cd Frontend
npm install
npm run dev
```
Open the Vite URL (normally http://localhost:5173). Set `VITE_API_URL` if the API is hosted elsewhere.

### Sample data
Upload `data/sample_posts.csv` from the dashboard. CSV files must contain a `text` column and may contain an `id` column.

## API
| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Service status |
| GET | `/health` | Health check |
| GET | `/api/summary` | Aggregate session counts |
| POST | `/api/analyze` | Analyse one text |
| POST | `/api/analyze/batch` | Analyse up to 500 records |
| POST | `/api/analyze/csv` | Upload CSV |
| GET | `/api/results` | Recent results |
| GET | `/api/export` | Download results as CSV |


## Analysis approach
1. Normalise whitespace and case.
2. Match against a transparent, configurable phrase list.
3. Estimate sentiment.
4. Calculate a review-priority heuristic.
5. Present matched terms and explanations for human verification.

Default phrases are illustrative placeholders. Maintain a balanced taxonomy with domain experts. Political criticism, dissent, satire, protest, and journalism must not automatically be treated as harmful.

## Limitations
- Rules can miss context, sarcasm, spelling variations, and multilingual content.
- Sentiment tools can misread political or culturally specific language.
- A score is a triage heuristic, not a probability or verdict.
- This starter does not establish coordination, attribution, bot activity, or claim veracity.
- Results are stored in memory and cleared when the API restarts.

## Production hardening
Add authentication, persistent storage, rate limiting, audit logs, privacy controls, retention rules, and documented evaluation before deployment.

## Screenshots
Add your real screenshot as `WebSS/WebSS.png`; then this will render:
![HackSecure dashboard](WebSS/WebSS.png)

**Team:** Code Clowns · **Event:** HackSecure Hackathon 2025

See [LICENSE](LICENSE).
