# invsto_task# Quantitative Trading Strategy

A multi-factor long-short equity trading strategy that generates alpha by going long on stocks expected to outperform and short on stocks expected to underperform.

## Overview

This strategy implements a systematic approach to equity trading using multiple alpha signals, risk management, and portfolio optimization. The strategy is designed to be market-neutral and includes comprehensive risk management features.

## Data Collection

The strategy uses the `yfinance` library to collect historical data for 10 major stocks:

- Apple (AAPL)
- Microsoft (MSFT)
- Amazon (AMZN)
- Google (GOOGL)
- Facebook (META)
- Tesla (TSLA)
- NVIDIA (NVDA)
- JPMorgan Chase (JPM)
- Johnson & Johnson (JNJ)
- Walmart (WMT)

### Data Features

- 5 years of daily historical data
- OHLCV (Open, High, Low, Close, Volume) prices
- Fundamental data (P/E ratio, market cap)
- Risk-free rate and market benchmark (S&P 500)

## Alpha Signal Development

The strategy combines three primary alpha signals:

1. **Momentum Signal**

   - 20-day rolling average of returns
   - Identifies stocks with strong upward/downward momentum
   - Helps capture trending market movements

2. **Mean Reversion Signal**

   - Deviation from 50-day moving average
   - Identifies overbought/oversold conditions
   - Helps capture price reversals

3. **Risk-Adjusted Returns Signal**
   - Rolling Sharpe ratio over 60-day window
   - Accounts for both returns and volatility
   - Helps identify stocks with better risk-adjusted performance

Additional technical indicators:

- RSI (Relative Strength Index)
- MACD (Moving Average Convergence Divergence)

## Strategy Implementation

### Signal Combination

- Dynamic weighting of signals based on recent performance
- Weights are adjusted monthly to adapt to changing market conditions
- Default weights: 40% momentum, 30% mean reversion, 30% risk-adjusted

### Portfolio Construction

- Long positions in top 3 ranked stocks
- Short positions in bottom 3 ranked stocks
- Dollar-neutral portfolio (50% long, 50% short)
- Volatility-adjusted position sizing
- POsrtfolio rebalances monthly automatically as it rebalances everyday

## Risk Management

### Position-Level Risk Controls

- Individual position stop-loss (5%)
- Trailing stop (3%)
- Transaction cost management:
  - 0.1% commission per trade
  - 0.05% slippage per trade
  - Minimum 5% position change threshold

### Portfolio-Level Risk Controls

- Portfolio stop-loss (10% from peak)
- Dollar neutrality enforcement
- Volatility-based position sizing
- Maximum position concentration limits

## Backtesting

### Performance Metrics

- Cumulative returns
- Sharpe ratio
- Maximum drawdown
- Alpha (relative to S&P 500)
- Win rate
- Profit factor
- Transaction cost analysis

### Validation Methods

- Walk-forward analysis

## Performance Analysis

### Visualizations

- Strategy vs S&P 500 cumulative returns
- Asset allocation over time
- Drawdown analysis
- Rolling performance metrics

### Analysis Features

- Trade-by-trade analysis
- Signal contribution analysis
- Risk attribution
- Transaction cost impact

## Code Structure

The code is organized into modular functions:

1. **Data Collection**

   - `collect_data()`: Downloads historical data using yfinance
   - `calculate_rsi()`: Computes RSI indicator
   - `calculate_macd()`: Computes MACD indicator

2. **Signal Generation**

   - `generate_signals()`: Creates alpha signals
   - `calculate_dynamic_weights()`: Adjusts signal weights
   - `calculate_risk_adjusted_returns()`: Computes Sharpe ratio

3. **Portfolio Construction**

   - `construct_portfolio()`: Builds long-short portfolio
   - `calculate_position_sizes()`: Determines position weights
   - `calculate_transaction_costs()`: Estimates trading costs

4. **Risk Management**

   - `check_stop_loss()`: Position-level stop-loss
   - `check_portfolio_stop_loss()`: Portfolio-level stop-loss
   - `update_trailing_stop()`: Manages trailing stops

5. **Backtesting**

   - `backtest()`: Runs strategy simulation
   - `calculate_metrics()`: Computes performance metrics
   - `plot_performance()`: Creates performance visualizations

6. **Analysis and Reporting**
   - `display_trade_details()`: Shows trade information
   - `export_trade_details_to_csv()`: Exports trade data
   - `walk_forward_analysis()`: Performs strategy validation

## Usage

1. Install required packages:

```bash
pip install pandas numpy yfinance matplotlib scipy scikit-learn
```

2. Run the strategy:

```python
python alpha_strategy_v2.py
```

3. View results:

- Performance metrics will be printed to console
- Performance plots will be displayed
- Trade details will be exported to CSV

## Performance Attribution

The strategy's performance can be attributed to:

1. Multi-factor signal combination
2. Dynamic signal weighting
3. Risk-adjusted position sizing
4. Comprehensive risk management
5. Transaction cost optimization

## Future Improvements

Potential enhancements:

1. Additional alpha signals
2. Machine learning-based signal combination
3. Dynamic position sizing based on market regime
4. Enhanced risk management features
5. Real-time trading implementation
