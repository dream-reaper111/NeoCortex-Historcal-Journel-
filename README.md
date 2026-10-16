# NeoCortexV3 Engineering Journal

## Historical Migration Entry

**Date:** 2026-10-16  
**Version:** NeoCortexV3 Pre-Alpha  
**Development Area:** Architecture / AI / Trading / Security / Infrastructure / Data Engineering  
**Status:** ACTIVE DEVELOPMENT

---

# Objective

Document the architectural and functional evolution of NeoCortex from the original V1 platform, through NeoCortexV2, and into the current NeoCortexV3 architecture.

The purpose of this entry is to preserve the development lineage of the platform and establish the reasoning behind the major changes introduced across each generation.

NeoCortex has evolved from a relatively centralized AI-assisted trading application into a distributed research, inference, risk-management, data-processing, security, and execution platform.

A major architectural theme across this evolution has been:

```text
V1
Trading application with AI components

        ↓

V2
Hybrid AI / trading research platform

        ↓

V3
Persistent distributed intelligence,
market-state memory,
multi-model orchestration,
risk governance,
and scalable infrastructure
```

---

# NeoCortex V1

## Original Architecture

NeoCortexV1 established the original platform foundation.

The early architecture centered around a Python-based trading and machine-learning application with a FastAPI backend and browser-based interfaces.

Major V1 components included:

- FastAPI backend
- PyTorch model support
- GPU-aware model execution
- Alpaca integration
- Paper and funded account support
- Trading position retrieval
- Profit and loss monitoring
- Basic model training
- Liquidity sweep analytics
- Trading strategy utilities
- API-based model interaction
- End-user dashboard
- Liquidity Radar interface
- Authentication
- Multi-user functionality
- Strategy backtesting
- Basic deployment tooling

The system primarily operated as a centralized application.

---

# V1 Trading Integration

The original platform established brokerage connectivity through Alpaca.

Capabilities included:

- Paper trading
- Funded/live account connectivity
- Position retrieval
- P&L retrieval
- Alpaca webhook handling
- Per-user brokerage credentials
- Trade update callbacks
- Account-specific access

These capabilities formed the original execution layer used by later NeoCortex versions.

---

# V1 Authentication and Credential Handling

Security functionality began expanding during V1 development.

Features introduced included:

- User accounts
- Administrator registration controls
- Admin private-key requirement
- Bearer-token authentication
- Browser login
- HTTP-only session cookies
- User-specific Alpaca credentials
- Fernet encryption for stored brokerage credentials
- TLS support
- HTTPS redirect support
- HTTP Strict Transport Security
- Webhook signature verification
- Replay protection

The platform moved away from relying solely on environment-level credentials toward supporting encrypted user-specific credential storage.

---

# V1 Strategy Layer

Early strategy components included:

- Liquidity sweep detection
- Market-footprint analytics
- Session-based trading analysis
- Strategy backtesting
- Indicator experimentation
- Strategy ranking
- Sharpe-ratio comparison
- Profit-factor comparison

These systems established the foundation for the more advanced market-state system developed later.

---

# V1 User Interfaces

User-facing interfaces included:

- End User Console
- Liquidity Sweep Radar
- Dashboard
- Trading metrics
- Account positions
- P&L visualization
- Webhook testing interfaces

The UI initially served primarily as an operational frontend for the underlying trading API.

---

# V1 Infrastructure

Infrastructure support expanded significantly during later V1 development.

Components included:

- Docker
- Docker Compose
- Redis
- PostgreSQL
- Celery
- n8n
- Prometheus
- Grafana
- Kubernetes manifests
- Fly.io deployment
- ngrok support

This laid the deployment foundation eventually used to transition NeoCortex away from a single-machine architecture.

---

# V1 Limitations

The original system had several architectural limitations that became targets for V2 development.

Important limitations included:

- Strong dependence on centralized application logic
- Limited persistent market-state memory
- Models largely operating independently
- Limited model arbitration
- Limited long-term interaction history
- Limited data provenance
- Limited replay capability
- Limited distributed compute architecture
- Risk controls existing primarily as individual checks rather than a complete governance layer
- Research and production functionality sharing common application boundaries

These limitations led to the V2 architectural redesign.

---

# NeoCortex V2

