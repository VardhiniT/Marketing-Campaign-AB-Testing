# Marketing Campaign A/B Testing — Facebook Ads vs Google AdWords

Statistical comparison of two paid-advertising channels over a full year (365 days of 2019) to decide where a marketing agency should put its client budget, based on clicks, conversions, spend and cost per conversion.

**Tech:** Python · pandas · NumPy · SciPy · statsmodels · scikit-learn · Matplotlib · Seaborn

## Business question

Which ad platform is more effective in terms of clicks, conversions and overall cost-effectiveness — and how many conversions can we expect for a given number of clicks?

## Dataset

`data/marketing_campaign.csv` — one row per day for each campaign (365 rows, 17 columns): ad views, clicks, conversions, cost per ad, click-through rate, conversion rate and cost per click for both Facebook and AdWords.

## Approach

1. **Exploratory analysis** — distributions of daily clicks and conversions, and frequency of low/medium/high-conversion days per platform.
2. **Correlation analysis** — relationship between clicks and conversions on each platform.
3. **A/B hypothesis test** — Welch's two-sample t-test on daily conversions.
   - H₀: μ_Facebook ≤ μ_AdWords · H₁: μ_Facebook > μ_AdWords
4. **Linear regression** — predict Facebook conversions from Facebook clicks.
5. **Temporal analysis** — conversions by weekday and month, and monthly cost per conversion.
6. **Cointegration test** (Engle–Granger) — long-run relationship between ad spend and conversions.

## Key results

| Metric | Facebook | AdWords |
|---|---|---|
| Mean daily conversions | **11.74** | 5.98 |
| Click → conversion correlation | **0.87** | 0.45 |

- **A/B test:** t = 32.88, p ≈ 9.3 × 10⁻¹³⁴ (p < 0.05) → reject H₀; Facebook drives significantly more conversions.
- **Regression (Facebook clicks → conversions):** R² = 0.76, MSE = 2.02. E.g. 50 clicks ≈ 13 conversions, 80 clicks ≈ 19 conversions.
- **Timing:** Mondays and Tuesdays convert best; conversions trend upward across the year. May and November had the lowest cost per conversion, February the highest.
- **Cointegration:** test statistic −14.76, p ≈ 2.1 × 10⁻²⁶ → spend and conversions share a stable long-run relationship, so budget changes have a predictable effect on conversions.

## Recommendation

Shift more budget to Facebook Ads, weight spend toward the start of the week and toward historically low cost-per-conversion months, and use the regression model to set realistic conversion targets for planned click volumes.

## Repository structure

```
├── Marketing_Campaign_AB_Testing.ipynb   # full analysis with outputs
├── data/
│   └── marketing_campaign.csv            # raw campaign data
├── requirements.txt
└── README.md
```

## Run it

```bash
pip install -r requirements.txt
jupyter notebook Marketing_Campaign_AB_Testing.ipynb
```

## Acknowledgement

The project idea and dataset follow a publicly available YouTube tutorial on marketing A/B testing; the analysis was reproduced and extended here for learning.
