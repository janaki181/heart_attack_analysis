# Heart Attack Risk in China

### Risk factors, healthcare inequality and public health policy: what a 239,266-patient dataset can and cannot tell us

**QACA Research Challenge | Public Health Analytics**
Prepared by **Janaki Rajvir** · November 2026

---

## The headline

> **12.15% of patients (29,071 of 239,266) had a heart attack, and no group differs from that rate by more than chance.**

No risk factor, healthcare access level, income, education, region or combination of risk factors stands out. Machine-learning models trained on the data perform no better than random guessing. The file also fails basic realism checks, so it looks **synthetic**. The recommendations in this project therefore rest on **published evidence about China**, not on patterns in the dataset.

An honest "no association" result, backed by tests that were powerful enough to find one, is the finding.

---

## What is in this repository

| Order | File | What it is |
|---|---|---|
| **1** | `Heart_Attack_Risk_China_Report.docx` | The full written report: findings, tables, figures, policy review and recommendations |
| **2** | `02_Baseline_to_Recommendations.ipynb` | **Main analysis notebook.** Baseline, risk factor tests, inequality, policy review, modelling, fairness, recommendations, limitations |
| **3** | `Heart_Attack_Dashboard.html` | **Interactive dashboard.** Opens in any browser, works offline, every chart filters every other chart |
| **4** | `01_Data_Understanding_and_EDA.ipynb` | How the data was loaded, checked and explored: data dictionary, quality checks, distributions |
| **5** | `heart_attack_china.csv` | The dataset (239,266 rows, 28 columns) |

**Start with the report or notebook 02, then open the dashboard to explore.**

---

## How to run it

**1. Install the libraries**

```bash
pip install pandas numpy plotly scipy scikit-learn xgboost nbformat jupyter
```

**2. Keep the files together.** The CSV must sit in the same folder as the notebooks.

**3. Open the notebooks**

```bash
jupyter notebook
```

Run notebook `01` first if you want the data study, then `02` for the full analysis. The dashboard needs no setup: just double-click `Heart_Attack_Dashboard.html`.

> **If a chart does not appear:** run `pip install --upgrade nbformat ipython`, restart the kernel, and run the cell again.

---

## The questions the brief asked, and the answers

| Question | What was done | Answer |
|---|---|---|
| **How common are heart attacks?** | Proportion with a 95% interval, by age band and gender | **12.15%** (12.02% to 12.28%), about 1 patient in 8 |
| **Does the data behave like real patients?** | Hypertension vs blood pressure, hypertension by age, province vs region, dataset vs national figures | **No.** Hypertension is unrelated to blood pressure and does not rise with age |
| **Which factors are linked to heart attacks?** | Chi-square for 64 groups against the rest, Bonferroni correction, risk ratios, t-tests, 24 risk combinations | **None.** 0 of 64 groups significant after correction |
| **Do access and social position matter?** | Access mix by area and income, rates with error bars, income by access heat map | **No gap.** All groups between 11.9% and 12.4% |
| **What has policy achieved?** | Published national evaluations, and what data an evaluation would need | **Evidence supports five measures**, but this file cannot test them |
| **Can a model predict heart attacks?** | Random forest, XGBoost, shuffled-label test, logistic regression, subgroup fairness | **No.** ROC-AUC 0.50 for every model and group |

---

## Key numbers

| Measure | Result |
|---|---|
| Overall heart attack rate | **12.15%** |
| Groups with p below 0.05 (64 tested) | **2** (about 3 expected by chance) |
| Groups significant after Bonferroni correction | **0** |
| Risk ratios of 9 yes/no factors | **0.99 to 1.01**, every interval includes 1 |
| Cohen's d for age, blood pressure, risk score | **-0.008 to 0.002** |
| 24 smoking x hypertension x age combinations | **11.54% to 12.81%** |
| Test ROC-AUC, random forest / XGBoost | **0.503 / 0.500** |
| Precision, XGBoost vs random guessing | **12.1% vs 12.1%** |
| PR-AUC, real labels vs shuffled labels | **0.1213 vs 0.1223** |
| Model score across 12 gender, area, income and region groups | **0.490 to 0.510** |

---

## Method, in plain words

