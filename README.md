# Cab_demand_prediction-GIH-

Cab Demand Prediction (GIH)

This repository contains code, data, and models used for predicting cab demand (peak-hour demand) in Bangalore. The project includes a small Flask service to serve predictions, pre-trained model artifacts, datasets used for training/analysis, and supporting front-end map pages for visualization.

**Quick Summary**
- **App (prediction API):** `PeakHourDemand/app.py` — Flask app that loads joblib model files and exposes a `/predict` endpoint.
- **Pre-trained models:** `PeakHourDemand/models/` — several `.pkl` files (`demand_prediction.pkl`, `demand_prediction_model1.pkl`, etc.).
- **Datasets:** `Dataset/` — CSVs used for training, cleaning, and analysis (parking, RideReqTimeData, apartment data, etc.).
- **Front-end / visualizations:** `PeakHourDemand/templates/` and `PeakHourDemand/static/` — HTML map pages and assets.

**Prerequisites**
- Python 3.8+ (3.10 recommended)
- A virtual environment (recommended)
- Git for version control

**Install & Run (PowerShell)**
1. Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install required packages (create a `requirements.txt` if you want reproducible installs). Typical packages for this project:

```powershell
pip install flask joblib numpy pandas scikit-learn
```

3. Run the Flask app (from repository root):

```powershell
python .\PeakHourDemand\app.py
```

The app will start on `http://127.0.0.1:5000/`. The root serves the front-end `index.html` from `PeakHourDemand/static`.

**Prediction API**
POST `/predict` accepts JSON with the following fields:

```json
{
	"model": "model1",            // optional: model1/model2/model3/model4
	"latitude": 12.9716,
	"longitude": 77.5946,
	"time": "14:30"              // 24-hour HH:MM format
}
```

Response (example):

```json
{ "demand": "High" }
```

Notes:
- The Flask app converts the `time` string into minutes-since-midnight and passes `[latitude, longitude, time_numeric]` to the selected model.
- Models are loaded via `joblib.load` from `PeakHourDemand/models/`.

**Repository structure (key items)**
- `PeakHourDemand/` — Flask app, models, templates, static assets, and example notebooks (`test1.ipynb`...).
- `Dataset/` — CSV files used in the project and cleaned datasets.
- `Miscelinous/`, `Research Papers/`, `screenshots/` — supporting documents and artifacts.

**Recommendations & Next Steps**
- Add a `requirements.txt` (e.g., `pip freeze > requirements.txt`) so others can install exact dependencies.
- Consider using `git-lfs` for the model `.pkl` files if they are large: `git lfs install; git lfs track "PeakHourDemand/models/*.pkl"`.
- Add a short CONTRIBUTING.md and LICENSE if you plan to share publicly.
- Add simple tests (for example, a pytest that calls `/predict` with a sample request) and a CI workflow (GitHub Actions) for automatic checks.

**How I inspected this repo**
- Main app: `PeakHourDemand/app.py`
- Models: files under `PeakHourDemand/models/`
- Datasets: files under `Dataset/`

If you want, I can:
- Generate a `requirements.txt` by scanning imports and creating a suggested list.
- Add a small integration test for the `/predict` endpoint.
- Create a GitHub Actions workflow that runs lint/tests on push.

---
If you'd like changes to wording, or to include environment/installation scripts (e.g., `docker-compose`, `requirements.txt`, or an environment.yml`), tell me which format you prefer and I'll add them.
