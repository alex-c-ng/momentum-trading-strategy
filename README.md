# Momentum Strategy vs S\&P 500

A from-scratch test of whether two simple equity **factors**  of momentum, and a momentum + low-volatility blend beat buying and holding the S&P 500, with transaction costs and reproducible data.

## The question

Do stocks that rose the most over the past year keep outperforming? I test a classic momentum strategy and with a second factor (low volatility), compare it to a passive S\&P 500 benchmark, and charge a realistic transaction cost of every trade.

## Method

* **Universe:** 20 large-cap U.S. stocks, 2015–2025.
* **Momentum Signal:** trailing 12-month return (momentum), measured at each month-end.
* **Low-volatility signal:** standard deviation of the trailing 12 monthly returns (lower = preferred).
* **Blend:** rank stocks on each factor, average the ranks, hold the top 5, equal-weighted, rebalanced monthly.
* **Rule:** each month, hold the 5 highest-momentum stocks/blend, equal-weighted; rebalance monthly.
* **Benchmark:** buy and hold SPY (S\&P 500 ETF).
* **Transaction costs:** 10 bps per trade (one-way), charged on actual turnover each rebalance.
* **Tools:** Python, pandas, yfinance, matplotlib.

## Results: Momentum Trading strategy (top 5, 12-month momentum) vs S&P500

*Net figures are after 10 bps transaction costs.*

|Metric|Momentum|Momentum + Low-Vol blend|S\&P 500|
|-|-|-|-|
|Gross CAGR|36.0%|34.9%|13.5%|
|Net CAGR (after costs)|35.4%|34.9%|13.5%|
|Cost drag|0.6%|~0%|~0%|
|Annual turnover|4.6x|~0x|~0x|
|Net Sharpe|1.45|1.46|0.90|
|Net max drawdown|-21.7%|-20.7%|-23.9%|

![Equity curve](https://github.com/alex-c-ng/momentum-trading-strategy/raw/main/equity_curve_net.png)
![Equity curve](https://github.com/alex-c-ng/momentum-trading-strategy/raw/main/equity_curve_multifactor.png)

**What I found:**

* The momentum strategy outperformed the S&P500 in this backtest with a pretty dramatic CAGR despite the assumed transaction costs.
* Momentum's max drawdown (-21.7%) was actually shallower than the S\&P's (-23.9%), higher returns did not come at a higher risk in this universe. Higher return alone doesn't mean lower risk.
* At 4.6x annual turnover, transaction costs shaved 0.6% off the annual return. Momentum has a high turnover rate by nature, although taking transaction costs into account still yielded higher returns.
* While the pretty intense CAGR is a shiny number, it's highly likely due to survivorship bias mentioned below because I picked stocks that are currently doing well, meaning in the past 6-12 months they probably also performed stronger than market returns.
* Adding the volatility gave less returns but provided a less bumpy earning ride. 

I also tested a more aggressive setup with top **3** stocks on a **6-month** signal and it posted much higher gross returns. I picked it *after* seeing which combination looked best. It trades far more and generated much higher returns:

|Setup|Gross CAGR|Net CAGR|Annual turnover|Cost drag|
|-|-|-|-|-|
|Top 5, 12-month (headline)|36.0%|35.4%|4.6x|0.6%|
|Top 3, 6-month (tuned)|47.0%|46.0%|7.4x|1.1%|

I treat this 3 stock 6 month backtest strategy as an interesting optimization, not a finding.

## Limitations

* **Survivorship bias:** the 20 tickers are today's well-known winners, chosen because they survived and thrived. A momentum strategy run on a list of known winners is structurally tilted to look good.
* **One regime:** large-cap U.S. only, over a single mostly-bull decade so results probably won't generalize perfectly.
* **Costs are approximate:** 10 bps lumps commission and slippage into one assumption generated from online estimates and ignores market impact, which would grow with position size.
* **Execution timing:** I assume I can trade at the same month-end close I measure the signal on, which is mildly optimistic.

Bottom line: suggestive, not tradeable.


