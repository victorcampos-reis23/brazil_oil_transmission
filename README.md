# Brazil Oil Price Transmission: A Time-Varying Analysis (2004–2024)

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**How do global oil price shocks transmit to the Brazilian economy — and has this changed over time?**

This project estimates the **time-varying pass-through** of Brent crude oil shocks to Brazilian inflation (IPCA), the exchange rate (BRL/USD), and economic activity (IBC-Br) using a rolling-window TVP-VAR framework.

---

## Key Finding

> **Oil price shocks transmit to Brazil primarily through the exchange rate channel — and this relationship has weakened significantly over two decades.** A 10% Brent shock appreciated the BRL by **3.2%** in the pre-boom era (2004–2010), but this effect declined to **1.0%** post-2017, suggesting structural changes in Brazil's commodity-currency nexus following energy sector reforms and the consolidation of pre-salt production. Inflation proved largely insulated from direct oil shocks across all regimes, pointing to the dominant role of administered prices and exchange rate hedging in Brazil's price formation.

---

## Transmission by Regime

| Period | → IPCA | → BRL/USD | → IBC-Br |
|---|---|---|---|
| Pre-boom (2004–2010) | 0.0015 | -0.3209 | 0.1620 |
| Petrobras era (2011–2016) | -0.0026 | -0.2447 | 0.1197 |
| Post-reform (2017–2024) | -0.0019 | -0.1003 | 0.0601 |

*Cumulative 12-month response to a 1% positive Brent crude shock. Negative BRL/USD = real appreciation.*

---

## Economic Interpretation

**Exchange rate (dominant channel)**
The negative sign on BRL/USD confirms Brazil's commodity-currency dynamics: rising oil prices strengthen the real. This effect weakened from -0.32 (pre-boom) to -0.10 (post-reform), consistent with greater capital account openness and a more complex relationship between oil revenues and currency flows as pre-salt production scaled up.

**Inflation (insulated)**
Near-zero IPCA responses across all regimes suggest that Petrobras pricing policies, fuel subsidies, and administered price mechanisms largely decoupled domestic fuel prices from global oil shocks — at the cost of deferred fiscal pressure, as documented in the 2014–2016 crisis.

**Economic activity (diminishing sensitivity)**
Positive oil shocks boosted IBC-Br by 0.16% in the pre-boom period, declining to 0.06% post-reform. This structural weakening is consistent with Brazil's gradual economic diversification and the reduced weight of the oil sector in aggregate demand transmission.

---

## Methodology

```
Global Oil Shock (Brent)
        │
        ├──► Exchange Rate (BRL/USD)  ──► Dominant channel (weakening post-2017)
        │
        ├──► IPCA Inflation           ──► Insulated by administered prices
        │
        └──► IBC-Br Activity          ──► Positive but diminishing effect
```

**Estimation approach:**
- **Baseline:** Standard VAR with Cholesky identification (oil price ordered first)
- **Time-varying:** Rolling 60-month window VAR to track coefficient evolution
- **Robustness:** Alternative window sizes, WTI price, structural break tests

**Identification assumption:** Global oil prices are exogenous to Brazilian domestic conditions (small open economy assumption), consistent with Allegret et al. (2015).

---

## Data Sources

| Variable | Source | Series ID | Transformation |
|---|---|---|---|
| Brent Crude (USD/bbl) | FRED | `DCOILBRENTEU` | Log-difference |
| IPCA Inflation | BCB/SGS | `433` | MoM % |
| BRL/USD Rate | Yahoo Finance | `BRL=X` | Log-difference |
| IBC-Br Activity | BCB/SGS | `24363` | Log-difference |

All data fetched automatically via public APIs — no manual downloads required.

---

## Reproducing the Results

```bash
# 1. Clone
git clone https://github.com/victorcampos-reis23/brazil-oil-transmission.git
cd brazil-oil-transmission

# 2. Install dependencies
pip install -r requirements.txt

# 3. Add your free FRED API key at fred.stlouisfed.org
#    Edit the notebook: FRED_API_KEY = 'your_key_here'

# 4. Run
jupyter notebook notebooks/brazil_oil_transmission.ipynb
```

---

## Project Structure

```
brazil-oil-transmission/
├── notebooks/
│   └── brazil_oil_transmission.ipynb   # Main analysis
├── outputs/
│   ├── fig1_raw_series.png
│   ├── fig2_rolling_correlations.png
│   ├── fig3_irf_baseline.png
│   ├── fig4_tvp_transmission.png
│   └── transmission_by_regime.csv
├── requirements.txt
└── README.md
```

---

## Related Work

This project extends my M.Sc. dissertation at UFPE/PIMES, which identified an **"Energy Paradox"** in Brazilian firm performance: a 1% geopolitical price shock leads to a **1.72% decline in energy sector EBITDA**, driven by technical rigidity in input-output relationships. The exchange rate channel documented here provides the macro-level mechanism underlying that firm-level finding.

See: [geopolitics-pimes](https://github.com/victorcampos-reis23/geopolitics-pimes)

---

## References

- Caldara, D. & Iacoviello, M. (2022). Measuring Geopolitical Risk. *American Economic Review*, 112(4), 1194–1225.
- Nakajima, J. (2011). Time-Varying Parameter VAR Model with Stochastic Volatility. *Bank of Japan Working Paper* 2011-E-11.
- Primiceri, G. (2005). Time Varying Structural Vector Autoregressions and Monetary Policy. *Review of Economic Studies*, 72(3), 821–852.
- Allegret, J.P., Couharde, C., Coulibaly, D. & Mignon, V. (2015). Current accounts and oil price fluctuations in oil-exporting countries. *Energy Economics*, 47, 91–101.

---

**Author:** Victor Hugo Campos Reis Alves
M.Sc. Economics — UFPE/PIMES | [LinkedIn](https://linkedin.com/in/victor-hugo-campos) | [GitHub](https://github.com/victorcampos-reis23)