- **Every comparison is made against the 12.15% baseline.** Only 12% of patients had a heart attack, so guessing "No" for everyone is right 88% of the time. **Accuracy is not used.**
- **Many tests means many chances to be fooled.** The **Bonferroni correction** (0.05 divided by 64 groups = 0.00078) stops a lucky p-value being reported as a finding.
- **Effect size matters, not only p-values.** Risk ratios and Cohen's d say how big a gap is, not just whether one exists.
- **Models are judged by precision, recall and PR-AUC.** Random guessing scores a precision of 12.15%, which is the number to beat.
- **A model needs something to learn.** The shuffled-label test trains the same model on random outcomes. If real labels score the same, the model found nothing.
- **Fairness is checked per group.** The same model is scored separately by gender, area, income level and region.
- **The "None" education trap.** Pandas reads the text "None" as missing, which wrongly showed 59,617 nulls. It is a real category (no formal education) and was kept.

---

## Interactive dashboard

Open **`Heart_Attack_Dashboard.html`** in any browser.

- **Filter:** click a slicer button on the left, or click **any bar or slice** in any chart. Click again to remove it.
- **Read:** the cards show patients, heart attacks, the heart attack rate and its gap to 12.15%, plus average age, blood pressure and CVD risk score.
- **Explore:** the **Explore any factor** chart has a dropdown for every variable, and the risk-factor profile compares your selection with all patients.
- **Charts:** bars are patient counts, and the red line is the heart attack rate.

All data is embedded in the file, so nothing is uploaded and no internet is needed.

---

## Policy evidence used

| Policy | Evidence |
|---|---|
| **Basic Public Health Service (from 2009)** | 2014 pilot: hypertension control 76.9% vs 68.2% |
| **Chest pain centres** | Odds of in-hospital death 0.67 (95% CI 0.51 to 0.88), 798,008 patients in 746 hospitals |
| **Air Pollution Action Plan** | PM2.5 fell from 52.5 to 42.2 ug/m3; about 64,000 fewer pollution-related deaths |
| **Tobacco tax (May 2015)** | Wholesale tax raised from 5% to 11%; cigarette sales down 7.8% |
| **Volume-based procurement (2019)** | 59.1% price cut on 7 blood pressure drugs in the pilot |

The scale of the problem: **330 million** people with cardiovascular disease and **245 million** with hypertension, of whom only **43.3%** are aware, **38.7%** treated and **12.9%** controlled (2020 to 2022).

---

## Recommendations

**Who to prioritise** (from published evidence, not from this dataset)

- **Adults aged 65 and over:** hypertension rises from 20.8% to 54.1% with age (CHARLS 2020)
- **Rural residents:** coronary heart disease mortality 148.19 vs 135.08 per 100,000, rural vs urban
- **People with unmanaged hypertension:** 43.3% aware, 12.9% controlled

**What to do**

1. **Close the hypertension care gap** with screening at village clinics and community centres
2. **Prioritise rural hospitals** for chest pain centres and ambulance links
3. **Keep cutting air pollution and tobacco use**
4. **Collect better data:** dates, follow-up, true geography, facility-level access and a **policy start-year sheet**
5. **Do not deploy the current models.** Re-run the same pipeline on real clinical data

---

## Limitations

- **The data looks synthetic:** flat distributions, round percentages, no relationships between variables
- **No dates or follow-up:** 12.15% is a share of patients in the file, not a yearly incidence, and no before-and-after policy comparison is possible
- **Region, Province and access are labels without real geography**
- **Cross-sectional data cannot show cause and effect**
- **The sample does not look like China:** half the patients smoke (national figure about 27%) and 30% are obese (17.8%)
- **External figures are for context only:** they come from different years and populations, and the policy evidence varies in strength (a pilot, a single city, a modelled estimate)

---

## Next steps with real data

| Question | Data needed |
|---|---|
| Which risk factors predict heart attack in China? | Clinical records with outcomes linked to age, blood pressure, smoking, diabetes and history |
| Is the outcome a future event? | Dates and follow-up |
| Do rural and low-income patients get treatment later? | Time from symptoms to treatment, hospital level, travel distance |
| Did a policy reduce heart attacks? | Place and date of each patient, plus policy start dates |
| Is a model fair across groups? | Subgroup labels and a record of how the outcome was diagnosed |

Suggested real datasets: **CHARLS** (China Health and Retirement Longitudinal Study, adults 45 and over) and the **China Kadoorie Biobank** (about 0.5 million adults, followed over time).

---

## Tools

**Python** · pandas · NumPy · SciPy · scikit-learn · XGBoost · Plotly · Jupyter · plain HTML and JavaScript for the dashboard

---
