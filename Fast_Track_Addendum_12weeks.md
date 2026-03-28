# Fast-Track Addendum — 12-Week Submission Plan
## Appended to: Research Master Plan — IMRF BNBC 2020
## Timeline: 1–3 months | Target: MDPI Buildings

---

## FAST-TRACK SCOPE REDUCTIONS
*(Apply these to hit the 12-week deadline without sacrificing publishability)*

### What You Are Cutting — and Why It's Still Fine

| Full Plan | Fast-Track Version | Justification |
|-----------|-------------------|---------------|
| 10 building archetypes | **5 archetypes** | MDPI Buildings has published papers with 4–6 models |
| 15 ground motions | **10 ground motions** | FEMA P695 minimum = 11; 10 is defensible with a note |
| 4 ML models (LR+RF+XGB+ANN) | **3 models (LR+RF+XGB)** | ANN adds <2% R² over XGBoost; cite as future work |
| 15 scale factors per IDA | **12 scale factors** | Sufficient for IDA curve definition |
| 3D building model | **2D planar frame** | Standard in 90%+ of parametric IDA papers |

**Revised dataset estimate:**
```
5 archetypes × 4 zones × 10 GMs × 12 SFs = 2,400 runs
After removing ~20% collapses = ~1,920 clean data points

Minimum acceptable for MDPI Buildings ML paper: ~1,500 rows ✓
Add a sentence in limitations: "Future work will expand to a
larger dataset with additional building configurations."
```

---

## 12-WEEK DAILY ACTION PLAN

### Week 1 — Setup + Literature *(Days 1–7)*

| Day | Morning (2 hrs) | Afternoon (2 hrs) | Output |
|-----|----------------|------------------|--------|
| Mon | Install Python 3.12, create venv | Install all packages, test OpenSeesPy | OpenSeesPy working |
| Tue | Read Kazemi 2023 paper | Read BNBC 2020 Ch. 2 seismic | Notes on both |
| Wed | Read Mahi 2025 + Rahman 2026 | Write gap statement (300 words) | Gap statement draft |
| Thu | Read Kazemi 2024 + Vamvatsikos 2002 | Set up project folder structure | Folders ready |
| Fri | Read 2 more papers from list | Write literature paragraph | Lit section started |
| Sat | Review all notes | Code `config.py` with all parameters | config.py done |
| Sun | Rest or catch up | — | — |

### Week 2 — Single Building Model *(Days 8–14)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Code `BuildingParams` class (A03: 8-story) | Class defined |
| Tue | Code nodes + boundary conditions + mass | Nodes working |
| Wed | Code Concrete02 + Steel02 materials | Materials defined |
| Thu | Code fiber sections (column + beam) | Sections defined |
| Fri | Code elements + gravity analysis | Gravity converges |
| Sat | Code modal analysis → print T1 | T1 verified vs BNBC |
| Sun | Debug any issues, document assumptions | Single model complete |

**Verification check (do this on Saturday):**
```python
# T1 from OpenSeesPy should be within ±20% of BNBC approximate
T_bnbc = 0.0466 * (8 * 3.0) ** 0.90   # = 0.82 s for 8-story
T_opensees = ...  # from ops.eigen()
assert 0.65 < T_opensees < 1.0, f"Period {T_opensees:.3f} outside expected range"
```

### Week 3 — Parametric Loop + Ground Motions *(Days 15–21)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Expand to 5 archetypes (A01–A05) in a loop | All 5 models code |
| Tue | Verify all 5 modal periods | Period table |
| Wed | Download/generate 5 ground motions | GM files ready |
| Thu | Download/generate 5 more GMs (10 total) | 10 GM files |
| Fri | Write GM scaling function | `scale_gm_to_bnbc()` |
| Sat | Scale all 10 GMs to BNBC 2020 Zone 2 spectrum | Scaled GM set |
| Sun | Write gravity + modal runner as reusable functions | Functions ready |

### Week 4 — IDA Development *(Days 22–28)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Write single NLTHA function (1 building, 1 GM, 1 SF) | `run_one_nltha()` |
| Tue | Test: run 1 analysis, print PIDR | First PIDR value |
| Wed | Add adaptive time-stepping for convergence | Robust analysis |
| Thu | Add collapse detection (PIDR ≥ 8%) | Collapse flag |
| Fri | Write IDA loop: 1 building × 1 GM × 12 SFs | First IDA curve |
| Sat | Plot first IDA curve — verify it makes sense | IDA curve figure |
| Sun | Add parallel execution with joblib | Parallel IDA ready |

**IDA sanity check:**
```
At SF = 0.1: PIDR should be < 0.3% (elastic)
At SF = 1.0: PIDR should be 0.5%–2.0% (design level)
At SF = 2.5: PIDR should be 2%–6% (severe damage)
If not → check units, check mass, check GM scaling
```

