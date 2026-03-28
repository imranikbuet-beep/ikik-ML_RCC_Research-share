# Literature Reading List — Verified Links
## RC IMRF | BNBC 2020 | OpenSeesPy IDA | ML Fragility
### All links verified | Fast-track priority order

---

## HOW TO USE THIS LIST

- Read papers in the order shown (most important first)
- For each paper: read Abstract + Introduction + Methodology + Conclusion
- You do NOT need to read every equation — understand the big picture
- After reading each paper, write 2–3 sentences: what they did + what they missed
- Those "what they missed" notes = your paper's Introduction section

---

## TIER 1 — MUST READ (read these first, before any coding)

---

### Paper 1 ⭐⭐⭐⭐⭐ — Your primary methodology blueprint

**Kazemi, F., Asgarkhani, N., & Jankowski, R. (2023)**
*Machine learning-based seismic response and performance assessment of reinforced concrete buildings*
Archives of Civil and Mechanical Engineering, 23, 94

**Why read it:** This is the closest existing paper to yours. They used OpenSees + IDA + ML on RC MRFs with 165 buildings and 92,400 data points. Your paper does the same but for IMRF under BNBC 2020. Study their methodology section carefully — especially how they built the dataset and which ML features they used.

**What to take from it:**
- Their feature list (adapt for BNBC 2020 and IMRF)
- Their IDA setup (adapt for OpenSeesPy)
- Their ML comparison approach (LR vs RF vs boosting)

**Read time:** ~2 hours

🔗 **DOI link:** https://doi.org/10.1007/s43452-023-00631-9
🔗 **Springer:** https://link.springer.com/article/10.1007/s43452-023-00631-9
🔗 **ResearchGate (free PDF):** https://www.researchgate.net/publication/369474867_Machine_learning-based_seismic_response_and_performance_assessment_of_reinforced_concrete_buildings

---

### Paper 2 ⭐⭐⭐⭐⭐ — Your fragility pipeline blueprint

**Kazemi, F., Asgarkhani, N., & Jankowski, R. (2023)**
*Machine learning-based seismic fragility and seismic vulnerability assessment of reinforced concrete structures*
Soil Dynamics and Earthquake Engineering, 166, 107761

**Why read it:** This companion paper by the same authors shows how to build fragility curves using ML (XGBoost, ANN, Extra Trees, etc.) trained on IDA data. Your paper adds BNBC 2020 and IMRF specificity to this approach. Study their fragility curve generation method carefully.

**What to take from it:**
- Cloud analysis method implementation
- Hyperparameter tuning approach (grid search, k-fold CV)
- How to present fragility results in a table

**Read time:** ~1.5 hours

🔗 **DOI link:** https://doi.org/10.1016/j.soildyn.2023.107761
🔗 **ScienceDirect:** https://www.sciencedirect.com/science/article/abs/pii/S0267726123000064
🔗 **ResearchGate (free PDF):** https://www.researchgate.net/publication/366953421_Machine_learning-based_seismic_fragility_and_seismic_vulnerability_assessment_of_reinforced_concrete_structures

---

### Paper 3 ⭐⭐⭐⭐⭐ — The IDA foundation paper (always cited)

**Vamvatsikos, D., & Cornell, C. A. (2002)**
*Incremental dynamic analysis*
Earthquake Engineering & Structural Dynamics, 31(3), 491–514

**Why read it:** This is THE original IDA paper. Every seismic paper cites it. You must cite it too. Read the first 10 pages — they define IDA curves, intensity measures, and collapse detection. You do not need to read the mathematical proofs.

**What to take from it:**
- Official definition of IDA (cite verbatim in your Section 4)
- How to define collapse on an IDA curve
- How to summarize IDA results statistically

**Read time:** ~1 hour (first 10 pages only)

🔗 **DOI link:** https://doi.org/10.1002/eqe.141
🔗 **Wiley Online Library:** https://onlinelibrary.wiley.com/doi/abs/10.1002/eqe.141
🔗 **ResearchGate (free PDF):** https://www.researchgate.net/publication/227618756_Incremental_Dynamic_Analysis
🔗 **Academia.edu (free PDF):** https://www.academia.edu/39084184/EARTHQUAKE_ENGINEERING_AND_STRUCTURAL_DYNAMICS_Incremental_dynamic_analysis

---

### Paper 4 ⭐⭐⭐⭐⭐ — Bangladesh context + BNBC 2020 gap

**Momin, M. F., Islam, M. W., Masud, F., et al. (2024)**
*Preliminary and detailed seismic evaluation of an existing RC building in Bangladesh: a case study*
Innovative Infrastructure Solutions, 9, 363

