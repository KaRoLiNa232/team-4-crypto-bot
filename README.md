# Team-4-Crypto Trading Strategy

## Strategy Overview

### Core Logic
Our strategy focuses on a **News-Based Sentiment & Technical Momentum** approach, optimized for the highest possible **Sharpe Ratio**. We follow a strict binary decision model (Buy/Sell) to comply with the competition rules.

1.  **Entry Condition (Buy):** - **Strong Sentiment:** When News Sentiment is POSITIVE with a confidence score > 0.85 AND the market is not overbought (RSI < 65).
    - **Mean Reversion:** When RSI < 32 (oversold) and News Sentiment is NOT Negative.
2.  **Exit Condition (Sell):** - **Risk Management:** Immediate exit if price drops by 4.5% (Stop-Loss) to protect the Sharpe Ratio.
    - **Profit Taking:** Exit when profit reaches 13% (Take-Profit) or RSI > 78 (overextended).
    - **Negative News:** Immediate sell/hedge if Sentiment turns NEGATIVE.

### Performance Results
- **Sharpe Ratio:** 1.244 
- **Total Return:** 8.23%
- **Win Rate:** 25.13%
- **Final Balance:** $10,823.49

### Comments after discussion
    - Strategy is a repeatable Trend-Following system, not a series of lucky guesses.
    - With 191 trades, the Law of Large Numbers confirms its edge: 'Big Hits' like XRP (+21%) and ETH (+12%) are specifically designed to outweigh the frequent, controlled 4.5% losses.
    - While the Sharpe Ratio is suppressed by this 'good' upside volatility, the $823.49 profit proves its positive expectancy.
    - Regarding risk: using a fixed conservative allocation ensured account survival, while implementing Dynamic Position Sizing (Kelly Criterion) would be my next logical upgrade to further optimize the risk-adjusted return

### Decision Flowchart (Mermaid)
```mermaid
graph TD
    Start[Market Data & News Input] --> CheckNews{Sentiment > 0.85?}
    CheckNews -->|Yes| CheckRSI{RSI < 65?}
    CheckNews -->|No| CheckDip{RSI < 32?}
    
    CheckRSI -->|Yes| Buy[Action: BUY]
    CheckRSI -->|No| Sell[Action: SELL / HEDGE]
    
    CheckDip -->|Yes| CheckNeg{News Negative?}
    CheckNeg -->|No| Buy
    CheckNeg -->|Yes| Sell
    CheckDip -->|No| Sell
    
    Buy --> Monitor[Monitor Position]
    Monitor --> ExitCond{StopLoss 4.5% OR TP 13% OR RSI > 78?}
    ExitCond -->|Yes| Sell
    ExitCond -->|No| Buy
