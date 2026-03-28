---
layout: post
title: "I Built a Multi-Agent Hedge Fund in Python (And You Can Too)"
date: 2025-03-28 10:00:00 +0000
categories: [algorithmic-trading, python, ai, finance]
tags: [python, ai, machine-learning, trading, fintech]
image: /assets/images/banner.svg
excerpt: "How four AI agents collaborate to trade markets with the discipline of a Wall Street institution"
---

![Multi-Agent Hedge Fund Banner](/assets/images/banner.svg)

*Ever wondered what would happen if you gave an algorithm the skepticism of a risk manager, the math skills of a quant, the instincts of a research analyst, and the memory of a librarian?*

I built exactly that. And the architecture might surprise you.

---

## The Problem with Most Algo Trading Bots

If you've ever tried building a trading bot, you know the drill:

1. **The Overfit Trap**: Your backtest shows 300% annual returns. You deploy real money. It loses 30% in the first month. The strategy was curve-fitted to historical noise.

2. **The Emotion Problem**: Even automated systems need human intervention. And humans panic. They override stop-losses during drawdowns. They FOMO into trades at market tops.

3. **The Data Mess**: One bad tick from your data provider corrupts your entire signal. You don't notice until you've already placed the trade.

4. **The Black Box**: You can't explain why the bot made a trade. Was it technical analysis? Sentiment? A bug? Good luck debugging live P&L.

What if, instead of a single monolithic algorithm, we built something that mirrors how actual hedge funds work?

---

## Introducing: The Multi-Agent Hedge Fund

This project is built on a simple but powerful idea: **separation of concerns**. Just like a real hedge fund has distinct teams that check each other's work, this system has four specialized agents that collaborate on every trade.

```
┌─────────────────────────────────────────────────────────────┐
│                    COLLABORATIVE WORKFLOW                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌────────┐│
│   │ Librarian│───▶│  Analyst │───▶│   Quant  │───▶│  Risk  ││
│   │ (Data)   │    │(Sentiment│    │(Strategy)│    │Manager ││
│   └──────────┘    └──────────┘    └──────────┘    └────────┘│
│        │               │               │              │     │
│        ▼               ▼               ▼              ▼     │
│   Daily market    NLP scoring    Backtested      Final veto │
│   data sync       & signals      alpha signals   on trades │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

Each agent has one job. And critically, **no agent can act alone**.

---

## Meet The Agents

### 🔍 The Analyst — "The Sentiment Engine"

The Analyst doesn't look at price charts. It reads the world.

- **News scraping** from global financial outlets
- **Earnings call transcripts** analyzed for management tone shifts
- **Social sentiment** from high-quality financial communities
- **Regulatory filing** parsers for early catalyst detection

**Output**: A Sentiment Vector for every ticker
- Directional Score: -1.0 (Strongly Bearish) to +1.0 (Strongly Bullish)
- Confidence Interval: 0-100%
- Catalyst Tags: #Earnings, #MergerRumor, #MacroHeadwind

```python
# Example: The Analyst flags negative sentiment before it hits price
if sentiment_score < -0.5:
    quant.ignore_all_buy_signals(ticker)  # The "Bias Filter"