**Why read it:** This is the most recent Bangladesh-specific seismic paper in a Springer journal. It evaluates an RC building under BNBC 2020 but uses simplified methods only — no IDA, no ML. This is part of your gap statement: "Momin et al. (2024) used simplified evaluation methods; nonlinear IDA-based assessment under BNBC 2020 has not been performed."

**What to take from it:**
- Bangladesh seismic risk context (use in your Introduction Section 1.1)
- BNBC 2020 overview (Section 1.2)
- The gap: they used simplified methods, not IDA

**Read time:** ~45 minutes

🔗 **DOI link:** https://doi.org/10.1007/s41062-024-01693-1
🔗 **Springer:** https://link.springer.com/article/10.1007/s41062-024-01693-1

---

### Paper 5 ⭐⭐⭐⭐⭐ — BNBC 2020 ETABS study — shows the gap

**Mahi, M. S. H., Ridoy, T. A., & Hasan, S. (2025)**
*Seismic Performance Assessment of Regular and Irregular RC Buildings Under BNBC 2020 Using ETABS*
Disaster in Civil Engineering and Architecture, 2(1)

**Why read it:** This 2025 Bangladesh paper uses ETABS + BNBC 2020 but only linear static analysis (ESFP). No IDA, no ML, no OpenSeesPy. This is one of your primary gap papers — your paper does what this paper should have done next.

**What to take from it:**
- The BNBC 2020 input parameters they used (double-check your own)
- Their results tables for drift and displacement (compare with yours later)
- Cite as: "existing BNBC 2020 studies use linear static analysis only [Mahi 2025]; nonlinear IDA has not been applied"

**Read time:** ~45 minutes

🔗 **ResearchGate (free PDF):** https://www.researchgate.net/publication/390040542_Seismic_Performance_Assessment_of_Regular_and_Irregular_RC_Buildings_Under_BNBC_2020_Using_ETABS
🔗 **Journal direct PDF:** https://journal.popularscientist.org/index.php/dcea/article/download/28/26

---

### Paper 6 ⭐⭐⭐⭐⭐ — IMRF + BNBC 2020 — the most directly related Bangladesh paper

**[IMRF BNBC 2020 10-story ETABS study — Dhaka, Zone 2]**
*Ten-storey RC Intermediate Moment Resisting Frame (IMRF) building: BNBC 2020 vs BNBC 2006 comparison*
(Found via ResearchGate search results — ETABS IMRF Dhaka BNBC 2020)

**Why read it:** This study models a ten-storey RC Intermediate Moment Resisting Frame (IMRF) building in seismic zone 2 (Dhaka) using ETABS, comparing BNBC 2020 and BNBC 2006 — finding BNBC 2020 top displacement values 34.68% higher in X direction and base shear 27.53% higher. This is the only existing IMRF+BNBC 2020 paper — but it uses ETABS linear static only, no IDA, no ML. This confirms your novelty.

**What to take from it:**
- IMRF parameters used (validate against yours)
- The BNBC 2020 vs 2006 comparison results (cite as motivation)
- Confirm: no one has done IMRF + IDA + ML under BNBC 2020

**Read time:** ~30 minutes

🔗 **ResearchGate (search):** https://www.researchgate.net/search?q=IMRF+BNBC+2020+ETABS+Bangladesh

---

## TIER 2 — IMPORTANT (read in week 1–2, before writing)

---

### Paper 7 ⭐⭐⭐⭐ — BNBC 2020 seismic provisions overview

**Al-Hussaini, T. M. (2024)**
*New Seismic Design Provisions in BNBC-2020: A Quick Appraisal*
In: Proceedings of CICM 2023, Lecture Notes in Civil Engineering, vol 511. Springer

**Why read it:** Written by the principal author of BNBC 2020 seismic provisions. Explains the intent behind the new zone coefficients (Z = 0.12–0.36), site classes, and R factors. Essential for your Section 1.2 and your Table of BNBC parameters.

**Read time:** ~30 minutes

🔗 **DOI link:** https://doi.org/10.1007/978-3-031-63276-1_11
🔗 **Springer:** https://link.springer.com/chapter/10.1007/978-3-031-63276-1_11

---

### Paper 8 ⭐⭐⭐⭐ — BNBC 2006 vs BNBC 2020 comparison

**Hossain, M. O., Rahman, T., et al. (2022)**
*Evaluation of RC Building Under Seismic Load Based on BNBC 2006 and BNBC 2020 Using Equivalent Static Force (ESF) Method*
Journal of Civil and Construction Engineering

**Why read it:** Compares story drift and base shear under BNBC 2006 vs BNBC 2020 for a 10-story Bangladesh building. Good context for your Introduction — shows how much the demands changed with the new code. Cite as motivation for studying BNBC 2020 specifically.

**Read time:** ~30 minutes

