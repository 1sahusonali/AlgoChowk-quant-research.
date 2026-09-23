# AlgoChowk-quant-research.
Objective: Investigate the hypothesis that the NIFTY 50 index recovers after a significant one-day fall (\le -2.0\%).
Setup & Reproducibility
Language: Python 3.11
Libraries: pandas, numpy, scipy, yfinance
Data: Daily OHLC data for NIFTY 50 (^NSEI) from 2010 to 2026. The cleaned dataset (nifty50_daily_clean_2010_2026.csv) is included in this repository.
To Run: Open the Jupyter Notebook (.ipynb) and execute all cells sequentially. The code is entirely vectorized and requires no additional frameworks.
Methodology & Assumptions
Event Definition: A daily Close-to-Close drop of -2.0% or worse.
Execution: To strictly prevent look-ahead bias, entry occurs at the Open of t+1, and exit occurs at the Close of t+k (where k=3). This isolates the capturable intraday drift from the uncapturable overnight gap.
Capital Allocation (Non-Overlapping): During market panics, events cluster tightly. To prevent fictitious leverage (assigning the same capital to simultaneous trades), the engine enforces a strict non-overlapping filter. Any event triggered while a position is already open is rejected.
Friction: The backtest applies a conservative 20 bps round-trip transaction cost to account for Indian Securities Transaction Tax (STT) and execution slippage.
Key Results
Event Occurrences: 89 independent (non-overlapping) crash events.
Statistical Significance: A 10,000-sample non-parametric permutation test yielded p = 0.0414. While technically crossing the \alpha = 0.05 threshold against the unconditional baseline, this metric masks severe structural weakness in the trade profile.
Out-of-Sample Degradation: Mean returns collapsed by more than half on unseen data, dropping from 0.43% In-Sample (2010–2019) to just 0.21% Out-of-Sample (2020–2026).
Backtest Performance: Subjected to realistic 20 bps transaction friction, the cumulative return over 16 years is just 8.48%, accompanied by a severe -28.27% maximum drawdown.
Limitations & Conclusion
Tail Risk Expansion: While the win rate remained stable out-of-sample, volatility (standard deviation) nearly doubled from 2.23% to 3.95%, and the worst-case single trade plummeted to -11.01%.
Final Verdict: The strategy is uninvestable. The apparent in-sample mean return fails to survive out-of-sample regime shifts, and the combination of high transaction friction and extreme drawdowns makes it completely unviable for live deployment. Allocating capital to this signal would constitute a failure of risk management.