## Architectural Goal

NeoCortexV2 moved the platform from a conventional AI-assisted trading application toward a hybrid research and decision system.

One of the largest changes was separating different forms of intelligence instead of relying on one model to make every decision.

---

# Hybrid Classical / Quantum Architecture

V2 introduced the Neo Cortex hybrid research pipeline.

The architecture intentionally remained classical-first.

Classical systems remained responsible for:

- Market-regime classification
- Risk gating
- Trade authorization
- Execution decisions
- Routing logic
- Production safety controls

Quantum components were introduced as supporting analytical systems rather than being given direct trading authority.

---

# PennyLane Integration

V2 added PennyLane-based quantum feature encoding.

Quantum circuits could be used to transform selected market features before they entered the hybrid model pipeline.

The purpose was to investigate whether quantum feature spaces could provide useful representations that classical models might not easily produce.

Fallback paths were retained so NeoCortex could continue operating when PennyLane was unavailable.

---

# Qiskit Integration

V2 introduced Qiskit-based research components.

Qiskit was primarily used for:

- Portfolio optimization research
- Quantum optimization experiments
- Quantum financial modeling
- Hybrid quantum/classical comparisons
- Research simulation

Quantum optimization was not intended for low-latency trade execution.

---

# Hybrid PyTorch Models

PyTorch remained part of the classical and hybrid inference layer.

The V2 pipeline allowed:

```text
Market Data
     ↓
Classical Feature Extraction
     ↓
Optional Quantum Encoding
     ↓
Hybrid Model
     ↓
Confidence
     ↓
Classical Risk Gate
     ↓
Execution Decision
```

Fallback models allowed NeoCortex to continue operating when optional quantum or ML packages were unavailable.

---

# Automation Pipeline

V2 integrated Neo Cortex directly into the automation architecture.

A dedicated service pipeline was introduced so the system could run market bars through:

- Data preparation
- Feature generation
- Model inference
- Quantum research components
- Confidence analysis
- Risk gating
- Trade approval or rejection

An automation endpoint was introduced to trigger the pipeline programmatically.

---

# Runtime-Safe Fallbacks

A major design goal in V2 was ensuring that experimental systems could fail without stopping the overall platform.

Fallback behavior was introduced for:

- Missing quantum libraries
- Missing PyTorch support
- Unsupported execution environments
- Experimental model failures

This was an important shift toward fault-tolerant architecture.

---

# MoE × LAM Direction

During later V2 development, NeoCortex began transitioning toward a combined:

**Mixture of Experts × Large Action Model**

architecture.

Instead of having one model attempt to understand all market behavior, the platform would contain specialized expert models.

Potential experts included:

- Market-regime expert
- Liquidity expert
- Volatility expert
- Momentum expert
- Mean-reversion expert
- Macro expert
- Sentiment expert
- Risk expert
- Execution expert
- Quantum research expert

The Mixture-of-Experts router determines which expert or combination of experts should be used for the current market state.

The LAM layer was designed to coordinate actions after expert inference.

---

# Deterministic Risk Gate

The risk system became increasingly separated from model prediction.

Models could recommend actions, but a deterministic risk layer retained final veto authority.

This architecture prevents an individual model from directly forcing execution.

Conceptually:

```text
Model Recommendation
        ↓
Expert Consensus
        ↓
LAM Controller
        ↓
RISK GATE
        ↓
Approved / Rejected
        ↓
Broker
```

---

# Historical Model Performance Development

One of the most important changes between the earlier NeoCortex versions and the V3 design was the increasing use of historical behavior as an active decision input.

The historical model does not simply ask whether a market setup exists.

It attempts to determine whether the current setup resembles previous setups that produced favorable outcomes.

The historical model evaluates combinations of:

- Market regime
- Time of day
- Session
- Liquidity conditions
- Direction of approach
- Sweep depth
- Rejection strength
- Reclaim behavior
- Previous reactions at the same level
- Volatility
- Momentum
- Volume behavior
- Trend alignment
- Macro conditions
- Model confidence
- Risk conditions
- Historical success of comparable setups

This allows NeoCortex to reject lower-quality trades rather than treating every valid technical setup equally.

---

# Observed Historical Trade Accuracy

