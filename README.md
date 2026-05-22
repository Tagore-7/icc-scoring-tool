# ICC Grant Success Predictor

Interactive tool for predicting grant proposal success probability, built for the Institute of Computing and Cybersystems at Michigan Technological University.

## How it works

Enter a proposal's PI, sponsor, department, funding type, duration, and amount — the tool instantly returns a predicted funding probability and a breakdown of which factors are helping or hurting the score.

Model trained on 369 proposals (FY22–FY25). AUC 0.69. For advisory use only.

## Files

| File | Purpose |
|---|---|
| `index.html` | The scoring tool (all logic runs in the browser) |
| `model_export.json` | Trained logistic regression coefficients + scaler |

PI win rates are fetched live from the ICC Google Sheet automatically — no file needed.

## Setup (first time)

**1. Upload both files** to the GitHub repo root:
- `index.html`
- `model_export.json`

**2. Enable GitHub Pages**
- Go to repo → Settings → Pages
- Source: Deploy from a branch → `main` → `/ (root)`
- Click Save

The tool will be live at: `https://YOUR-USERNAME.github.io/REPO-NAME/`

## Updating the data

**PI win rates** update automatically — the tool fetches them live from the Google Sheet every time it loads. No action needed when new proposals are added.

**Model coefficients** only need updating if the model is retrained with new data:

```bash
cd ~/ICC_research_work
python3 05_export_model.py
```

Then re-upload `model_export.json` to the GitHub repo.

## Using it locally

```bash
cd ~/ICC_research_work
python3 -m http.server 8080
```

Then open: `http://localhost:8080`

## Notes

- Non-competitive proposal types (Continuations, Amendments, Supplements) win at ~100% and are excluded from the model
- New PIs with no history default to the overall mean win rate (40.9%)
- Fiscal year is fixed at FY26