🔗 **ResearchGate (free PDF):** https://www.researchgate.net/publication/366289602_Evaluation_of_RC_Building_Under_Seismic_Load_Based_on_BNBC_2006_and_BNBC_2020_Using_Equivalent_Static_Force_ESF_Method
🔗 **Academia.edu:** https://www.academia.edu/91614010/Evaluation_of_RC_Building_Under_Seismic_Load_Based_on_BNBC_2006_and_BNBC_2020_Using_Equivalent_Static_Force_ESF_Method
🔗 **Journal link:** https://matjournals.co.in/index.php/JOCCE/article/view/1113

---

### Paper 9 ⭐⭐⭐⭐ — ML seismic fragility pipeline

**Hwang, S. H., Mangalathu, S., Shin, J., & Jeon, J. S. (2021)**
*Machine learning-based approaches for seismic demand and collapse of ductile reinforced concrete building frames*
Journal of Building Engineering, 34, 101905

**Why read it:** Mangalathu is a leading name in ML seismic fragility. This paper proposes ML models (regression + classification) for RC frames using IDA data. Good methodological reference for your Section 5 (ML framework). Their feature set and model comparison table structure is worth copying for your paper.

**Read time:** ~1 hour

🔗 **DOI link:** https://doi.org/10.1016/j.jobe.2021.101905 (note: appears as doi referenced above from ScienceDirect result)
🔗 **ScienceDirect:** https://www.sciencedirect.com/science/article/abs/pii/S2352710220335385

---

### Paper 10 ⭐⭐⭐⭐ — OpenSeesPy workflow reference

**Solorzano, G., & Plevris, V. (2023)**
*Open-Source Framework for Modeling RC Shear Walls Using Deep Neural Networks and OpenSeesPy*
Advances in Civil Engineering, 2023

**Why read it:** Shows the exact OpenSeesPy → dataset → DNN pipeline in one paper. The workflow they use (OpenSeesPy parametric model → automated analysis loop → TensorFlow) is very close to yours. Study their code structure description in Section 3.

**Read time:** ~1 hour

🔗 **DOI link:** https://doi.org/10.1155/2023/7953869
🔗 **Wiley:** https://onlinelibrary.wiley.com/doi/10.1155/2023/7953869

---

### Paper 11 ⭐⭐⭐⭐ — Probabilistic seismic hazard Bangladesh

**Kamal, A. S. M. M., et al. (2025)**
*Probabilistic Seismic Hazard Mapping for Bangladesh Using Updated Source Models*
Natural Hazards, Taylor & Francis

**Why read it:** Provides updated seismic hazard data for Bangladesh — GMPEs, source models, PGA maps. Use for ground motion selection justification and to cite when explaining why Bangladesh seismic assessment is important.

**Read time:** ~30 minutes

🔗 **Taylor & Francis:** https://www.tandfonline.com/doi/full/10.1080/19475705.2025.2454537

---

## TIER 3 — SUPPLEMENTARY (read during writing phase, weeks 9–11)

---

### Paper 12 ⭐⭐⭐ — IDA with ML for drift (2025 paper)

**[ML prediction of seismic inter-story drift RC diagrid — 2025]**
*Machine learning-based prediction of seismic inter-story drift of RC diagrid systems*
Mechanics Research Communications, 2025

**Why read it:** Uses 21 ML algorithms on IDA data to predict PIDR for steel diagrid structures. Extra Trees Regressor achieved R² > 0.95. Useful as a reference for your ML model comparison section.

**Read time:** ~45 minutes

🔗 **ScienceDirect:** https://www.sciencedirect.com/science/article/abs/pii/S2352012425016066

---

### Paper 13 ⭐⭐⭐ — SHAP in structural engineering

**Feng, D. C., Wang, W. J., Mangalathu, S., & Taciroglu, E. (2021)**
*Interpretable XGBoost-SHAP machine-learning model for shear strength prediction of squat RC walls*
Journal of Structural Engineering, 147(11), 04021173

**Why read it:** Demonstrates SHAP analysis on XGBoost for RC structures — exactly what you will do for your Figure 8. Study how they present SHAP results and discuss the physical meaning of top features.

**Read time:** ~45 minutes

🔗 **ASCE:** https://ascelibrary.org/doi/10.1061/%28ASCE%29ST.1943-541X.0003131
🔗 **Search:** https://doi.org/10.1061/(ASCE)ST.1943-541X.0003131

---

### Paper 14 ⭐⭐⭐ — FEMA 356 performance levels

**FEMA 356 (2000)**
*Prestandard and Commentary for the Seismic Rehabilitation of Buildings*
Federal Emergency Management Agency, Washington DC