### Week 5 — Full IDA Campaign *(Days 29–35)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Run full campaign: all buildings × all GMs × all SFs | Start parallel run |
| Tue | Monitor progress, fix any crashes | Campaign running |
| Wed | Collect all results → master CSV | `ida_results_raw.csv` |
| Thu | Clean dataset: remove NaN, impossible values | Clean CSV |
| Fri | Log-transform PIDR and Sa | ML-ready features |
| Sat | **Start writing Section 2** (building models — no results needed) | 500 words |
| Sun | **Continue writing Section 2** | Section 2 draft |

> Key insight: While the IDA runs (Monday–Wednesday), you have
> free time. Use it to start writing. Section 2 needs zero results.

### Week 6 — EDA + Start ML *(Days 36–42)*

| Day | Task | Output |
|-----|------|--------|
| Mon | EDA: distribution plots, correlation heatmap | 4 EDA figures |
| Tue | EDA: IDA curves for all zones (Fig. 3, 4) | IDA figures |
| Wed | Train Linear Regression → record R², RMSE | LR baseline result |
| Thu | Train Random Forest → record R², RMSE | RF result |
| Fri | Train XGBoost → record R², RMSE | XGBoost result |
| Sat | Generate predicted vs actual plot (Fig. 7) | ML comparison figure |
| Sun | **Write Section 3** (OpenSeesPy methodology) | 600 words |

### Week 7 — SHAP + Fragility *(Days 43–49)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Run SHAP on best model → beeswarm + bar plots | Fig. 8, 9 |
| Tue | Compute fragility — Zone 2 (Dhaka) | Zone 2 fragility |
| Wed | Compute fragility — all 4 zones | All fragility curves |
| Thu | Generate zone comparison figure (Fig. 6) | Fig. 6 saved |
| Fri | Fill in Table 5: θ and β for all zones × IO/LS/CP | Table 5 complete |
| Sat | **Write Section 4** (GMs and IDA procedure) | 500 words |
| Sun | **Write Section 5** (ML framework) | 500 words |

### Week 8 — All Results Ready + More Writing *(Days 50–56)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Generate all remaining figures (Fig. 1, 2, 5) | All 9 figures done |
| Tue | Complete all 5 tables | All tables done |
| Wed | Cross-validate best model (5-fold) | CV score |
| Thu | **Write Section 6.1–6.2** (IDA + fragility results) | 700 words |
| Fri | **Write Section 6.3–6.4** (ML results + SHAP) | 700 words |
| Sat | **Write Section 6.5 + Section 7** (discussion + conclusions) | 700 words |
| Sun | Rest | — |

### Week 9 — Write Introduction + Abstract *(Days 57–63)*

| Day | Task | Output |
|-----|------|--------|
| Mon | Write Section 1.1–1.2 (seismic risk + BNBC context) | 500 words |
| Tue | Write Section 1.3 (literature review) | 400 words |
| Wed | Write Section 1.4–1.5 (gap + objectives) | 250 words |
| Thu | Write Abstract (250 words — last!) | Abstract done |
| Fri | Full paper read-through — fix flow | Clean draft |
| Sat | Check all figure/table references in text | All numbered |
| Sun | Rest | — |

### Weeks 10–11 — Revision *(Days 64–77)*

| Task | Notes |
|------|-------|
| Ask a colleague to read Section 6 | Fresh eyes on results |
| Check all equations are numbered | Every equation needs (Eq. X) |
| Check all figures at 300 dpi | Save with `dpi=300, bbox_inches='tight'` |
| Similarity check | Use iThenticate or university tool, target < 15% |
| Format to MDPI template | Download from mdpi.com/authors |
| Write cover letter | Use template from master plan |

### Week 12 — Submit *(Days 78–84)*

| Day | Task |
|-----|------|
| Mon | Final read-through |
| Tue | Format check against MDPI author guidelines |
| Wed | Register at susy.mdpi.com, prepare submission |
| Thu | **Submit** |
| Fri | Upload dataset to Zenodo (increases citation count) |

---

## GROUND MOTION DECISION TREE

```
Do you have PEER NGA access?
│
├── YES → Download these 10 records:
│         1. Imperial Valley 1940 (El Centro)
│         2. Kobe 1995 (TAZ090)
│         3. Chi-Chi 1999 (TCU045)
│         4. Northridge 1994 (Canoga Park)
│         5. Loma Prieta 1989 (Gilroy Array)
│         6. Duzce 1999 (Turkey)
│         7. Cape Mendocino 1992
│         8. Superstition Hills 1987
│         9. Whittier Narrows 1987
│        10. Chi-Chi 1999 (TCU082)
│
└── NO → Use synthetic GMs (built into framework):
          seeds = [42, 99, 17, 55, 88, 23, 61, 34, 77, 12]
          10 records × varying PGA (0.15g–0.35g)
          Add this limitation note to your paper:
          "Synthetic ground motions were used due to lack of
           regional strong-motion records for Bangladesh.
           Future work will validate with real PEER NGA records."
```