```

### 🔢 The Quant — "The Truth Machine"

The Quant is skeptical by design. It doesn't care about your feelings or the Analyst's gut instincts. It only cares about what the data proves.

**Key capabilities**:
- **Walk-Forward Analysis**: Divides history into training/validation sets to detect overfitting
- **Point-in-Time Constraints**: Prevents look-ahead bias (the silent killer of backtests)
- **Dynamic Slippage Models**: Adjusts for liquidity based on Average Daily Volume
- **Factor Optimization**: Bayesian search for optimal signal weights

**The Quant answers**: *"Would this strategy have worked in 2008? In March 2020? During the meme stock craze?"*

### 🛡️ The Risk Manager — "The Red Button"

This is where most DIY algo traders fail. They have entry signals but no exit discipline. The Risk Manager is the final veto on every trade.

**Pre-trade checks**:
- Concentration limits (no single stock > X% of portfolio)
- Correlation analysis (are you doubling down on the same bet?)
- Liquidity validation (can you actually exit this position?)
- Volatility regimes (is the market too chaotic right now?)

**Live monitoring**:
- Kelly Criterion position sizing
- Drawdown circuit breakers (>X% loss = automatic de-risking)
- Value at Risk (VaR) reporting

```python
# The Risk Manager can say NO
status = risk_manager.validate_trade(order)
# Returns: APPROVED | REJECTED | RESIZE[new_size]
```

### 📚 The Librarian — "The Immutable Archive"

The unsung hero. The Librarian ensures that every agent works with clean, point-in-time data.

**The Vault Architecture**:
- `raw/`: Immutable daily snapshots (protects against upstream corruption)
- `master/`: Consolidated chronological history for backtesting
- `constituents.json`: Point-in-time universe definitions

This means when you backtest a strategy for 2019, you're only using data that was *actually available* in 2019. No survivor bias. No lookahead. No "oh, I didn't realize that stock was delisted."

---

## Why This Architecture Matters

### 1. **Check and Balance**

In a single-bot system, one bug wipes out your account. Here, a bug in the Quant gets caught by the Risk Manager. Bad data from the Librarian gets flagged by the Analyst. It's distributed fault tolerance.

### 2. **Explainability**

Every trade decision leaves an audit trail:

```
AAPL BUY 100 shares @ $175.50
├── Analyst: Sentiment +0.72 (Earnings beat, strong guidance)
├── Quant: Momentum signal triggered, backtest WinRate 68%
├── Risk: Position size 2.1% of portfolio (within 5% limit)
└── Risk: Approved (liquidity OK, no earnings in next 48h)
```

### 3. **Modular Improvement**

Want to add options trading? Update the Risk Manager's Greeks calculation. Want to add crypto? Extend the Librarian's data connectors. Want to use GPT-4 for earnings analysis? Swap the Analyst's NLP engine.

Each agent is independently upgradeable.

---

## Real-World Use Cases

### 🏦 For Individual Traders
Deploy with paper trading first. The Risk Manager enforces discipline you might lack at 3 AM when a position moves against you.

### 🏢 For Prop Firms
Use as a framework for systematic strategy development. Teams can specialize: one group improves sentiment models, another optimizes execution, another manages risk parameters.

### 🤖 For Fintech Startups
White-label the engine for robo-advisory products. The modular design makes compliance auditing straightforward.

### 🔬 For Researchers
Study how multi-agent systems make decisions under uncertainty. The architecture is generalizable beyond finance.

---

## Getting Started in 5 Minutes

```bash
# Clone the repository
git clone https://github.com/ankushbhatiya/hedge_fund.git
cd hedge-fund

# Install dependencies
pip install -r requirements.txt

# Sync market data
python quant_librarian/sync_today.py

# Run your first analysis
python -c "from analyst_agent import Analyst; Analyst().score_universe()"
```

The system currently supports:
- ✅ Yahoo Finance data via `yfinance`
- ✅ Factor modeling (Quality, Momentum, Low Volatility)
- ✅ Vectorized backtesting with `bt` and `quantstats`
- ✅ Point-in-time data integrity

---

## What's Next?

This is a foundation, not a finished product. Here's what I'm working on:

| Feature | Status | Impact |
|---------|--------|--------|
| Real-time WebSocket feeds | 🔄 Planned | Live trading capability |
| LLM-powered earnings analysis | 🔄 Planned | Better sentiment accuracy |
| Interactive Brokers integration | 🔄 Planned | Real order execution |
| Docker containerization | 🔄 Planned | Cloud deployment |
| Web dashboard | 📋 Backlog | Visual monitoring |

---

## A Word of Caution

> **This software is for research purposes only.** Past performance does not indicate future results. The agents can be wrong. Markets can behave in ways no backtest predicts. Never trade with money you cannot afford to lose.

The goal isn't to replace human judgment—it's to systematize the parts of trading that humans are bad at: emotional discipline, data hygiene, and statistical rigor.

---

## The Bigger Picture

We're entering an era where AI systems don't just execute tasks—they collaborate. This project is a glimpse at what that looks like in a high-stakes domain.

Each agent has different "cognitive strengths":
- The Analyst excels at pattern recognition in unstructured data
- The Quant excels at mathematical optimization
- The Risk Manager excels at worst-case scenario planning
- The Librarian excels at memory and data integrity

Together, they're more robust than any single algorithm could be.

---

## Join the Community

If you're interested in systematic trading, multi-agent AI, or just want to see how far we can push this architecture:

⭐ **Star the repo** to follow development  
🐛 **Open issues** for bugs or feature requests  
🤝 **Submit PRs** for new data connectors or risk models  
💬 **Start discussions** about strategy ideas  

The future of trading isn't a super-intelligent AI making all the decisions. It's multiple specialized AIs checking each other's work—just like a real hedge fund.

---

*What would you add to this system? Drop your ideas in the comments below.*

---

## Resources

- [GitHub Repository](https://github.com/ankushbhatiya/hedge_fund)
- [Analyst Agent Documentation](https://github.com/ankushbhatiya/hedge_fund/blob/main/analyst_agent/Analyst_Agent.md)
- [Quant Agent Documentation](https://github.com/ankushbhatiya/hedge_fund/blob/main/quant_agent/Quant_Agent.md)
- [Risk Manager Documentation](https://github.com/ankushbhatiya/hedge_fund/blob/main/risk_manager/Risk_Manager_Agent.md)
- [Librarian Documentation](https://github.com/ankushbhatiya/hedge_fund/blob/main/quant_librarian/README.md)
