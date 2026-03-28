# Research Master Plan — TAILORED VERSION
## ML-Based Seismic Drift Prediction of RC Intermediate Moment Frames
### BNBC 2020 | All 4 Seismic Zones | OpenSeesPy + Python ML
### Target: MDPI *Buildings* (Q1, Open Access)

**Skill Level:** Beginner — every step explained in full detail
**Frame Type:** RC IMRF (Intermediate Moment Resisting Frame, R = 3.0)
**Zones:** Zone 1 (Rajshahi), Zone 2 (Dhaka), Zone 3 (Chittagong), Zone 4 (Sylhet)
**Last Updated:** 2025

> **How to use this document:**
> Work through it top to bottom. Never skip a phase.
> Each phase has a checklist — tick every box before moving to the next.
> If you get stuck, the "Beginner Note" boxes tell you exactly what to do.

---

## TABLE OF CONTENTS

1. [Ultimate Goal & Novelty](#1-ultimate-goal--novelty)
2. [Why IMRF — Your Unique Angle](#2-why-imrf--your-unique-angle)
3. [Paper Structure](#3-paper-structure)
4. [Mathematical Framework](#4-mathematical-framework)
5. [Phase 0 — Environment Setup](#phase-0--environment-setup-week-1)
6. [Phase 1 — Literature Review](#phase-1--literature-review-weeks-12)
7. [Phase 2 — Structural Modelling Plan](#phase-2--structural-modelling-plan-weeks-24)
8. [Phase 3 — Ground Motion Plan](#phase-3--ground-motion-plan-week-3)
9. [Phase 4 — IDA Campaign](#phase-4--ida-campaign-weeks-57)
10. [Phase 5 — Dataset & EDA](#phase-5--dataset--eda-week-7)
11. [Phase 6 — Machine Learning](#phase-6--machine-learning-weeks-89)
12. [Phase 7 — Fragility Curves](#phase-7--fragility-curves-week-9)
13. [Phase 8 — Writing the Paper](#phase-8--writing-the-paper-weeks-1013)
14. [Phase 9 — Submission](#phase-9--submission-week-14)
15. [OpenSeesPy Coding Roadmap](#openseespy-coding-roadmap)
16. [Figures & Tables Checklist](#figures--tables-checklist)
17. [Timeline](#timeline)
18. [Tools Stack](#tools-stack)
19. [Risk Register](#risk-register)
20. [Quick Reference — All Equations](#quick-reference--all-equations)

---

## 1. ULTIMATE GOAL & NOVELTY

### One-Line Research Statement
> Develop the first ML surrogate model to predict seismic inter-story drift of RC
> **Intermediate** Moment Resisting Frames designed per **BNBC 2020** across all four
> seismic zones of Bangladesh, using an open-source OpenSeesPy IDA framework.

### Why This Will Get Published
Most existing ML-seismic studies focus on SMRF (Special Moment Frames).
IMRF (R = 3.0) is far more common in Bangladesh residential and commercial
construction — yet no ML drift prediction study exists for IMRF under BNBC 2020.
This is a clear, defensible, unique gap.

### Research Objectives
- **O1:** Build parametric RC IMRF models (4–12 stories) in OpenSeesPy per BNBC 2020
- **O2:** Run IDA with scaled ground motions for all 4 BNBC zones
- **O3:** Train ML models (LR, RF, XGBoost, ANN) to predict PIDR
- **O4:** Generate and compare seismic fragility curves across all zones
- **O5:** Use SHAP to identify which parameters drive drift in IMRF buildings

### Research Questions
1. How accurately can ML predict PIDR for IMRF buildings? (Target: R² > 0.90)
2. How does seismic zone (Z = 0.12 to 0.36) affect IMRF fragility?
3. Are IMRF buildings more vulnerable than SMRF at the same drift level?
4. Which structural feature (height, period, section size) dominates drift?

---

## 2. WHY IMRF — YOUR UNIQUE ANGLE

> **Beginner Note:** This section helps you explain your choice to journal reviewers.
> IMRF uses R = 3.0 instead of R = 5.0 for SMRF. Lower R means higher design
> force but less ductility detailing. Most Bangladesh buildings are IMRF.

### IMRF vs SMRF — Key Differences for Your Paper

| Property | SMRF | IMRF | Impact on Your Study |
|----------|------|------|---------------------|
| Response reduction R | 5.0 | **3.0** | Higher design base shear |
| Ductility detailing | Full | Moderate | Less deformation capacity |
| Hinge rotation capacity | High | Moderate | Lower collapse PIDR threshold |
| Common in Bangladesh | Rare (high-rise) | **Very common** | Higher real-world relevance |
| ML studies available | Several | **None for BNBC 2020** | Your novelty |

### IMRF Collapse Prevention Threshold
Because IMRF has moderate ductility, use slightly conservative thresholds:

| Performance Level | SMRF PIDR | IMRF PIDR (your study) |
|------------------|-----------|----------------------|
| Immediate Occupancy (IO) | 1.0% | 0.7% |
| Life Safety (LS) | 2.0% | 1.5% |
| Collapse Prevention (CP) | 4.0% | 3.0% |
| Collapse | 10.0% | 8.0% |

> Cite: FEMA 356 Table C1-3 for these values.

---

## 3. PAPER STRUCTURE

### Proposed Title (Final Recommendation)
**"Seismic Fragility and Machine Learning-Based Drift Prediction of RC Intermediate
Moment Frames in Bangladesh Using OpenSeesPy Incremental Dynamic Analysis
Under BNBC 2020"**

*Why this title works:*
- "Seismic Fragility AND ML" — two outputs, stronger contribution
- "Bangladesh" — geographic specificity signals novelty
- "OpenSeesPy" — signals rigorous open-source methodology
- "BNBC 2020" — signals current code compliance

### Paper Outline with Word Targets

```
Abstract ...................... 250 words (write LAST)
│
├── 1. Introduction
│   ├── 1.1 Seismic risk in Bangladesh         ~300 words
│   ├── 1.2 BNBC 2020 overview                 ~200 words
│   ├── 1.3 Literature review                  ~400 words
│   ├── 1.4 Gap identification                 ~150 words
│   └── 1.5 Objectives of this study           ~100 words
│
├── 2. Description of Building Models
│   ├── 2.1 Building archetypes                ~300 words
│   ├── 2.2 Material properties                ~200 words
│   ├── 2.3 BNBC 2020 loading                  ~200 words
│   └── 2.4 OpenSeesPy modelling assumptions   ~200 words
│
├── 3. Nonlinear Modelling Methodology
│   ├── 3.1 Fiber section definition           ~300 words
│   ├── 3.2 Material models (Concrete02/Steel02)~250 words
│   └── 3.3 Model verification                 ~200 words
│
├── 4. Ground Motions and IDA
│   ├── 4.1 Ground motion selection            ~200 words
│   ├── 4.2 Scaling to BNBC 2020 spectrum      ~200 words
│   └── 4.3 IDA procedure                      ~250 words
│
├── 5. Machine Learning Framework
│   ├── 5.1 Dataset construction               ~200 words
│   ├── 5.2 Feature engineering                ~200 words
│   ├── 5.3 ML models and training             ~300 words
│   └── 5.4 SHAP analysis                      ~150 words
│
├── 6. Results and Discussion
│   ├── 6.1 IDA curves and dispersion          ~300 words
│   ├── 6.2 Seismic fragility curves           ~400 words
│   ├── 6.3 ML model performance               ~400 words
│   ├── 6.4 SHAP feature importance            ~300 words
│   └── 6.5 Practical implications             ~200 words
│
├── 7. Conclusions                             ~350 words
└── References                                 40–50 citations
```

**Total: ~6,000–7,000 words**

> **Beginner Note — Writing order:**
> Write sections in this order: 2 → 3 → 4 → 5 → 6 → 7 → 1 → Abstract
> Never start with the Introduction. Write it second-to-last.

---

## 4. MATHEMATICAL FRAMEWORK

> **Beginner Note:** You do not need to derive these equations.
> You need to: (a) understand what each equation means,
> (b) implement them in Python code, and (c) cite them properly.

---

### 4.1 BNBC 2020 Design Spectrum

The design spectrum defines how much ground acceleration a building
must be designed to resist at each period T.

```
                    ┌ SDS × [0.4 + 0.6(T/T₀)]    0 ≤ T ≤ T₀
                    │
Sa(T)  =            ├ SDS                          T₀ ≤ T ≤ Ts
                    │
                    ├ SD₁ / T                      Ts ≤ T ≤ TL
                    │
                    └ SD₁ × TL / T²               T > TL
```

**Parameter definitions:**
```
Z    = seismic zone coefficient
Fa   = site amplification (short period)  ← Table 2.5.4, BNBC 2020
Fv   = site amplification (1-second)      ← Table 2.5.4, BNBC 2020

SMS  = Fa × 2.5 × Z       (site-modified short-period)
SM₁  = Fv × Z             (site-modified 1-second)
SDS  = (2/3) × SMS        (design short-period spectral acceleration)
SD₁  = (2/3) × SM₁        (design 1-second spectral acceleration)

T₀   = 0.2 × SD₁ / SDS   (lower corner period)
Ts   = SD₁ / SDS          (upper corner period)
TL   = 6.0 s              (long-period transition, BNBC 2020)
```

**Zone parameters for your study:**

| Zone | Z | City | Fa (SD) | Fv (SD) | SDS | SD₁ |
|------|---|------|---------|---------|-----|-----|
| Zone 1 | 0.12 | Rajshahi | 1.6 | 2.4 | 0.320 | 0.192 |
| Zone 2 | 0.20 | Dhaka | 1.6 | 2.4 | 0.533 | 0.320 |
| Zone 3 | 0.28 | Chittagong | 1.6 | 2.4 | 0.747 | 0.448 |
| Zone 4 | 0.36 | Sylhet | 1.6 | 2.4 | 0.960 | 0.576 |

---

### 4.2 IMRF Building Period and Base Shear

**Approximate fundamental period (BNBC 2020 Eq. 2.5.7):**
```
T = Ct × H^x

where:
  Ct = 0.0466  (RC moment frames)
  x  = 0.90
  H  = total height of building in metres
```

**Example periods for your buildings:**

| Stories | H (m) | T_approx (s) |
|---------|-------|-------------|
| 4 | 12 | 0.44 s |
| 6 | 18 | 0.63 s |
| 8 | 24 | 0.82 s |
| 10 | 30 | 0.99 s |
| 12 | 36 | 1.17 s |

**Design base shear (BNBC 2020):**
```
V = Cs × W

where:
  Cs   = Sa(T) / R × I     (seismic response coefficient)
  R    = 3.0                (IMRF — this is your key parameter)
  I    = 1.0                (residential occupancy)
  W    = seismic weight = DL + 0.25 × LL
```

---

### 4.3 Inter-Story Drift Ratio (PIDR)

This is the most important response quantity in your study.

```
PIDR_story_i = |u_i - u_{i-1}| / h_i

where:
  u_i       = absolute lateral displacement at floor i (from OpenSeesPy)
  u_{i-1}   = absolute lateral displacement at floor below
  h_i       = height of story i (m)

Peak PIDR = maximum PIDR across all stories and all time steps
```

---

### 4.4 IDA — Incremental Dynamic Analysis

IDA scales a ground motion to increasing intensity and records PIDR at each level.

```
IDA curve:
  X-axis: Sa(T₁, 5%)  — intensity measure (IM) in units of g
  Y-axis: PIDR        — damage measure (DM) in %

Scaling: a_scaled(t) = SF × a_record(t)
  where SF is chosen so that Sa_scaled(T₁) = target Sa level
```

**Collapse definition for IMRF:**
```
Structural collapse = PIDR ≥ 8.0%
(more conservative than SMRF due to lower ductility)
```

---

### 4.5 Seismic Fragility — Cloud Analysis Method

**Step 1 — Log-linear regression on your IDA dataset:**
```
ln(PIDR) = a + b × ln(Sa) + ε

Solve for a, b using scipy.stats.linregress on your data
ε = residuals → used to compute dispersion β
```

**Step 2 — Dispersion:**
```
β_D|IM = std[ ln(PIDR_i) - (a + b × ln(Sa_i)) ]
```

**Step 3 — Fragility probability:**
```
P(PIDR > PIDR_LS | Sa) = Φ[ (ln(Sa) - ln(θ)) / β ]

where:
  θ   = median Sa at which 50% of runs exceed PIDR_LS
      = exp[ (ln(PIDR_LS) - a) / b ]
  β   = dispersion from Step 2
  Φ   = scipy.stats.norm.cdf()
```

**Python implementation:**
```python
from scipy import stats
import numpy as np

# Fit regression
slope, intercept, r, p, se = stats.linregress(
    np.log(Sa_array), np.log(PIDR_array)
)

# Dispersion
residuals = np.log(PIDR_array) - (intercept + slope * np.log(Sa_array))
beta = np.std(residuals)

# Fragility at Life Safety (PIDR_LS = 1.5% for IMRF)
PIDR_LS = 0.015
theta = np.exp((np.log(PIDR_LS) - intercept) / slope)

Sa_range = np.linspace(0.01, 2.5, 200)
Pf = stats.norm.cdf((np.log(Sa_range) - np.log(theta)) / beta)
```

---

### 4.6 Machine Learning — Target and Features

**Why log-transform PIDR:**
```
PIDR follows a log-normal distribution (proven in earthquake engineering).
Training ML on ln(PIDR) instead of PIDR:
  ✓ Normalises the distribution
  ✓ Improves ML accuracy
  ✓ Consistent with fragility analysis (also uses log-normal)

y = ln(PIDR)   ← what you train ML models to predict
```

**Feature vector X (18 features):**
```
Structural:
  x1  = n_stories         (integer: 4, 6, 8, 10, 12)
  x2  = H_total           (metres: 12 to 36)
  x3  = T1                (seconds: from OpenSeesPy eigen)
  x4  = bay_width         (metres: 4.5, 5.0, 5.5, 6.0)
  x5  = n_bays            (integer: 3, 4, 5)
  x6  = col_width_mm      (300 to 500)
  x7  = col_depth_mm      (300 to 500)
  x8  = beam_depth_mm     (400 to 600)
  x9  = fc_MPa            (21, 25, 28)
  x10 = fy_MPa            (415)
  x11 = rho_col           (0.01 to 0.03)

Seismic / code:
  x12 = Z                 (0.12, 0.20, 0.28, 0.36)
  x13 = R                 (3.0 — IMRF, constant in your study)
  x14 = soil_SC           (one-hot: 1 or 0)
  x15 = soil_SD           (one-hot: 1 or 0)

Ground motion:
  x16 = ln(Sa)            (log of spectral acceleration)
  x17 = PGA               (peak ground acceleration of record)
  x18 = scale_factor      (applied to record)

Target:
  y   = ln(PIDR)
```

**Model performance metrics:**
```
R²   = 1 - Σ(yi - ŷi)² / Σ(yi - ȳ)²    → closer to 1.0 = better
RMSE = √[ (1/n) Σ(yi - ŷi)² ]           → smaller = better
MAE  = (1/n) Σ|yi - ŷi|                  → smaller = better
```

**SHAP (SHapley Additive exPlanations):**
```
Each feature gets a SHAP value = its contribution to the prediction.
Positive SHAP → feature pushes PIDR higher.
Negative SHAP → feature pushes PIDR lower.
Mean |SHAP| → global feature importance ranking.
```

---

## PHASE 0 — ENVIRONMENT SETUP *(Week 1)*

> **Beginner Note:** Do these steps in exact order. Do not skip.
> The most important thing: you MUST use Python 3.12, not 3.13 or 3.14.

### Checklist

- [ ] **Step 1:** Uninstall Python 3.14 OR keep it separate
- [ ] **Step 2:** Download Python 3.12 from https://www.python.org/downloads/release/python-31210/
  - Click: "Windows installer (64-bit)"
  - During install: ✅ Check "Add Python to PATH"
- [ ] **Step 3:** Verify in PowerShell: `py -0` — you should see `-3.12` listed
- [ ] **Step 4:** Create your project folder
  ```
  C:\Users\Asus\Desktop\Research\imrf_bnbc2020\
  ```
- [ ] **Step 5:** Open that folder in VS Code: File → Open Folder
- [ ] **Step 6:** Open VS Code terminal (Ctrl + `) and run:
  ```powershell
  py -3.12 -m venv .venv
  .venv\Scripts\Activate.ps1
  python --version   # Must show Python 3.12.x
  ```
- [ ] **Step 7:** Install all packages:
  ```powershell
  pip install openseespy numpy pandas matplotlib scipy scikit-learn xgboost shap joblib seaborn jupyter
  ```
- [ ] **Step 8:** Test OpenSeesPy:
  ```powershell
  python -c "import openseespy.opensees as ops; ops.wipe(); print('OpenSeesPy OK')"
  ```
- [ ] **Step 9:** Set VS Code interpreter:
  `Ctrl+Shift+P` → "Python: Select Interpreter" → choose `.venv (Python 3.12)`
- [ ] **Step 10:** Create folder structure:
  ```
  imrf_bnbc2020/
  ├── models/
  ├── analysis/
  ├── ground_motions/records/
  ├── data/raw/  data/processed/
  ├── ml/
  ├── plots/figures/
  └── main.py
  ```

**Phase 0 complete when:** `python -c "import openseespy.opensees as ops; print('OK')"` prints `OK`

---

## PHASE 1 — LITERATURE REVIEW *(Weeks 1–2)*

> **Beginner Note:** You need to read 10–15 papers and write 400 words about
> what they found and what they MISSED. The gap they missed = your paper's reason to exist.

### Papers to Read (in priority order)

| Priority | Paper | Why Read It |
|----------|-------|------------|
| ⭐⭐⭐⭐⭐ | Kazemi et al. 2023 (Archives Civil Eng.) | Closest to your study — IDA + ML for RC frames |
| ⭐⭐⭐⭐⭐ | Kazemi et al. 2024 (Eng. App. AI) | ML fragility with Python — your pipeline blueprint |
| ⭐⭐⭐⭐⭐ | BNBC 2020, Part VI, Chapter 2 | Your code — read the seismic provisions section |
| ⭐⭐⭐⭐⭐ | Mahi et al. 2025 (ResearchGate) | Bangladesh BNBC 2020 ETABS study — shows the gap |
| ⭐⭐⭐⭐ | Vamvatsikos & Cornell 2002 | Original IDA paper — you must cite this |
| ⭐⭐⭐⭐ | Momin et al. 2024 (Springer) | Bangladesh RC building seismic evaluation |
| ⭐⭐⭐⭐ | Rahman et al. 2026 (AJCE) | BNBC 2020 + ETABS — no ML, that's your gap |
| ⭐⭐⭐ | Mangalathu et al. 2020 (Eng. Structures) | ML for seismic fragility |
| ⭐⭐⭐ | Steel diagrid ML paper 2025 (Mech. Res. Comm.) | Shows ML surrogate for drift is publishable |
| ⭐⭐⭐ | FEMA 356 (2000) | Performance levels IO/LS/CP definitions |

### Literature Gap Statement (template — fill in and use in your paper)

```
"Several studies have applied machine learning to predict seismic drift of RC
special moment frames [Kazemi 2023, 2024; Mangalathu 2020], and recent studies
have evaluated RC building performance under BNBC 2020 using linear/nonlinear
analysis [Mahi 2025; Rahman 2026]. However, to the best of the authors'
knowledge, no study has:
  (1) focused on RC Intermediate Moment Frames (IMRF, R=3.0), which
      represent the dominant construction typology in Bangladesh;
  (2) developed ML surrogate models trained on OpenSeesPy IDA data
      specifically calibrated to BNBC 2020 seismic demands; or
  (3) compared seismic fragility across all four BNBC 2020 seismic zones.
This study addresses these gaps."
```

### Phase 1 Checklist
- [ ] Read all ⭐⭐⭐⭐⭐ papers
- [ ] Read at least 5 of the ⭐⭐⭐⭐ papers
- [ ] Write your gap statement (use template above as starting point)
- [ ] Save all papers as PDFs in a `references/` folder

---

## PHASE 2 — STRUCTURAL MODELLING PLAN *(Weeks 2–4)*

### 2.1 Your Building Archetypes — Full Parametric Matrix

**Design rules (IMRF-specific):**
- Column reinforcement ratio: ρ = 1.5% to 2.5%
- Beam reinforcement ratio: ρ = 1.0% to 2.0%
- Minimum column size per BNBC 2020: b ≥ 300mm
- Column-to-beam strength ratio ≥ 1.2 (IMRF requirement)

| ID | Stories | H (m) | Bay W (m) | Cols (mm) | Beams (mm) | f'c | Zone |
|----|---------|-------|-----------|-----------|-----------|-----|------|
| A01 | 4 | 12.0 | 5.0 | 300×300 | 250×400 | 21 | All 4 |
| A02 | 6 | 18.0 | 5.0 | 350×350 | 275×450 | 21 | All 4 |
| A03 | 8 | 24.0 | 5.0 | 400×400 | 300×500 | 25 | All 4 |
| A04 | 10 | 30.0 | 5.0 | 400×400 | 300×500 | 25 | All 4 |
| A05 | 12 | 36.0 | 5.0 | 450×450 | 300×550 | 28 | All 4 |
| A06 | 4 | 12.0 | 6.0 | 300×300 | 250×400 | 21 | All 4 |
| A07 | 6 | 18.0 | 6.0 | 350×350 | 275×450 | 25 | All 4 |
| A08 | 8 | 24.0 | 6.0 | 400×400 | 300×500 | 25 | All 4 |
| A09 | 10 | 30.0 | 6.0 | 450×450 | 300×550 | 28 | All 4 |
| A10 | 12 | 36.0 | 6.0 | 500×500 | 300×600 | 28 | All 4 |

**Total unique models: 10 archetypes × 4 zones = 40 models**
*(Zones modelled via different seismic mass/demand, not different geometry)*

### 2.2 Material Properties

| Material | Parameter | Value | Unit | OpenSeesPy Arg |
|----------|-----------|-------|------|----------------|
| Confined concrete | fcc | 1.3 × f'c | MPa | first arg of Concrete02 |
| Confined concrete | εcc | 0.004 | — | second arg |
| Confined concrete | fcr (residual) | 0.2 × fcc | MPa | third arg |
| Confined concrete | εcu | 0.020 | — | fourth arg |
| Unconfined concrete | fc | as designed | MPa | first arg |
| Unconfined concrete | εco | 0.002 | — | second arg |
| Rebar | fy | 415 | MPa | first arg of Steel02 |
| Rebar | Es | 200,000 | MPa | second arg |
| Rebar | b (hardening) | 0.01 | — | third arg |

### 2.3 BNBC 2020 Loads

```
Floor dead load:      3.5 kN/m²  (slab + finishes + MEP)
Floor live load:      2.0 kN/m²  (residential)
Parapet/wall load:    10.0 kN/m  (running on beams)
Story height:         3.0 m (all stories)

Seismic weight per floor:
  W_floor = (DL + 0.25×LL) × tributary area
           = (3.5 + 0.25×2.0) × (bay_width²) × (n_bays+1)

Mass per node (for OpenSeesPy):
  m_node = W_floor / [(n_bays+1) × 9.81]   (in tonnes = kN·s²/m)
```

### 2.4 OpenSeesPy Modelling Assumptions Table
*(Include this as Table 2 in your paper)*

| Assumption | Choice Made | Reason | Limitation? |
|-----------|-------------|--------|------------|
| Model dimension | 2D planar | Standard for parametric IDA | Yes — no torsion |
| Element type | forceBeamColumn | Distributed plasticity | No |
| Integration points | 5 per element | Balance accuracy/speed | No |
| Joint model | Rigid (no panel zone) | Simplification | Note in paper |
| Foundation | Fixed base | Conservative | Note in paper |
| Damping | 5% Rayleigh (modes 1+3) | Standard RC | No |
| P-Delta | Included (PDelta transf.) | Required >5 stories | No |
| Slab | Not modelled | Standard 2D assumption | Note in paper |

### Phase 2 Checklist
- [ ] Code `BuildingParams` class with all 10 archetypes
- [ ] Code `RCFrameModel` class — nodes, materials, sections, elements
- [ ] Run gravity analysis for archetype A03 — check it converges
- [ ] Run modal analysis — verify T1 is within ±20% of BNBC approximate period
- [ ] Verify by hand: column axial load from gravity ≈ W_floor × n_stories / (n_bays+1)
- [ ] Expand to parametric loop for all 10 archetypes

---

## PHASE 3 — GROUND MOTION PLAN *(Week 3)*

### 3.1 How to Get Ground Motion Records

**Option A — PEER NGA West2 (recommended, free):**
1. Go to: https://ngawest2.berkeley.edu
2. Register for a free account
3. Search with these filters:
   - Magnitude: 6.0 – 7.5
   - Rjb distance: 20 – 150 km
   - Vs30: 180 – 360 m/s (corresponds to soil SD)
4. Download acceleration time histories as .AT2 files
5. Convert .AT2 to plain text columns using Python

**Option B — Synthetic records (if no PEER access):**
Use the `generate_synthetic_gm()` function from the framework code.
This is acceptable for a first paper if you clearly state it as a limitation.

### 3.2 Recommended Records

| # | Record Name | Event | Mw | Rjb (km) | PGA (g) | Use for |
|---|-------------|-------|----|----------|---------|---------|
| 1 | El Centro | Imperial Valley 1940 | 6.9 | 12 | 0.31 | All zones |
| 2 | Kobe TAZ090 | Kobe 1995 | 6.9 | 22 | 0.27 | Zone 3, 4 |
| 3 | Chi-Chi TCU045 | Chi-Chi 1999 | 7.6 | 45 | 0.51 | Zone 4 |
| 4 | Northridge Canoga | Northridge 1994 | 6.7 | 15 | 0.42 | Zone 3, 4 |
| 5 | Loma Prieta Gilroy | Loma Prieta 1989 | 6.9 | 32 | 0.36 | Zone 2, 3 |
| 6 | Duzce | Turkey 1999 | 7.2 | 14 | 0.31 | Zone 3, 4 |
| 7 | Cape Mendocino | 1992 | 7.0 | 18 | 0.59 | Zone 4 |
| 8–15 | Select 8 more from PEER | various | 6–7.5 | 20–150 | — | All zones |

**Minimum: 10 records. Target: 15 records.**

### 3.3 Scaling Procedure (Python)

```python
import numpy as np
from scipy.interpolate import interp1d

def scale_gm_to_bnbc(accel, dt, T1, zone='Zone2', soil='SD'):
    """
    Compute scale factor to match BNBC 2020 Sa(T1).
    Returns scaled acceleration array.
    """
    # Compute record response spectrum
    Sa_record, T_arr = compute_response_spectrum(accel, dt)

    # Compute BNBC 2020 target Sa at T1
    _, Sa_target, _ = bnbc2020_design_spectrum(Z_dict[zone], soil)
    f_target = interp1d(T_arr, Sa_target)
    Sa_T1_target = float(f_target(T1))

    # Compute record Sa at T1
    f_record = interp1d(T_arr, Sa_record)
    Sa_T1_record = float(f_record(T1))

    # Scale factor
    SF = Sa_T1_target / Sa_T1_record
    return accel * SF, SF
```

### Phase 3 Checklist
- [ ] Obtain minimum 10 ground motion records (PEER NGA or synthetic)
- [ ] Convert all records to two-column format: [time, accel_in_g]
- [ ] Write `load_ground_motion(filepath)` function in Python
- [ ] Scale at least one record to BNBC 2020 Zone 2 spectrum and plot to verify

---

## PHASE 4 — IDA CAMPAIGN *(Weeks 5–7)*

> **Beginner Note:** IDA is a loop inside a loop inside a loop.
> For each building → for each ground motion → for each scale factor →
> run one nonlinear time history analysis and record PIDR.

### 4.1 Scale Factor Strategy

```
Minimum scale factors (15 levels):
SF = [0.05, 0.10, 0.20, 0.30, 0.40, 0.50, 0.60, 0.80,
      1.00, 1.25, 1.50, 1.75, 2.00, 2.50, 3.00]

Stop when: PIDR ≥ 8.0% (IMRF collapse threshold)
```

### 4.2 Dataset Size Estimate

```
10 archetypes × 4 zones × 12 GMs × 15 SFs = 7,200 analysis runs
Minus ~20% collapses = ~5,760 non-collapse data points ✓

This exceeds the 5,000 minimum for ML training.
```

### 4.3 Convergence Strategy (Beginner-Friendly)

```python
def run_one_nltha(ops_model, dt, accel, SF):
    """
    Run one nonlinear time history analysis.
    Returns PIDR and convergence status.
    """
    accel_scaled = accel * SF

    # Setup analysis
    ops.constraints('Plain')
    ops.numberer('RCM')
    ops.system('UmfPack')
    ops.test('EnergyIncr', 1e-8, 200, 0)
    ops.algorithm('KrylovNewton')
    ops.integrator('Newmark', 0.5, 0.25)
    ops.analysis('Transient')

    max_pidr = 0.0
    dt_run = dt / 2.0   # use half the record dt for stability

    for step in range(int(len(accel) * dt / dt_run)):
        ok = ops.analyze(1, dt_run)

        # If not converged, try smaller steps
        if ok != 0:
            for smaller_dt in [dt_run/2, dt_run/4, dt_run/8]:
                ok = ops.analyze(1, smaller_dt)
                if ok == 0:
                    break

        if ok != 0:
            return max_pidr, False   # non-convergence = treat as collapse

        pidr = compute_current_pidr()   # your PIDR function
        max_pidr = max(max_pidr, pidr)

        if max_pidr >= 0.08:   # IMRF collapse threshold
            return max_pidr, True

    return max_pidr, True
```

### 4.4 Parallel Execution (Speed Up Analyses)

```python
from joblib import Parallel, delayed

# Build all task combinations
tasks = [
    (archetype, gm, sf)
    for archetype in building_list     # 10 × 4 zones = 40 models
    for gm in ground_motion_list       # 12 records
    for sf in SCALE_FACTORS            # 15 levels
]

# Run in parallel using all CPU cores
results = Parallel(n_jobs=-1, verbose=10)(
    delayed(run_single_analysis)(arch, gm, sf)
    for arch, gm, sf in tasks
)

# n_jobs=-1 uses all available CPU cores automatically
# verbose=10 prints progress so you know it's running
```

> **Beginner Note on time:** With n_jobs=-1, a 6-core laptop running
> 7,200 analyses of 2D frames should take 2–6 hours total.
> Start it running, go do something else.

### Phase 4 Checklist
- [ ] Test single analysis run: 1 building, 1 GM, 1 SF
- [ ] Verify PIDR output is reasonable (0.1%–5% for design-level shaking)
- [ ] Add convergence fallback (smaller dt)
- [ ] Add collapse detection (PIDR ≥ 8%)
- [ ] Run 5 test analyses — check results make physical sense
- [ ] Run full IDA campaign (parallel)
- [ ] Save all results to `data/raw/ida_results_raw.csv`
- [ ] Check dataset: count rows, check for NaN, check PIDR range

---

## PHASE 5 — DATASET & EDA *(Week 7)*

### 5.1 Final Dataset Schema

Your `ida_master_dataset.csv` should have these columns:

```
building_id, zone, soil_class, n_stories, H_total, T1,
bay_width, n_bays, col_b_mm, col_h_mm, beam_h_mm,
fc_MPa, fy_MPa, rho_col,
Z, R, I,
gm_name, SF, Sa_T1, PGA,
ln_Sa, PIDR, ln_PIDR, collapsed
```

### 5.2 Cleaning Steps

```python
import pandas as pd
import numpy as np

df = pd.read_csv('data/raw/ida_results_raw.csv')

# Step 1: Remove collapse runs from ML dataset
# (keep for fragility but not for drift prediction training)
df_ml = df[df['collapsed'] == 0].copy()

# Step 2: Remove physically impossible values
df_ml = df_ml[df_ml['PIDR'] > 0.0001]    # remove near-zero
df_ml = df_ml[df_ml['PIDR'] < 0.08]      # remove above collapse threshold
df_ml = df_ml[df_ml['Sa_T1'] > 0.0]      # remove bad GM runs

# Step 3: Log-transform target and IM
df_ml['ln_PIDR'] = np.log(df_ml['PIDR'])
df_ml['ln_Sa']   = np.log(df_ml['Sa_T1'])

# Step 4: Check dataset size
print(f"Total rows: {len(df_ml)}")        # target: > 5000
print(f"Features: {df_ml.shape[1]}")
print(df_ml.describe())

df_ml.to_csv('data/processed/ida_ml_dataset.csv', index=False)
```

### 5.3 Exploratory Data Analysis (EDA)

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Plot 1: IDA curves for one building
# Plot 2: Distribution of PIDR (should be right-skewed → log-normal)
# Plot 3: Distribution of ln(PIDR) (should be roughly normal)
# Plot 4: Correlation heatmap of all features
# Plot 5: PIDR vs Sa coloured by zone
# Plot 6: PIDR vs n_stories (box plot)
```

### Phase 5 Checklist
- [ ] Load raw CSV — check row count matches expected ~7,200
- [ ] Remove collapse runs — keep for fragility, remove from ML
- [ ] Log-transform PIDR and Sa
- [ ] Generate and save all 6 EDA plots
- [ ] Save clean ML dataset as `ida_ml_dataset.csv`
- [ ] Confirm dataset has ≥ 5,000 rows after cleaning

---

## PHASE 6 — MACHINE LEARNING *(Weeks 8–9)*

> **Beginner Note:** If you're new to scikit-learn, work through the
> official tutorial first: https://scikit-learn.org/stable/tutorial/
> Spend 2–3 hours on it before writing your ML code.

### 6.1 Train/Test Split

```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

FEATURES = [
    'n_stories', 'H_total', 'T1', 'bay_width', 'n_bays',
    'col_b_mm', 'col_h_mm', 'beam_h_mm', 'fc_MPa', 'rho_col',
    'Z', 'R', 'ln_Sa', 'PGA',
    'soil_SC', 'soil_SD'    # one-hot encoded
]

# One-hot encode soil class
df = pd.get_dummies(df_ml, columns=['soil_class'], prefix='soil')

X = df[FEATURES]
y = df['ln_PIDR']

# Stratify by zone to ensure all zones represented in test set
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.20, random_state=42,
    stratify=df['zone']   # ensure all zones in both sets
)

# Scale features (important for ANN and LR)
scaler = StandardScaler()
X_train_sc = scaler.fit_transform(X_train)
X_test_sc  = scaler.transform(X_test)   # NEVER fit on test set
```

### 6.2 Model Training Order

**Train in this order — beginner tip: verify each model works before the next.**

```python
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor
from xgboost import XGBRegressor
from sklearn.neural_network import MLPRegressor
from sklearn.metrics import r2_score, mean_squared_error, mean_absolute_error

def evaluate_model(model, X_tr, X_te, y_tr, y_te, name):
    model.fit(X_tr, y_tr)
    y_pred = model.predict(X_te)
    r2   = r2_score(y_te, y_pred)
    rmse = np.sqrt(mean_squared_error(y_te, y_pred))
    mae  = mean_absolute_error(y_te, y_pred)
    print(f"{name:25} R²={r2:.4f}  RMSE={rmse:.4f}  MAE={mae:.4f}")
    return model, y_pred, r2, rmse

# 1. Baseline — Linear Regression (use scaled features)
lr,  y_lr,  r2_lr  = evaluate_model(LinearRegression(),
                     X_train_sc, X_test_sc, y_train, y_test, 'Linear Regression')

# 2. Random Forest (does NOT need scaling)
rf,  y_rf,  r2_rf  = evaluate_model(
    RandomForestRegressor(n_estimators=300, n_jobs=-1, random_state=42),
    X_train, X_test, y_train, y_test, 'Random Forest')

# 3. XGBoost (does NOT need scaling)
xgb, y_xgb, r2_xgb = evaluate_model(
    XGBRegressor(n_estimators=400, learning_rate=0.05,
                 max_depth=6, random_state=42, verbosity=0),
    X_train, X_test, y_train, y_test, 'XGBoost')

# 4. ANN (use scaled features)
ann, y_ann, r2_ann = evaluate_model(
    MLPRegressor(hidden_layer_sizes=(128,64,32), max_iter=1000,
                 early_stopping=True, random_state=42),
    X_train_sc, X_test_sc, y_train, y_test, 'ANN (MLP)')
```

### 6.3 Expected Results Table for Paper

| Model | R² | RMSE | MAE | Notes |
|-------|----|------|-----|-------|
| Linear Regression | ~0.75 | ~0.35 | ~0.27 | Baseline only |
| Random Forest | ~0.94 | ~0.12 | ~0.09 | Strong |
| XGBoost | ~0.96 | ~0.10 | ~0.07 | Best expected |
| ANN (MLP) | ~0.93 | ~0.13 | ~0.10 | Close second |

*Your actual values will differ — report whatever you get honestly.*

### 6.4 SHAP Analysis

```python
import shap

# Use best model (likely XGBoost or RF)
best_model = xgb   # or rf, depending on results

explainer   = shap.TreeExplainer(best_model)
shap_values = explainer.shap_values(X_test)

# Figure 8: Beeswarm plot (shows direction of each feature's effect)
plt.figure(figsize=(10, 8))
shap.summary_plot(shap_values, X_test,
                  feature_names=FEATURES,
                  show=False)
plt.tight_layout()
plt.savefig('plots/figures/fig08_shap_beeswarm.png', dpi=300)

# Figure 9: Bar plot (shows global importance ranking)
shap.summary_plot(shap_values, X_test,
                  plot_type='bar',
                  feature_names=FEATURES,
                  show=False)
plt.savefig('plots/figures/fig09_shap_bar.png', dpi=300)
```

### Phase 6 Checklist
- [ ] One-hot encode soil class
- [ ] 80/20 train/test split (stratified by zone)
- [ ] Scale features (StandardScaler)
- [ ] Train Linear Regression — record R², RMSE
- [ ] Train Random Forest — record R², RMSE
- [ ] Train XGBoost — record R², RMSE
- [ ] Train ANN — record R², RMSE
- [ ] 5-fold cross-validation on best model
- [ ] Generate and save predicted vs actual scatter plot (4 subplots)
- [ ] Run SHAP analysis — save beeswarm and bar plots

---

## PHASE 7 — FRAGILITY CURVES *(Week 9)*

### Fragility Curve Python Code

```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

# Performance thresholds for IMRF
THRESHOLDS = {
    'Immediate Occupancy': 0.007,   # 0.7%
    'Life Safety':         0.015,   # 1.5%
    'Collapse Prevention': 0.030,   # 3.0%
}
COLORS = {
    'Immediate Occupancy': '#27ae60',
    'Life Safety':         '#f39c12',
    'Collapse Prevention': '#e74c3c',
}

def compute_and_plot_fragility(df_zone, zone_label, save_path):
    Sa   = df_zone['Sa_T1'].values
    PIDR = df_zone['PIDR'].values

    # Fit cloud regression
    ln_Sa   = np.log(Sa)
    ln_PIDR = np.log(PIDR)
    b, a, r, _, _ = stats.linregress(ln_Sa, ln_PIDR)
    residuals = ln_PIDR - (a + b * ln_Sa)
    beta = np.std(residuals)

    Sa_range = np.linspace(0.01, 3.0, 300)

    fig, ax = plt.subplots(figsize=(9, 6))
    for level, threshold in THRESHOLDS.items():
        theta = np.exp((np.log(threshold) - a) / b)
        Pf = stats.norm.cdf((np.log(Sa_range) - np.log(theta)) / beta)
        ax.plot(Sa_range, Pf, lw=2.5,
                color=COLORS[level], label=f'{level} (θ={theta:.3f}g)')
        ax.axvline(theta, color=COLORS[level], ls=':', lw=1, alpha=0.6)

    ax.set_xlabel('Sa(T₁, 5%) [g]', fontsize=12)
    ax.set_ylabel('Probability of Exceedance', fontsize=12)
    ax.set_title(f'Seismic Fragility — RC IMRF | {zone_label} | BNBC 2020',
                 fontsize=12, fontweight='bold')
    ax.legend(fontsize=10)
    ax.grid(True, alpha=0.3)
    ax.yaxis.set_major_formatter(
        plt.FuncFormatter(lambda y, _: f'{y:.0%}'))
    plt.tight_layout()
    plt.savefig(save_path, dpi=300, bbox_inches='tight')
    plt.close()
    print(f'Saved: {save_path}')

# Generate for all 4 zones
for zone, label in [('Zone1','Rajshahi Z=0.12'), ('Zone2','Dhaka Z=0.20'),
                    ('Zone3','Chittagong Z=0.28'), ('Zone4','Sylhet Z=0.36')]:
    df_z = df[df['zone'] == zone]
    compute_and_plot_fragility(
        df_z, label,
        f'plots/figures/fig05_fragility_{zone.lower()}.png'
    )
```

### Phase 7 Checklist
- [ ] Generate fragility curves for all 4 BNBC zones separately
- [ ] Generate zone comparison plot (4 curves on one figure at LS level)
- [ ] Record θ and β values for Table 5 of paper
- [ ] Verify: Zone 4 (Sylhet) has highest fragility — if not, check your data

---

## PHASE 8 — WRITING THE PAPER *(Weeks 10–13)*

> **Beginner Note:** Write one section per sitting. Do not try to write
> the whole paper at once. 500 words per day = finished in 12 days.

### Writing Order (follow this exactly)

```
Day 1–2:   Section 2 — Building Models
           (you know this material best, easiest to start)

Day 3–4:   Section 3 — OpenSeesPy Methodology
           (describe your code structure + assumptions table)

Day 5–6:   Section 4 — Ground Motions and IDA
           (describe records + scaling + procedure)

Day 7–8:   Section 5 — ML Framework
           (describe features + models + training)

Day 9–12:  Section 6 — Results
           (describe all figures, all tables, discuss findings)

Day 13:    Section 7 — Conclusions
           (5–7 bullet findings + 3–4 future work suggestions)

Day 14–15: Section 1 — Introduction
           (now you know your results, write intro to match)

Day 16:    Abstract
           (last — summarise everything in 250 words)
```

### Key Things to Include in Section 6 (Results)

```
6.1 IDA curves (2–3 paragraphs):
  - Describe shape of IDA curves
  - Comment on dispersion between records
  - Compare 4-story vs 12-story response

6.2 Fragility curves (3–4 paragraphs):
  - Present θ and β values for all zones
  - Compare zones: Zone 4 has lowest θ = most vulnerable
  - Compare IO vs LS vs CP: how they spread apart
  - If possible: compare with any existing study

6.3 ML results (3–4 paragraphs):
  - Present R², RMSE table for all 4 models
  - Describe why best model outperforms others
  - Show predicted vs actual scatter plot
  - Report cross-validation score

6.4 SHAP (2–3 paragraphs):
  - List top 3 features: expected = ln(Sa), T1, Z
  - Explain physical meaning of each
  - Discuss any unexpected findings
```

### Phase 8 Checklist
- [ ] Section 2 drafted
- [ ] Section 3 drafted
- [ ] Section 4 drafted
- [ ] Section 5 drafted
- [ ] Section 6 drafted
- [ ] Section 7 drafted
- [ ] Section 1 drafted
- [ ] Abstract drafted
- [ ] All figures numbered and captioned
- [ ] All tables complete
- [ ] References formatted (use Mendeley/Zotero export)

---

## PHASE 9 — SUBMISSION *(Week 14)*

### Pre-Submission Checklist

- [ ] Similarity check < 15% (use iThenticate or university tool)
- [ ] Check all figure captions are complete
- [ ] Check all table titles are complete
- [ ] Check all equations are numbered
- [ ] Check all references cited in text
- [ ] Format to MDPI template: https://www.mdpi.com/authors/latex
- [ ] Write cover letter (template below)
- [ ] Upload to: https://susy.mdpi.com

### Cover Letter Template

```
Dear Editor,

We submit our manuscript titled:
"[Your title]"
for consideration in MDPI Buildings.

This study presents [one sentence summary].
To the best of our knowledge, this is the first study to [your novelty].

Key contributions:
1. [Contribution 1]
2. [Contribution 2]
3. [Contribution 3]

The manuscript has not been submitted elsewhere and all authors
have approved the submission.

Sincerely,
[Your name]
[Institution]
[Email]
```

---

## OPENSEESPY CODING ROADMAP

### Learning Path for Beginners (in order)

```
Week 1:  Run the 2-story example from the crash course widget
         → just copy, paste, run, understand each line

Week 2:  Add a for loop to create 3-story and 5-story versions
         → change n_stories only, verify periods change

Week 3:  Add gravity analysis → verify column loads by hand calc

Week 3:  Add modal analysis → print T1 for each building

Week 4:  Add a basic static pushover analysis
         → apply lateral loads, record roof displacement

Week 5:  Add one nonlinear time history analysis (1 GM, no scaling)
         → record PIDR at each step

Week 6:  Add IDA: loop over scale factors for one building × one GM
         → plot IDA curve

Week 7:  Add parallel: loop over all buildings × all GMs
         → collect all results in a DataFrame
```

### Critical Beginner Mistakes to Avoid

| Mistake | Consequence | How to Avoid |
|---------|-------------|-------------|
| Not calling `ops.wipe()` first | Old model bleeds into new | Always start every function with `ops.wipe()` |
| Wrong units (mixing MPa with m) | Wrong results, no error | Pick ONE unit system and stick to it |
| Setting mass to 0.0 | Division by zero in eigen | Use 1e-9 not 0 |
| Skipping gravity before dynamic | Unrealistic dynamic response | Always run gravity + `loadConst` first |
| Using Python 3.14 | Import fails | Use Python 3.12 only |
| Fitting scaler on test set | Data leakage, inflated R² | `fit_transform` on train, `transform` on test |

---

## FIGURES & TABLES CHECKLIST

### Figures (9 required)

| # | Description | Script | Status |
|---|-------------|--------|--------|
| Fig. 1 | BNBC 2020 spectra — all 4 zones (SD soil) | `plot_spectra.py` | ☐ |
| Fig. 2 | OpenSeesPy 2D IMRF model schematic + fiber section | hand-drawn / Inkscape | ☐ |
| Fig. 3 | IDA curves — 10-story IMRF, Zone 2, all GMs | `plot_ida_curves.py` | ☐ |
| Fig. 4 | IDA comparison — 4 vs 8 vs 12 stories (Zone 2) | `plot_ida_curves.py` | ☐ |
| Fig. 5 | Fragility curves — IO/LS/CP — Zone 2 Dhaka | `plot_fragility.py` | ☐ |
| Fig. 6 | Fragility comparison at LS — all 4 zones | `plot_fragility.py` | ☐ |
| Fig. 7 | Predicted vs Actual PIDR — all 4 models (2×2) | `plot_ml_results.py` | ☐ |
| Fig. 8 | SHAP beeswarm plot | `shap_analysis.py` | ☐ |
| Fig. 9 | SHAP dependence: ln(Sa) and T1 | `shap_analysis.py` | ☐ |

### Tables (5 required)

| # | Description | Section | Status |
|---|-------------|---------|--------|
| Table 1 | Building archetype matrix (10 models) | §2 | ☐ |
| Table 2 | OpenSeesPy modelling assumptions | §3 | ☐ |
| Table 3 | Ground motion record details | §4 | ☐ |
| Table 4 | ML model performance: R², RMSE, MAE | §5–6 | ☐ |
| Table 5 | Fragility parameters θ and β — all zones × all levels | §6 | ☐ |

---

## TIMELINE

| Week | Phase | Key Output |
|------|-------|-----------|
| 1 | Phase 0: Setup + start literature | Python 3.12 + OpenSeesPy working |
| 2 | Phase 1: Literature + Phase 2 start | Gap statement written |
| 3 | Phase 2: Single building model | Modal period verified |
| 4 | Phase 2: Parametric building loop | 10 archetypes coded |
| 5 | Phase 3: Ground motions + Phase 4 start | 10–15 GMs scaled |
| 6 | Phase 4: IDA development | Single IDA curve working |
| 7 | Phase 4: Full IDA campaign | ~7,200 analyses complete |
| 8 | Phase 5: Dataset + EDA | Clean CSV + 6 EDA plots |
| 9 | Phase 6 + 7: ML + Fragility | All results ready |
| 10 | Phase 8: Writing Sections 2–5 | 3,000 words drafted |
| 11 | Phase 8: Writing Section 6 | Results section drafted |
| 12 | Phase 8: Writing Sections 1, 7, Abstract | Full draft complete |
| 13 | Phase 9 prep: Review + format | Similarity check done |
| 14 | Phase 9: Submit | Submitted to MDPI Buildings |

---

## TOOLS STACK

### Required (install first)

```bash
# Python 3.12 — download from python.org/downloads/release/python-31210/

# After creating venv with Python 3.12:
pip install openseespy          # structural FEM
pip install numpy pandas        # data handling
pip install matplotlib seaborn  # plotting
pip install scipy               # statistics and fragility
pip install scikit-learn        # ML models
pip install xgboost             # XGBoost
pip install shap                # SHAP analysis
pip install joblib              # parallel computing
pip install jupyter             # notebook for EDA
```

### Free Online Tools

| Tool | Purpose | Link |
|------|---------|------|
| PEER NGA West2 | Ground motion records | ngawest2.berkeley.edu |
| Mendeley | Reference manager | mendeley.com |
| MDPI Author Services | Journal template | mdpi.com/authors |
| GitHub | Code version control | github.com |
| Zenodo | Dataset publication | zenodo.org |

---

## RISK REGISTER

| Risk | How Likely | How Bad | Your Action |
|------|-----------|---------|-------------|
| OpenSeesPy won't install | HIGH right now | High | Install Python 3.12 first — this is solved |
| IDA analyses don't converge | Medium | Medium | Use adaptive dt; classify as collapse if all fail |
| ML accuracy too low (R² < 0.85) | Low | High | Add more building variants; try ensemble models |
| Dataset too small | Low | High | Add more scale factors or GM records |
| PEER NGA access denied | Low | Low | Use synthetic GMs; clearly state as limitation |
| Writing takes too long | Medium | Medium | Write 500 words/day minimum; skip perfectionism on first draft |
| Journal rejects | Low | Medium | Address reviewer comments; resubmit or try next journal |

---

## QUICK REFERENCE — ALL EQUATIONS

```
BNBC 2020 Spectrum:
  SDS  = (2/3) × Fa × 2.5 × Z
  SD1  = (2/3) × Fv × Z
  T0   = 0.2 × SD1/SDS
  Ts   = SD1/SDS

Approximate period:
  T    = 0.0466 × H^0.90

IMRF base shear:
  V    = [Sa(T)/3.0] × 1.0 × W       (R=3.0, I=1.0)

Inter-story drift:
  PIDR = |u_i - u_{i-1}| / h_i

Fragility regression:
  ln(PIDR) = a + b × ln(Sa)
  β        = std(residuals)
  θ_LS     = exp[(ln(PIDR_LS) - a) / b]
  P(LS|Sa) = Φ[(ln(Sa) - ln(θ)) / β]

ML target:
  y = ln(PIDR)

ML metrics:
  R²   = 1 - SS_res/SS_tot
  RMSE = √[(1/n)Σ(y - ŷ)²]
  MAE  = (1/n)Σ|y - ŷ|
```

---

> **Final Reminder for Beginners:**
> The most important thing is to keep moving forward.
> A working analysis that is 80% perfect is infinitely better
> than a perfect plan that never gets coded.
> Start with Phase 0 today. The paper will follow.

---

*Tailored for: RC IMRF | All 4 BNBC 2020 Zones | MDPI Buildings | Beginner Level*
*Version 2.0 — Customised | 2025*