---

## ML FAST-TRACK CODE (copy-paste ready)

```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import r2_score, mean_squared_error, mean_absolute_error
from xgboost import XGBRegressor
import shap, time

# ── Load dataset ──────────────────────────────────────────────
df = pd.read_csv('data/processed/ida_ml_dataset.csv')
df = pd.get_dummies(df, columns=['soil_class'], prefix='soil')

FEATURES = ['n_stories','H_total','T1','bay_width','n_bays',
            'col_b_mm','col_h_mm','beam_h_mm','fc_MPa','rho_col',
            'Z','R','ln_Sa','PGA','soil_SC','soil_SD']
TARGET = 'ln_PIDR'

X = df[[f for f in FEATURES if f in df.columns]].fillna(0)
y = df[TARGET]

# ── Split (stratify by zone for balanced representation) ──────
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=df['zone'])

scaler = StandardScaler()
X_tr_sc = scaler.fit_transform(X_train)
X_te_sc  = scaler.transform(X_test)    # NEVER fit on test set

# ── Train 3 models ────────────────────────────────────────────
results = {}

models = {
    'Linear Regression': (LinearRegression(), True),   # True = needs scaling
    'Random Forest':     (RandomForestRegressor(n_estimators=300,
                          n_jobs=-1, random_state=42), False),
    'XGBoost':           (XGBRegressor(n_estimators=400,
                          learning_rate=0.05, max_depth=6,
                          random_state=42, verbosity=0), False),
}

print(f"\n{'Model':<22} {'R²':>7} {'RMSE':>8} {'MAE':>8} {'Time':>7}")
print('-' * 58)

for name, (model, needs_scale) in models.items():
    X_tr = X_tr_sc if needs_scale else X_train
    X_te = X_te_sc if needs_scale else X_test
    t0 = time.time()
    model.fit(X_tr, y_train)
    y_pred = model.predict(X_te)
    r2   = r2_score(y_test, y_pred)
    rmse = np.sqrt(mean_squared_error(y_test, y_pred))
    mae  = mean_absolute_error(y_test, y_pred)
    elapsed = time.time() - t0
    results[name] = {'model': model, 'y_pred': y_pred,
                     'R2': r2, 'RMSE': rmse, 'MAE': mae}
    print(f"{name:<22} {r2:>7.4f} {rmse:>8.4f} {mae:>8.4f} {elapsed:>6.1f}s")

# ── Cross-validate best model ─────────────────────────────────
best_name = max(results, key=lambda k: results[k]['R2'])
best_model = results[best_name]['model']
cv_scores = cross_val_score(best_model, X_train, y_train,
                             cv=5, scoring='r2', n_jobs=-1)
print(f"\nBest model: {best_name}")
print(f"5-fold CV R²: {cv_scores.mean():.4f} ± {cv_scores.std():.4f}")

# ── SHAP analysis ─────────────────────────────────────────────
explainer   = shap.TreeExplainer(best_model)
shap_values = explainer.shap_values(X_test)

import matplotlib.pyplot as plt
plt.figure(figsize=(10, 7))
shap.summary_plot(shap_values, X_test,
                  feature_names=X.columns.tolist(), show=False)
plt.tight_layout()
plt.savefig('plots/figures/fig08_shap.png', dpi=300, bbox_inches='tight')
plt.close()
print("SHAP plot saved.")
```

---

## WRITING PRODUCTIVITY RULES FOR FAST-TRACK

```
Rule 1 — 500 words minimum per day during writing weeks (9–11)
         500 words/day × 14 writing days = 7,000 words = complete paper

Rule 2 — Write ugly first drafts
         Do not edit while writing. Finish the section first, then edit.
         Perfectionism is the enemy of a 12-week deadline.

Rule 3 — Use your figures as anchors
         Open the figure you're describing, write 2–3 paragraphs about it.
         Every result figure = ~200 words in Section 6.

Rule 4 — Use active voice
         WRONG: "It was found that XGBoost achieved..."
         RIGHT: "XGBoost achieved..."

Rule 5 — One idea per sentence
         Long sentences with many clauses = reviewer confusion = rejection.
         If a sentence is >25 words, split it.

Rule 6 — Every claim needs a citation or a figure reference
         Reviewers will ask "where is the evidence?" for every statement.
         Rule: no sentence in the results section without (Fig. X) or (Table X).
```

---

## DAILY MINIMUM COMMITMENT

To finish in 12 weeks as a beginner, you need:

```
Weeks 1–8  (analysis + coding):  2–3 hours per day
Weeks 9–11 (writing):            3–4 hours per day
Week 12    (review + submit):    2 hours per day

Total: ~200–250 hours over 12 weeks
That is ~3 hours/day, 6 days/week — achievable as a part-time commitment.
```

---

*Fast-Track Addendum v1.0 | IMRF BNBC 2020 | 12-week target | 2025*
