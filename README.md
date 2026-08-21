# Bitcoin Price Prediction from Limit Order Book Data

Raunak Sood and Noah Baird · undergraduate research paper

An LSTM trained on Binance BTC perpetual limit-order-book data, benchmarked against an
Auto-ARIMA baseline for short-horizon price and price-change prediction.

## Data

Binance Bitcoin perpetual LOB data (Kaggle), 12 consecutive days from 9–20 January 2023:
**3,730,870 rows × 42 columns** sampled at 250ms, covering 10 bid levels and 10 ask levels
of price and volume.

Preprocessing downsamples to every 40th row (10 seconds), which both denoises the series and
approximates the execution latency of a crypto exchange. Mid price is taken as the average of
the best bid and best ask; targets are the next mid price and the next percentage change.

## Result

| model | MAE, price | MAE, % change |
|---|---|---|
| **LSTM** | **9.98** | **0.00015** |
| Auto-ARIMA (baseline) | 1101.95 | 0.00016 |

The LSTM decisively beats the baseline on price level and only marginally on percentage
change — which is the more honest comparison of the two, since price level is close to a
random walk and easy to track. The percentage-change result is the one that would matter to
a trader, and there the edge is thin.

## Files

- `Bitcoin LOB Analysis.pdf` — the write-up
- `ProjectCode1.ipynb` — data preparation, ARIMA baseline, LSTM
