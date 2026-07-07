# Write-up: Trader Performance vs Market Sentiment

## Methodology

I used two datasets for this analysis:

1. **Bitcoin Fear & Greed Index** — daily sentiment labels such as Fear, Neutral, and Greed  
2. **Hyperliquid historical trade data** — trade-level records containing account, side, size, PnL, and timestamp information

First, I converted the trade timestamps into calendar dates and aligned the trade data with the daily sentiment data.  
The sentiment series had one missing trading day relative to the trader dataset, so I created a complete daily sentiment calendar and forward-filled the missing day before merging.

After merging, I created **trader-day metrics**:
- **daily_pnl** → total closed PnL per trader per day
- **win_rate** → share of profitable trades per trader-day
- **avg_trade_size** → average trade size in USD
- **trades_per_day** → number of trades taken by a trader on a day
- **long_ratio** → share of long / buy trades

I then built a trader-level summary table and created 3 simple segments:
- **Frequent vs Infrequent traders** using average trades per day
- **High Size vs Low Size traders** using average trade size
- **Consistent vs Inconsistent traders** using the standard deviation of daily PnL

---

## Key Insights

### 1) Fear days showed the strongest average trader-day profitability
The sentiment comparison showed that **Fear days had the highest average daily PnL** among the major sentiment groups in this sample.  
Greed days had the weakest average daily PnL, while Extreme Greed performed better than Greed but still below Fear.

**Interpretation:** fearful markets seem to create stronger short-term opportunities for these traders, likely because volatility is higher.

### 2) Traders became more aggressive during Fear periods
The behavior charts showed that **Fear days had the highest average trade size** and relatively strong trade frequency.  
This means traders were not becoming defensive during fearful conditions — instead, they were generally taking **larger trades and staying active**.

**Interpretation:** in this dataset, traders appear to lean into volatility during fear rather than reduce risk.

### 3) Frequent traders outperformed infrequent traders
Among the segment comparisons, **Frequent traders had much higher average daily PnL** than Infrequent traders.  
High Size traders also outperformed Low Size traders on average PnL, but trading activity was the stronger signal.

**Interpretation:** the most profitable traders in this sample were not simply the ones taking bigger positions, but the ones participating more actively and capturing more opportunities.

### 4) Inconsistent traders earned more, but with higher risk
The segmentation chart also showed that **Inconsistent traders had higher average daily PnL than Consistent traders**.  
However, this likely reflects a higher-risk style with more volatile outcomes rather than a more stable edge.

**Interpretation:** higher returns in this group may come from larger swings in PnL, so the result should not be treated as a pure quality signal.

---

## Strategy Recommendations

### Strategy 1 — Use sentiment as a participation filter
Since **Fear days show stronger average PnL and larger trade sizes**, sentiment can be used as a context signal.

**Rule of thumb:**  
During **Fear** days, allow higher trading activity mainly for traders who already perform well, especially **Frequent traders**.

### Strategy 2 — Prioritize active traders over simply large traders
Frequent traders clearly outperformed Infrequent traders, while large trade size alone was not enough to explain performance.

**Rule of thumb:**  
If position size or capital allocation is being increased, give priority to **active traders with strong recent PnL**, rather than increasing exposure for all traders equally.

---

## Conclusion

This analysis shows that **market sentiment is linked with both trader behavior and trader performance** in the provided Hyperliquid sample.

- **Fear days** were associated with the strongest average PnL
- Traders took **larger trades** during Fear periods
- **Frequent traders** performed better than Infrequent traders
- Segment-based rules are likely more useful than one rule applied to every trader

Overall, sentiment seems most useful as a **context variable for risk allocation and trader selection**, rather than as a standalone trading signal.