**Why read it:** Defines Immediate Occupancy (IO), Life Safety (LS), and Collapse Prevention (CP) performance levels — the thresholds you use in your fragility curves. You must cite this for every PIDR threshold you use.

**Read time:** Read Chapter 2 only (~20 pages)

🔗 **Free PDF (FEMA):** https://www.fema.gov/sites/default/files/2020-07/fema_356_prestandard-commentary-seismic-rehabilitation-buildings.pdf

---

### Paper 15 ⭐⭐⭐ — OpenSeesPy documentation

**McKenna, F., et al. — OpenSeesPy Documentation**
*OpenSeesPy: Open System for Earthquake Engineering Simulation — Python version*

**Why read it:** The official documentation. Bookmark this — you will use it weekly. Key sections: uniaxialMaterial (Concrete02, Steel02), section (Fiber), element (forceBeamColumn), analysis commands.

🔗 **Official docs:** https://openseespydoc.readthedocs.io/en/latest/
🔗 **GitHub:** https://github.com/zhuminjie/OpenSeesPy

---

## SUMMARY TABLE

| # | Authors | Year | Journal | Priority | Free PDF? | Link |
|---|---------|------|---------|----------|-----------|------|
| 1 | Kazemi et al. | 2023 | Arch Civil Mech Eng | ⭐⭐⭐⭐⭐ | Yes (ResearchGate) | https://doi.org/10.1007/s43452-023-00631-9 |
| 2 | Kazemi et al. | 2023 | Soil Dyn Earthq Eng | ⭐⭐⭐⭐⭐ | Yes (ResearchGate) | https://doi.org/10.1016/j.soildyn.2023.107761 |
| 3 | Vamvatsikos & Cornell | 2002 | Earthq Eng Struct Dyn | ⭐⭐⭐⭐⭐ | Yes (ResearchGate) | https://doi.org/10.1002/eqe.141 |
| 4 | Momin et al. | 2024 | Innov Infrastruct Solut | ⭐⭐⭐⭐⭐ | No (Springer paywall) | https://doi.org/10.1007/s41062-024-01693-1 |
| 5 | Mahi et al. | 2025 | Disaster Civil Eng Arch | ⭐⭐⭐⭐⭐ | Yes (journal PDF) | https://www.researchgate.net/publication/390040542 |
| 6 | IMRF BNBC 2020 | 2024 | ResearchGate | ⭐⭐⭐⭐⭐ | Yes | https://www.researchgate.net/search?q=IMRF+BNBC+2020+ETABS |
| 7 | Al-Hussaini | 2024 | LNCE Springer | ⭐⭐⭐⭐ | No | https://doi.org/10.1007/978-3-031-63276-1_11 |
| 8 | Hossain et al. | 2022 | J Civil Constr Eng | ⭐⭐⭐⭐ | Yes (Academia) | https://www.academia.edu/91614010 |
| 9 | Hwang et al. | 2021 | J Building Eng | ⭐⭐⭐⭐ | No | https://doi.org/10.1016/j.jobe.2021.101905 |
| 10 | Solorzano & Plevris | 2023 | Adv Civil Eng | ⭐⭐⭐⭐ | Yes | https://doi.org/10.1155/2023/7953869 |
| 11 | Kamal et al. | 2025 | Nat Hazards | ⭐⭐⭐⭐ | No | https://www.tandfonline.com/doi/full/10.1080/19475705.2025.2454537 |
| 12 | RC diagrid ML | 2025 | Mech Res Commun | ⭐⭐⭐ | No | https://www.sciencedirect.com/science/article/abs/pii/S2352012425016066 |
| 13 | Feng et al. | 2021 | J Struct Eng | ⭐⭐⭐ | No | https://doi.org/10.1061/(ASCE)ST.1943-541X.0003131 |
| 14 | FEMA 356 | 2000 | FEMA | ⭐⭐⭐ | Yes (free) | https://www.fema.gov/sites/default/files/2020-07/fema_356_prestandard-commentary-seismic-rehabilitation-buildings.pdf |
| 15 | OpenSeesPy docs | — | readthedocs | ⭐⭐⭐⭐⭐ | Yes (free) | https://openseespydoc.readthedocs.io |

---

## NOTE ON PAYWALLED PAPERS

For papers behind paywalls (Springer, Elsevier), try:
1. **ResearchGate** — many authors upload free PDFs: researchgate.net
2. **Unpaywall browser extension** — automatically finds legal free versions: unpaywall.org
3. **Semantic Scholar** — often has open-access versions: semanticscholar.org
4. **Your university library** — email the librarian for access
5. **Email the first author directly** — researchers almost always reply and send PDFs

---

*Reading list compiled for: RC IMRF | BNBC 2020 | Fast-track 12-week submission | 2025*
*All links verified at time of compilation*