During historical-model development and strategy evaluation, the system has shown periods where selected trade setups produced win rates above 60%.

This performance should be treated as an **observed research and testing result**, not as a guaranteed future performance level.

A trade may only receive elevated historical confidence when:

```text
Current Market State
        ↓
Historical Pattern Match
        ↓
Comparable Setups Found
        ↓
Historical Success Rate
        ↓
Confidence Threshold
        ↓
Risk Validation
        ↓
Trade Eligible
```

For example:

```text
Comparable historical setups: 184
Winning outcomes: 119
Losing outcomes: 65

Historical win rate:
119 / 184 = 64.7%
```

A setup with this type of historical profile can receive greater confidence than a setup with limited evidence or poor historical performance.

---

# Trade Filtering and the 60% Threshold

The historical system is not intended to trade every detected signal.

A major reason the model can maintain stronger results is selective execution.

NeoCortex can reject signals when:

- Historical win rate is below the required threshold
- Sample size is insufficient
- Current regime differs significantly from historical examples
- Expert models strongly disagree
- Market volatility is abnormal
- Liquidity conditions are poor
- Expected reward does not justify risk
- Portfolio exposure is already elevated
- Confidence calibration indicates excessive uncertainty

Conceptually:

```text
Technical Setup Detected
          ↓
Historical Match
          ↓
Historical Win Rate
          ↓
      < Threshold
       /       \
     YES       NO
      ↓         ↓
   REJECT    Continue
                ↓
          Expert Consensus
                ↓
            Risk Gate
                ↓
             Execute
```

This is fundamentally different from simply increasing prediction accuracy.

NeoCortex improves trade quality by reducing the number of weak trades that reach execution.

---

# Historical Confidence Scoring

Historical performance can contribute to a composite confidence score.

An example model could use:

```text
Historical Pattern Match       25%
Market Structure               20%
Liquidity                      15%
Regime Compatibility           15%
Momentum                       10%
Volatility                     5%
Macro / Sentiment              5%
Expert Agreement               5%
```

Example:

```text
Historical similarity:     0.89
Historical win rate:       0.64
Market structure:          0.82
Liquidity confidence:      0.78
Regime match:              0.91
Momentum alignment:        0.74
Expert agreement:          0.81
```

The combined result can become an execution confidence score.

The exact production weighting should remain calibrated through testing rather than being permanently hard-coded.

---

# Sample-Size Protection

NeoCortex should never treat a high historical win rate from a small number of observations as equally reliable to a large sample.

For example:

```text
6 wins / 8 trades
= 75%

500 wins / 760 trades
= 65.8%
```

Although 75% appears numerically higher, the larger second dataset provides substantially stronger evidence.

V3 therefore emphasizes:

- Minimum historical sample sizes
- Confidence intervals
- Regime-specific statistics
- Out-of-sample validation
- Walk-forward testing
- Paper-trading confirmation

---

# Expectancy Versus Win Rate

The historical model does not evaluate performance using win rate alone.

A profitable system can have a lower win rate if winning trades are substantially larger than losing trades.

NeoCortex therefore evaluates:

```text
Expectancy =
(Probability of Win × Average Win)
-
(Probability of Loss × Average Loss)
```

Example:

```text
Win rate:        62%
Average winner:  +2.0R
Average loser:   -1.0R

Expectancy:
(0.62 × 2.0R) - (0.38 × 1.0R)

= +0.86R per trade
```

This means the historical system can distinguish between:

- High win-rate but poor reward/risk strategies
- Lower win-rate but high-expectancy strategies
- High win-rate and high-expectancy setups

---

# Regime-Specific Accuracy

V3 is designed to avoid treating a strategy's overall win rate as universally valid.

The same strategy may behave differently across market regimes.

Example:

```text
Trending Market
Win Rate: 68%

Range Market
Win Rate: 61%

High-Volatility Market
Win Rate: 54%

Low-Liquidity Market
Win Rate: 47%
```

In this case NeoCortex could:

- Prefer execution during trending conditions
- Reduce position size in range conditions
- Reject trades during high-volatility conditions
- Disable the setup during low-liquidity conditions

This makes the historical system conditional rather than static.

---

# Historical Pattern Weighting

Older observations do not necessarily receive the same weight as recent observations.

