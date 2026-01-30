# Open_311_Data_Analysis

A collection of analysis, scripts, and notebooks for working with Open 311 service request data. This repository centralizes data processing, exploratory analysis, visualizations, and reproducible notebooks to help understand trends, response times, and spatial patterns in 311 service requests.

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Install](#install)
- [Data](#data)
- [Usage](#usage)
  - [Notebooks](#notebooks)
  - [Scripts](#scripts)
- [Examples](#examples)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Project Overview

This repo is intended to host reproducible analyses of Open 311 datasets (city-provided 311 service request data). Typical tasks include:

- Data ingestion and cleaning
- Time-series and trend analysis
- Spatial analysis and mapping
- Response-time and SLA analysis
- Generating reproducible notebooks and reports

## Repository Structure

(Adjust these folders to match your repo contents)

- `data/` — raw and processed datasets (do not store sensitive data here; use .gitignore for large/raw files)
- `notebooks/` — Jupyter/R Markdown notebooks for exploration and reports
- `src/` or `scripts/` — Python/R scripts and utilities used by notebooks or for batch processing
- `reports/` — generated figures, PDF reports, or dashboards
- `requirements.txt` / `environment.yml` — Python dependencies and environment specs
- `README.md` — this file

## Getting Started

### Prerequisites

- Python 3.8+ (or the version you prefer)
- pip or conda
- Optional: Git for version control

### Install

Using pip:
```bash
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
.venv\Scripts\activate           # Windows
pip install --upgrade pip
pip install -r requirements.txt
```

Or with conda:
```bash
conda env create -f environment.yml
conda activate open-311
```

## Data

This project expects Open 311 datasets (CSV/JSON) from one or more cities. Data acquisition can vary by city — common sources:

- City open data portals (CSV/JSON endpoints)
- Socrata / data.city.* portals
- API endpoints for 311 systems

Place downloaded raw files in `data/raw/` and processed outputs in `data/processed/`. Example dataset columns typically include:
- `service_request_id`, `service_name`, `status`, `requested_datetime`, `updated_datetime`, `address`, `latitude`, `longitude`, `agency_responsible`, etc.

If your dataset is large, keep raw files out of Git and provide scripts that fetch/process the data.

## Usage

### Notebooks

Open the notebooks in `notebooks/` to explore analyses. To run them interactively:
```bash
jupyter lab
# or
jupyter notebook
```

Recommended notebooks:
- `notebooks/01_data_ingest.ipynb` — data download and basic cleaning
- `notebooks/02_exploratory_analysis.ipynb` — trends, counts, time-series
- `notebooks/03_spatial_analysis.ipynb` — maps and heatmaps
- `notebooks/04_response_time.ipynb` — SLA and response-time analysis

(Replace names above with actual notebook filenames in the repo.)

### Scripts

Scripts in `scripts/` perform common tasks:
- `scripts/fetch_data.py` — fetch city data via API
- `scripts/clean_data.py` — standardize and clean raw inputs
- `scripts/generate_report.py` — run pipeline to produce reports/figures

Run a script:
```bash
python scripts/clean_data.py --input data/raw/city_311.csv --output data/processed/city_311_clean.csv
```

## Examples

Quick examples of analyses you might run:

- Count service requests by type:
```python
# in a notebook
df.groupby('service_name').size().sort_values(ascending=False).head(20)
```

- Calculate response time (hours):
```python
df['requested_datetime'] = pd.to_datetime(df['requested_datetime'])
df['closed_datetime'] = pd.to_datetime(df['closed_datetime'])
df['response_hours'] = (df['closed_datetime'] - df['requested_datetime']).dt.total_seconds() / 3600
```

- Create a heatmap of request density (example using geopandas / contextily)

## Testing

If tests exist, run them with:
```bash
pytest
```
Add tests for new processing functions and utilities to keep analyses reproducible.

## Contributing

Contributions are welcome! Suggested workflow:

1. Fork the repo
2. Create a branch for your feature/fix
3. Add tests or notebooks demonstrating the change
4. Open a pull request with a clear description

Please follow code style (PEP8 for Python) and include reproducible examples in notebooks.

## License

Specify your license here (e.g., MIT, Apache-2.0). If unsure, add a LICENSE file at the repo root.

## Contact

Project maintainer: Your Name (replace this line)  
Repository: https://github.com/EddiePueb1/Open_311_Data_Analysis
