# S&P 500 Variance Risk Premium and Synthetic Gamma Scalping

Empirical research on forecasting the S&P 500 variance risk premium (VRP), evaluating volatility-model forecasts, and studying the mechanics of delta-hedged straddles through a synthetic options simulation.

> **Important:** The options and straddle results in this project are model-generated simulations, not a historical backtest using executable SPX option quotes. They should not be interpreted as realised trading performance or investment advice.

## Research question

Do HAR, GARCH(1,1), and GJR-GARCH(1,1) forecasts provide information about the S&P 500 variance risk premium beyond VIX-based measures, and does that information improve stylised variance-timing and delta-hedged straddle decisions?

## Project workflow

The Jupyter notebook, [`Quant_VRP_Gamma_Scalping_Research.ipynb`](Quant_VRP_Gamma_Scalping_Research.ipynb), implements the following workflow:

1. **Market data:** Downloads daily S&P 500, VIX, VIX9D, VIX3M, and E-mini S&P 500 futures-proxy data from Yahoo Finance.
2. **Volatility forecasting:** Constructs realised-variance targets and compares HAR, Student-t GARCH(1,1), and Student-t GJR-GARCH(1,1) forecasts.
3. **Out-of-sample evaluation:** Uses chronological and rolling-origin evaluation, VIX-regime and calendar-year comparisons, and MSE, RMSE, and QLIKE loss measures.
4. **Statistical inference:** Applies HAC/Newey–West standard errors, Holm multiple-testing corrections, moving-block bootstraps, and non-overlapping-cohort checks.
5. **VRP analysis:** Forms a proxy as VIX-implied variance minus forecast physical variance, then evaluates its calibration, ranking, and relationship with subsequent realised VRP.
6. **Synthetic options experiment:** Prices European straddles with Black–Scholes, simulates delta hedging, and analyses hedge frequency and assumed transaction-cost sensitivity.
7. **Risk attribution and futures hedging:** Examines Greeks, higher-order Greeks, Shapley attribution, integer-contract ES hedges, futures-roll adjustments, drawdowns, and accounting checks.

## Data

The notebook uses the following Yahoo Finance symbols:

| Symbol | Series |
| --- | --- |
| `^GSPC` | S&P 500 cash index |
| `^VIX` | Cboe Volatility Index |
| `^VIX9D` | 9-day VIX measure |
| `^VIX3M` | 3-month VIX measure |
| `ES=F` | Continuous E-mini S&P 500 futures proxy |

The data are retrieved when the notebook runs. The available history, observations, and saved-run statistics can change as Yahoo Finance data are revised or become unavailable. Record the run date and data sample when reproducing results.

## Main findings and interpretation

The saved analysis suggests:

- HAR, GARCH, and GJR-GARCH do **not** establish a reliable overall forecasting improvement over the VIX-only benchmark.
- Some VRP signal quintiles display patterns of interest, but the globally corrected bootstrap intervals do not establish a robust Q5–Q1 premium.
- The strategy comparisons do not establish a statistically robust, implementable VRP-timing advantage.
- The options simulation is useful for studying model mechanics, Greek exposures, hedging, and sensitivity to assumptions. It does not demonstrate executable option-strategy profitability.

These are empirical findings from a particular saved run, not universal claims. Re-run the notebook before quoting numerical results.

## Important limitations

1. **No historical SPX option chain:** Yahoo Finance does not provide the historical, strike-specific SPX option quotes required for an executable options backtest. Option prices and implied-volatility inputs are therefore synthetic/model-based.
2. **Simplified pricing assumptions:** The baseline Black–Scholes setup uses zero risk-free rate and dividend yield. Option execution costs are scenario assumptions; the baseline includes zero option execution cost.
3. **Incomplete market frictions:** Bid–ask spreads, market impact, margin, financing, funding constraints, taxes, and all operational execution effects are not fully represented.
4. **Continuous futures proxy:** `ES=F` is not a full history of individual listed ES contracts. Roll adjustment and integer-contract hedging improve the implementation analysis but do not replace contract-level execution data.
5. **Statistical power:** Small samples in some volatility regimes and a limited number of active simulated trades constrain inference. Multiple-testing adjustments and bootstrap intervals should be considered when interpreting results.

Accordingly, the synthetic gamma-scalping section is a **mechanics and sensitivity study**, not evidence of a live or historically executable trading edge.

## Reproducing the analysis

### 1. Clone the repository

```bash
git clone https://github.com/Bhavya-project1/spx-variance-risk-premium-research.git
cd spx-variance-risk-premium-research
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS / Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Launch JupyterLab

```bash
jupyter lab
```

Open `Quant_VRP_Gamma_Scalping_Research.ipynb` and run the notebook from top to bottom. An internet connection is required for Yahoo Finance downloads.

For reproducibility, preserve the notebook, package versions, run date, downloaded data snapshot (where permitted), and generated outputs used for any reported result.

## Repository contents

```text
.
├── Quant_VRP_Gamma_Scalping_Research.ipynb
├── README.md
├── requirements.txt
├── CITATION.cff
├── CONTRIBUTING.md
└── .gitignore
```

## Disclaimer

This repository is an academic and educational research project. It is not investment advice, a recommendation to trade, or a claim of realised investment performance. The simulated results depend on modelling assumptions and data-source limitations. Validate all calculations and assumptions independently before using them for any financial decision.