V3 can weight data based on:

- Recency
- Regime similarity
- Instrument similarity
- Volatility similarity
- Session similarity
- Liquidity similarity
- Model version
- Market structure similarity

A historical trade that closely resembles current conditions can therefore contribute more than a trade from a very different environment.

---

# Level Interaction Memory

The historical model becomes significantly stronger when combined with the V3 Level-State engine.

For each major level, NeoCortex can remember:

```text
Level: 5,820.25

Interactions: 14

Previous sweeps: 6
Successful reclaims: 5
Failed reclaims: 1

Average rejection:
18.4 points

Bullish continuation after reclaim:
71%

Average time near level:
7.8 minutes

Strongest session:
New York AM
```

When price returns to the same area, NeoCortex is no longer evaluating the level as completely new.

It can compare the current interaction against the stored history.

---

# Active Trade Learning

V3 extends historical learning beyond backtests.

Each completed trade can feed sanitized outcome data back into persistent memory.

Example:

```text
Trade Setup
     ↓
Prediction
     ↓
Execution
     ↓
Outcome
     ↓
Post-Trade Analysis
     ↓
Historical Memory
     ↓
Future Pattern Matching
```

Stored fields can include:

- Setup ID
- Strategy version
- Model version
- Entry regime
- Entry confidence
- Risk level
- Expected outcome
- Actual outcome
- Maximum favorable excursion
- Maximum adverse excursion
- Exit reason
- Reward-to-risk achieved

This creates an increasingly rich dataset for future validation.

---

# Winning Trade Reinforcement

When a trade behaves as predicted, NeoCortex can strengthen the historical relevance of the associated pattern.

It does not simply memorize:

```text
"This setup won."
```

Instead it records why the setup may have worked.

For example:

```text
Liquidity sweep
+
Strong reclaim
+
NY session
+
Bullish higher timeframe structure
+
Increasing volume
+
Low opposing liquidity
=
Successful continuation
```

Future setups with similar characteristics can then receive stronger historical support.

---

# Losing Trade Analysis

Losing trades are equally important.

For unsuccessful trades, NeoCortex can analyze:

- Whether the historical match was weak
- Whether the regime changed
- Whether volatility increased unexpectedly
- Whether opposing liquidity was underestimated
- Whether confidence was miscalibrated
- Whether the stop was too tight
- Whether execution latency affected the result
- Whether the model overfit previous observations

This allows a losing trade to improve future decision quality rather than simply being counted as a failure.

---

# Continuous Performance Monitoring

A critical V3 requirement is monitoring whether historical accuracy remains stable.

Metrics should include:

- Rolling win rate
- Rolling expectancy
- Profit factor
- Maximum drawdown
- Sharpe ratio
- Average R multiple
- Calibration error
- Regime-specific accuracy
- Strategy-specific accuracy
- Model-specific accuracy
- Confidence-bucket accuracy

Example:

```text
Last 50 trades:   66%
Last 100 trades:  64%
Last 250 trades:  62%
Lifetime:         63%

Current target:
>60%
```

If rolling performance falls below the acceptable level, NeoCortex can reduce exposure, disable the strategy, or return the model to shadow mode.

---

# Model Promotion Requirements

A model should not be promoted to active execution simply because it briefly exceeds a 60% win rate.

V3 model promotion should consider:

- Minimum trade count
- Out-of-sample performance
- Walk-forward results
- Paper-trading results
- Expectancy
- Maximum drawdown
- Profit factor
- Confidence calibration
- Stability across regimes
- Performance degradation
- Execution costs
- Slippage
- Statistical uncertainty

Example promotion rule:

```text
Win Rate              >= 60%
Minimum Trades        >= 200
Positive Expectancy   Required
Profit Factor         > 1.5
Maximum Drawdown      Within Risk Limit
Paper Validation      Passed
Calibration           Passed
Risk Review           Passed
```

These numbers should be considered example thresholds until validated against the actual NeoCortex dataset.

---

# No Performance Guarantee

Historical performance is evidence, not a guarantee.

The system should explicitly avoid assuming:

```text
Past win rate = future win rate
```

Market structure, liquidity, volatility, macroeconomic conditions, and participant behavior can change.

