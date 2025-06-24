# Junior-data-scientist-assignment
# Junior Data Scientist - Trader Behavior Insights

## Assignment Overview

This assignment focuses on exploring the relationship between trader performance and market sentiment. The primary objective is to uncover hidden patterns and deliver actionable insights that can drive smarter trading strategies in the Web3 space.

We work with two primary datasets:
1.  **Bitcoin Market Sentiment Dataset**: Contains `Date` and `Classification` (Fear/Greed) of market sentiment.
2.  **Historical Trader Data from Hyperliquid**: Includes details such as `account`, `symbol`, `execution price`, `size`, `side`, `time`, `start position`, `event`, `closedPnL`, and `leverage` (though 'Leverage' column was not present in the provided `historical_data.csv`).

## Data Acquisition and Preprocessing

The datasets were obtained from the provided Google Drive links:
* Historical Data: `historical_data.csv`
* Fear Greed Index: `fear_greed_index.xlsx` (provided as `fear_greed_index.xlsx - Sheet1.csv`)

**Steps Performed:**
1.  Both datasets were loaded into Pandas DataFrames.
2.  Date columns (`Timestamp IST` in historical data and `date` in fear/greed index) were converted to datetime objects and standardized to `date` format for accurate merging.
3.  The two datasets were merged on their respective date columns to combine trader performance with market sentiment. A left merge was performed to retain all historical trading data and append the corresponding sentiment.

## Exploratory Data Analysis (EDA) and Key Findings

After merging the datasets, an exploratory data analysis was conducted to understand the relationship between market sentiment and trader behavior/performance.

### 1. Performance Metrics by Sentiment Classification

| classification | Average_Closed_PnL | Total_Closed_PnL | Number_of_Trades | Avg_PnL_Per_Trade |
| :------------- | :----------------- | :--------------- | :--------------- | :---------------- |
| Extreme Fear   | 450.67             | 32448.27         | 72               | 450.67            |
| Extreme Greed  | 40.64              | 21499.10         | 529              | 40.64             |
| Fear           | 143.35             | 513769.42        | 3584             | 143.35            |
| Greed          | 68.26              | 48598.09         | 712              | 68.26             |
| Neutral        | 173.65             | 205076.82        | 1181             | 173.65            |

**Observations:**
* **Highest Profitability in Extreme Fear:** Despite a low number of trades, `Extreme Fear` periods show the highest average 'Closed PnL' per trade, suggesting a highly profitable contrarian opportunity.
* **Lower Profitability in Greed:** `Greed` and `Extreme Greed` periods consistently yield lower average PnL per trade, indicating that trading during these optimistic phases may be riskier or less efficient.
* **Consistent Returns in Neutral/Fear:** `Neutral` and `Fear` periods present more stable, moderate average PnL per trade, with `Fear` accounting for the largest volume of trades.

### 2. Trade Side Distribution by Sentiment Classification

| Side           | BUY  | SELL |
| :------------- | :--- | :--- |
| Extreme Fear   | 66   | 6    |
| Extreme Greed  | 237  | 292  |
| Fear           | 1964 | 1620 |
| Greed          | 220  | 492  |
| Neutral        | 527  | 654  |

**Observations:**
* **Extreme Fear: Predominantly BUY:** During `Extreme Fear`, traders overwhelmingly favor BUY trades, aligning with the observed high profitability from contrarian buying.
* **Greed/Extreme Greed: More SELL:** In `Greed` and `Extreme Greed` periods, SELL trades are more prevalent, suggesting profit-taking or attempts to short the market, though with lower overall average PnL.
* **Neutral: More SELL:** Even in `Neutral` markets, SELL trades slightly outnumber BUY trades.

### 3. Trade Direction Distribution by Sentiment Classification

| Direction      | Buy | Close Long | Close Short | Long > Short | Open Long | Open Short | Sell | Spot Dust Conversion |
| :------------- | :-- | :--------- | :---------- | :----------- | :-------- | :--------- | :--- | :------------------- |
| Extreme Fear   | 0   | 0          | 16          | 0            | 50        | 6          | 0    | 0                    |
| Extreme Greed  | 197 | 47         | 0           | 0            | 40        | 185        | 59   | 1                    |
| Fear           | 42  | 1243       | 677         | 1            | 1245      | 376        | 0    | 0                    |
| Greed          | 44  | 76         | 59          | 0            | 117       | 416        | 0    | 0                    |
| Neutral        | 292 | 166        | 0           | 0            | 235       | 24         | 464  | 0                    |

**Observations:**
* **Extreme Fear: Opening Long:** Dominated by 'Open Long' trades, reinforcing the contrarian long strategy during periods of high fear.
* **Extreme Greed: Mixed but Significant Shorting:** Shows a notable number of 'Open Short' positions alongside 'Buy' trades. The lower average PnL suggests that shorting in extreme greed may be challenging.
* **Fear: Balanced but Active:** High activity in both 'Open Long' and 'Close Long', as well as 'Close Short' and 'Open Short', indicates dynamic trading with a mix of strategies.
* **Greed: Leaning Towards Shorting:** 'Open Short' trades are significantly higher than 'Open Long' trades, consistent with the observed higher volume of SELL trades.

## Actionable Insights for Smarter Trading Strategies

Based on the analysis, here are key insights that can drive more informed trading decisions:

1.  **Contrarian Play in Extreme Fear:** The data strongly suggests that **buying during periods of `Extreme Fear`** is a highly profitable strategy. Traders might consider accumulating positions when the market sentiment is at its lowest.

2.  **Prudence During Extreme Greed:** **Reduce exposure or take profits during `Extreme Greed`** periods. The significantly lower average PnL indicates that extending positions or initiating new ones during peak optimism tends to be less rewarding and potentially riskier.

3.  **Adaptive Strategies for Fear and Neutral Markets:** While not yielding extreme profits, `Fear` and `Neutral` market conditions offer more consistent, albeit moderate, returns. These periods are suitable for more standard trading strategies, potentially with a slight bias towards **buying in `Fear`** and being cautious with **selling in `Neutral`** given the observed distributions.

4.  **Behavioral Bias & Opportunity:** The observed biases in trade side and direction for different sentiments (e.g., more selling/shorting in `Greed`) can be leveraged. If collective behavior during certain sentiments leads to lower average PnL, a **contrarian approach to that collective bias** could present an edge.

## Files in this Repository

* `historical_data.csv`: The raw historical trader data.
* `fear_greed_index.xlsx - Sheet1.csv`: The raw Bitcoin market sentiment data.
* `merged_trading_sentiment_data.csv`: The combined dataset of historical trades and market sentiment, after preprocessing and merging.
* `sentiment_performance_summary.csv`: A CSV file summarizing the average PnL, total PnL, number of trades, and average PnL per trade, grouped by market sentiment classification.
* `sentiment_side_distribution.csv`: A CSV file showing the count of BUY and SELL trades for each market sentiment classification.
* `sentiment_direction_distribution.csv`: A CSV file detailing the counts of various trade directions (e.g., 'Open Long', 'Open Short', 'Close Long') for each market sentiment classification.

---

This analysis provides a foundational understanding of how market sentiment influences trader performance and behavior, offering valuable insights for developing more effective trading strategies.
