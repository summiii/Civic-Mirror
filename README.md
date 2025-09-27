[README.md](https://github.com/user-attachments/files/22575567/README.md)
# Civic Mirror — AI Transparency & Trust Index

**200‑char pitch:**  
Civic Mirror uses AI to track promises vs. outcomes, creating a Transparency Index that empowers citizens, pressures leaders, and rebuilds trust in governance.

---

## What this project does
- Collects/“scrapes” **public promises** (official ministry news, budget PDFs).
- Pulls **outcomes** from the **World Bank WDI API** (health, education, environment).
- Computes a **Transparency Index (0–100)** per sector using:
  - **Fulfillment (50%)** = delivered / promised (capped at 1.0)
  - **Timeliness (30%)** = on‑time delivery (penalize delays)
  - **Confidence (20%)** = source triangulation
- Visualizes results and exports **annex CSVs** + an auto **policy brief**.

---

## Quick start (Google Colab — easiest)
1. Open **https://colab.research.google.com** → **Upload** your `.ipynb` notebook.
2. **Runtime → Run all** (first cell will install packages).
3. Outputs will appear in `data/processed/`:
   - `sector_index.csv`, `sector_summary.csv`, `peer_compare.csv`, `policy_brief.md`
4. (Optional) Run the last cell to launch the **Gradio** mini‑app.

> Colab is recommended if you’re new to Jupyter. No local setup needed.

---

## Run locally (Anaconda / JupyterLab)
```bash
# Create & activate environment
conda create -n civicmirror python=3.11 -y
conda activate civicmirror

# Install dependencies
pip install -r requirements.txt

# Launch JupyterLab and open your notebook
jupyter lab
# Run cells top-to-bottom
```

### Export notebook to PDF (two easy methods)
- **Colab/Browser:** File → Print → **Save as PDF** (recommended)
- **Local (optional):**
  ```bash
  pip install nbconvert pyppeteer
  python -m pyppeteer install
  jupyter nbconvert --to webpdf --allow-chromium-download CivicMirror.ipynb
  ```

---

## Suggested repo layout
```
civic-mirror/
├─ CivicMirror.ipynb
├─ requirements.txt
├─ README.md
├─ data/
│  ├─ raw/         # scraped/API dumps (can be ignored in git)
│  ├─ interim/     # cleaned but not final
│  └─ processed/   # final outputs for judges
│     ├─ sector_index.csv
│     ├─ sector_summary.csv
│     ├─ peer_compare.csv
│     └─ policy_brief.md
└─ (optional) .gitignore
```

**.gitignore example:**
```
data/raw/
data/interim/
.ipynb_checkpoints/
.DS_Store
```

---

## Data sources (cite in paper/DevPost)
- **World Bank — World Development Indicators (API):** country indicators such as
  - `SH.XPD.CHEX.GD.ZS` (Health spend % GDP),
  - `SE.PRM.ENRR` (Primary enrollment %),
  - `EN.ATM.CO2E.PC` (CO₂ per capita).
  Base URL: `https://api.worldbank.org/v2/country/<ISO3>/indicator/<INDICATOR>?format=json`
- **Official ministry announcements / press releases:** the URLs you scraped for promises.
- **(Optional) Budget/Gazette PDFs:** parsed with `pdfplumber`.

> Keep a CSV catalog of sources (the notebook generates `sources_catalog.csv`); add it to your annex.

---

## Key outputs for judges
- `data/processed/sector_index.csv` — final Transparency Index table.
- `data/processed/sector_summary.csv` — average index, delivery gap, on‑time rate.
- `data/processed/peer_compare.csv` — peer country WDI comparison.
- `data/processed/policy_brief.md` — 1‑page auto brief (export to PDF if you like).

---

## DevPost submission tips
- **Thumbnail:** 1200×800 PNG (3:2 ratio).
- **Elevator pitch (200 chars):** already provided above.
- **Links:** GitHub repo + 5‑minute demo video (YouTube unlisted is fine).
- **Description sections:** Problem → What it does → How we built it → Challenges → Impact (SDG16) → What’s next.

---

## License
MIT (or your preferred open-source license).