NeoCortexV3 therefore continuously compares current performance against historical expectations and can automatically downgrade models whose edge appears to deteriorate.

---

# Security Boundaries

V2 further separated cybersecurity responsibilities from trading intelligence.

Security work included:

- Stronger authentication boundaries
- Credential encryption
- Admin-registration restrictions
- Network hardening
- TLS
- HSTS
- Webhook signature verification
- Replay prevention
- Access controls
- Secret management
- Security-focused service boundaries

---

# HellPot

A major security concept developed during V2 was the isolated HellPot system.

HellPot was designed as an isolated security environment separated from the primary NeoCortex trading stack.

Intended purposes included:

- Threat observation
- Suspicious connection isolation
- Security telemetry
- Deception systems
- Controlled attack-surface monitoring
- Security testing
- Failure isolation

HellPot was specifically intended to remain isolated from sensitive trading infrastructure.

---

# NeoCortex V3

## Architectural Goal

NeoCortexV3 represents the largest architectural change in the project.

The fundamental shift is:

> **V2 processed data. V3 remembers it.**

V3 is designed to maintain historical market interaction state instead of treating every market observation as an isolated event.

---

# Historical Intelligence as a Core V3 Component

The historical model is now intended to operate as one of the primary intelligence layers of NeoCortexV3.

Its role is not simply to predict direction.

Its purpose is to answer:

```text
Have we seen something like this before?

How many times?

Under what conditions?

How often did it work?

How much did winning trades make?

How much did losing trades lose?

Is the current market truly comparable?

Does this pattern still have an edge?
```

This moves NeoCortex toward evidence-weighted decision making.

---

# V3 Historical Decision Flow

The expanded decision process becomes:

```text
LIVE MARKET
     ↓
DATA VALIDATION
     ↓
CURRENT MARKET STATE
     ↓
HISTORICAL SEARCH
     ↓
SIMILARITY SCORING
     ↓
HISTORICAL OUTCOMES
     ↓
REGIME FILTER
     ↓
EXPECTANCY ANALYSIS
     ↓
MoE EXPERT REVIEW
     ↓
DISSENT / QUORUM
     ↓
CONFIDENCE CALIBRATION
     ↓
GLOBAL EXPOSURE GOVERNOR
     ↓
DETERMINISTIC RISK GATE
     ↓
EXECUTION
     ↓
OUTCOME
     ↓
HISTORICAL MEMORY UPDATE
```

---

# Performance Goal

The historical intelligence system is intended to maintain high-quality selective execution rather than maximize the number of trades.

A target such as:

```text
Validated Win Rate: >60%
```

can be used as an operational quality threshold where testing supports it.

However, NeoCortex should prioritize:

```text
Positive expectancy
+
Controlled drawdown
+
Stable calibration
+
Adequate sample size
+
Consistent regime performance
```

over win rate alone.

---

# Core Principle

The major historical-model improvement introduced through V2 and expanded in V3 can be summarized as:

> **NeoCortex does not only predict what the market may do. It compares the present market to what has happened before, determines how reliable that historical evidence is, filters out weak setups, measures actual outcomes, and continuously updates its understanding of which conditions produce profitable trades.**

---

# Decision

**Status:** ACCEPTED — HISTORICAL MODEL EXPANSION

Historical state, pattern matching, outcome tracking, confidence calibration, and performance degradation monitoring are considered core components of NeoCortexV3.

Any claim of sustained performance above 60% must be tied to validated backtest, walk-forward, paper-trading, or live-trading data with an adequate sample size.

---

# Follow-Up Work

- Store historical setup IDs.
- Track win rate by setup.
- Track expectancy by setup.
- Track performance by regime.
- Track performance by session.
- Track performance by instrument.
- Add minimum sample-size requirements.
- Add rolling win-rate monitoring.
- Add confidence intervals.
- Add confidence calibration.
- Add model-decay detection.
- Add automatic shadow-mode fallback.
- Add historical similarity scoring.
- Add post-trade outcome analysis.
- Record maximum favorable excursion.
- Record maximum adverse excursion.
- Track entry and exit quality.
- Compare predicted probability against actual outcome.
- Add strategy-level performance dashboards.
- Add historical-model health monitoring.
- Require validation before documenting sustained >60% performance as production performance.
