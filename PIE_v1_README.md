# PIE-v1 — 2-Phase Inducement Engine
### Absolute Dollar Intelligence (ADI) | Emmanuel, Nairobi EAT/UTC+3

> *"The more inducement respected, the more liquidity to take out, the bigger the move."*
> — VectorFX 2-Phase Inducement Trap Theorem

---

## What PIE-v1 Is

PIE-v1 codifies the **VectorFX 2-Phase Inducement Trap Theorem** into a fully automated Pine Script v6 indicator system. It detects and narrates the complete sequence that precedes every high-probability trade entry:

```
Asia Build-Up → Phase 1 Inducement Sweep → Manipulation into OB
→ Vector Level Interaction → MSS Confirmation → Phase 2 Entry
→ Distribution / Expansion
```

The system is split into two files that both live on the same chart:

| File | Modules | Purpose |
|---|---|---|
| `PIE_v1_CORE.pine` | M1–M7 | Session engine, Asia analysis, structure, OBs, inducement, Vector Level |
| `PIE_v1_SIGNALS.pine` | M8–M10 | Entry signals, KNN episodic memory, Glass Box narrative |

---

## Installation

1. Open TradingView → Pine Script Editor
2. Create a new script → paste `PIE_v1_CORE.pine` → Save as **"PIE-v1 CORE"** → Add to chart
3. Create a second new script → paste `PIE_v1_SIGNALS.pine` → Save as **"PIE-v1 SIGNALS"** → Add to chart
4. Both indicators now share the same chart pane (overlay=true)
5. Set your preferred timeframe (recommended: **1m, 5m, or 15m** for entries; CORE auto-reads 4H HTF)

> **Important:** Add CORE first, then SIGNALS. Both must be on the same symbol and timeframe.

---

## Input Reference

### CORE Inputs

| Input | Default | Description |
|---|---|---|
| Dollar Risk per Trade | $50 | Base risk in USD per trade |
| KNN Max Episodes | 500 | Maximum trade memories stored |
| Show Session Boxes | true | Render Asia range box |
| Show MMM Windows | true | Highlight Magic Minute Mitigation windows |
| Swing Lookback | 10 bars | Used for BoS/ChoCh detection |
| OB Lookback | 20 bars | Used for orderblock scanning |
| HTF Reference | 240 (4H) | Higher timeframe for bias |
| Manual Bias Override | Auto | Force Bullish/Bearish/Ranging if Auto is wrong |

### SIGNALS Inputs

| Input | Default | Description |
|---|---|---|
| Dollar Risk per Trade | $50 | Must match CORE value |
| KNN Max Episodes | 500 | Must match CORE value |
| KNN k neighbors | 7 | Nearest neighbors for confidence scoring |
| Broker | Pepperstone | Affects pip/lot calculation |
| Instrument | Auto | Auto-detects from ticker; override for Deriv synthetics |
| Enable Divergence Confluence | true | Adds RSI/MACD divergence check (+5 confidence if present) |
| Divergence Indicator | RSI | RSI or MACD |
| RSI Length | 14 | RSI period |
| Log Trade Outcome | 9 (Skip) | Set to 0/1/2 on bar after trade closes to train KNN |

---

## Module Descriptions

### M1 — Session Engine
All times in **EAT (UTC+3), no DST**. Detects:
- **Asia** 03:00–10:00 EAT
- **Frankfurt** 10:00–11:00 EAT
- **London Open** 11:00–12:00 EAT (broad London 11:00–20:00)
- **NY Open** 16:00–17:00 EAT
- **NY Trap** 17:00–18:00 EAT
- **London Close** 20:00–21:00 EAT
- **MMM Windows**: 11:30, 12:30, 16:30, 17:30 EAT (±30 bars tolerance)

Yellow background = MMM window active. Cyan dashed line = London open. Purple dashed line = NY open.

### M2 — Asia Range Analyzer
Builds Asia high/low/mid during the session. At Frankfurt open, classifies:

| Class | Name | Condition |
|---|---|---|
| 0 | AWS (Asian Whipsaw) | Both sides swept |
| 1 | High/Low | One side swept |
| 2 | Continuation | >40 pip range, mitigates HV orders |
| 3 | Midline Mitigation | Price near Asia midline |
| 4 | Impulsive Range | >40 pips → continuation OB expected |
| 5 | Build-Up | <40 pips → expect sweep then reversal |
| 6 | Rangebound | No clear intention |

Gray box = Asia range. Dashed gray line = Asia midline.

### M3 — Daily Cycle Classifier
Uses HTF momentum + Asia class to classify the day:

| Cycle | Counter-Trend OK? | Strength |
|---|---|---|
| DowntrendRun (0) | No | Strong |
| SlightDowntrend (1) | Yes | Medium |
| WithinRange (2) | Yes | Weak/Both |
| TrendReversal (3) | No | Strong |

Week phase: Monday/Fake (0), Tue–Thu/Real (1), Friday/Accum (2).

### M4 — Structure Engine
- **BoS** (Break of Structure): close beyond last confirmed swing → labeled on chart
- **ChoCh** (Change of Character): wick sweep + opposing BoS; valid ONLY if inducement exists (M6 confirms)
- **ChoCh = SMT** if no inducement exists → marked separately
- **MSS Pending**: ChoCh candidate waiting for M7 confirmation
- **LPOD/S**: Last Point of Demand/Supply — if broken, full leg gets targeted
- **Corrective Leg**: all opposing demand/supply mitigated → single Phase 1 only needed

### M5 — Orderblock Validator
Five OB types, all must pass the **3-Rule Binary Gate**:

| Rule | Condition |
|---|---|
| 1. Has Imbalance | FVG detectable on 1m TF |
| 2. Be Impulsive | Body > 70% ATR |
| 3. Creates Inducement | Swing extreme exists above/below zone |

**If any rule fails → zone is rejected. No partial scoring.**

Types: Engulfed (0), Imbalance (1), Wick/Hammer (2), Complex/SMT⚠ (3 — do not trade), Phase 1 Reaction-Sweep (4).

Refinement cascade: Daily→4H | 4H→15m | 15m→5m/1m | 5m→1m | 1m→15s/5s.

Slight Mitigation: price entered zone but didn't reach high-volume body → registered as partial, usable as Phase 2 inducement.

### M6 — Inducement Layer (The Core)
**Phase 1**: last level of price before OB imbalance; the "evil candle" extreme. Marked with `●` and dashed `x1` line.

**Phase 2 Sub-types** (solid `x2` line):
| Type | Name | Aggressiveness |
|---|---|---|
| 0 | ChoCh Inducement | Most Passive — wait 5s/15s fail |
| 1 | Resting Liquidity/SMT | Semi-Aggressive — 5s fail or limit |
| 2 | Two Phase 1s / Long Phase 1 | Aggressive — limit acceptable |
| 3 | Second Miss of Refinement | Most Aggressive — limit, near-zero post-tap |

**AMD (Power of 3)**:
- Accumulation = Phase 1 box (below OB if buying, above if selling)
- Manipulation = Phase 1 swept into OB
- Distribution = post-MSS continuation

**Inducement Count** (`ind_count`): the single most important KNN feature. Higher count = more liquidity taken = larger expected move.

### M7 — Vector Level Tracker
Orange `VL` dashed line. The zone responsible for the Phase 1 sweep that **fails to create new low (buy) / new high (sell)**.

**MSS Validity Gate** (must reach VL before MSS is valid):
- ✓ **VALID**: Price mitigates VL + creates Phase 2 inducement
- ✓ **VALID**: Price breaks VL + creates Phase 2 inducement
- ✗ **INVALID**: Price respects VL → reclassified as IPB continuation

### M8 — Entry Signal Generator
Three signal types:
- **reversal**: mss_valid + manipulation_confirmed + 2-Phase complete + OB valid + P/D gate clear
- **ipb_continuation**: single sweep + prior 2-Phase exists + 50% P/D gate clear
- **no_trade**: everything else

**50% P/D Gate — HARD STOP, no exceptions**: once price crosses the 50% equilibrium of the HTF leg, ALL pro-trend continuations are suppressed.

**Corrective Leg Mode**: single Phase 1 sweep sufficient → no Phase 2 wait needed.

**MMM Alignment**: when entry zone overlaps with MMM window → elevated confidence (+5 in KNN).

### M9 — KNN Episodic Memory
12-dimensional feature vector per episode. Up to `max_episodes` stored (default 500).

**Distance weighting**: `inducement_count` (dim 7) is weighted ×2 — most important feature.

**KNN output**:
- `confidence_score` (0–100%): win rate of 7 nearest neighbors, distance-weighted
- `pattern_tag`: session/phase2/inducement description of dominant cluster
- `risk_multiplier` (0.5–1.5): scales dollar risk for position sizing

#### How to Log Trade Outcomes
1. After your trade closes, change the **"Log Trade Outcome"** input to:
   - `0` = Loss
   - `1` = Win
   - `2` = Partial (took some profit)
2. Wait 1 bar, then change it back to `9` (Skip)
3. The KNN will record this episode and improve future confidence scores over time

### M10 — Glass Box Narrative
Three-tier automated narrative, displayed in the top-right table and sent via alerts:

- **Tier 1** (War Room): full 15-line analysis — signal, entry, SL, lots, KNN, context
- **Tier 2** (TP updates): TP1/TP2/TP3 hit conditions
- **Tier 3** (Environmental): session, MMM, P/D gate, divergence status
- **Public channel**: 3 lines + "Full analysis in the War Room 🔐"

---

## Signal Interpretation Guide

### Reading the Dashboard (CORE — top right)
Each module has a row. Green = bullish/confirmed. Yellow = pending/MMM. Red = bearish/invalid.

Key states to watch:
1. `M2 Asia` → sets the day's liquidity blueprint
2. `M6 Inducement` → `Ph1:swept Ph2:ChoCh` means 2-Phase complete
3. `M7 Vector/MSS` → must say `VALID ✓` before taking a reversal
4. `M8 Signal` → `REVERSAL` or `IPB` is your trade trigger

### Reading the Narrative Table (SIGNALS — also top right)
The signal type appears prominently at top in green (buy) or red (sell).
- Check AMD phase: enter only at `Manipulation` or `Distribution`
- Check P/D Gate: `SUPPRESS ⛔` means stay out
- Check KNN confidence: ≥70% = high confidence (green), 50–69% = medium (yellow), <50% = caution (red)

### Trade Execution Sequence
```
1. Note Asia class → sets day expectation
2. Mark Phase 1 level (dashed x1 line appears)
3. Wait for Phase 1 sweep (● evil candle appears)
4. Watch Vector Level (orange VL line)
5. MSS confirms → "VALID ✓" appears
6. Phase 2 sweeps (solid x2 line appears)
7. Signal fires → triangle label on chart
8. Entry: method depends on Phase 2 sub-type (see aggressiveness text)
9. SL: dotted line below/above manipulation sweep
10. TP1 → TP2 → TP3: labeled dashed lines
11. Log outcome after close for KNN learning
```

---

## ADI Instrument Pip/Lot Reference

| Instrument | Broker | Pip Value / Unit | Min Lot |
|---|---|---|---|
| XAUUSD | Pepperstone | $10.00/pip/lot | 0.01 |
| XAUUSD | Deriv | $0.10/pt/unit | 1 unit |
| GBPUSD | Pepperstone | $10.00/pip/lot | 0.01 |
| Volatility 75 | Deriv | $1.00/pt/unit | 1 unit |
| Volatility 50 | Deriv | $1.00/pt/unit | 1 unit |
| Volatility 25 | Deriv | $0.10/pt/unit | 1 unit |
| Volatility 10 | Deriv | $0.10/pt/unit | 1 unit |
| Step Index | Deriv | $1.00/pt/unit | 1 unit |

**ADI Lot Sizing Formula** (the pedagogical anchor):
```
lot_size = dollar_risk / (sl_pips × pip_value_per_lot)
```
Lot size is always derived from dollar risk — never the other way.

---

## Color Coding

| Color | Meaning |
|---|---|
| 🟢 Green (#00e676) | Bullish zones, OBs, BoS |
| 🔴 Red (#ff1744) | Bearish zones, SL |
| 🟡 Yellow (#ffd600) | MMM windows, neutral |
| 🟠 Orange (#ff9800) | Vector Level |
| 🔵 Gray (#78909c) | Asia range |
| 🟣 Purple | Divergence confluences |
| Dashed line | Phase 1 (x1) |
| Solid line | Phase 2 (x2) |
| Dotted line | Stop-loss |

---

## Strategy Rules (Non-Negotiable)

1. **3-Rule OB Gate is binary** — if any of the 3 rules fails, the zone is dead. No partial credit.
2. **50% P/D Gate is a hard stop** — even a perfect 2-Phase setup is suppressed past equilibrium.
3. **MSS must be valid** (M7) before trading a reversal — if `mss_valid = false`, treat as IPB or skip.
4. **Phase 2 sub-type determines entry aggressiveness** — ChoCh (Type 0) needs most confirmation; Second Miss (Type 3) needs almost none.
5. **KNN modulates risk only** — it never gates or blocks M8 signals. A 30% confidence score still takes the trade at 0.5× risk.
6. **Inducement count is the most important KNN dimension** — more inducement phases swept = larger expected distribution move.
7. **SL always at end of confirmed manipulation sweep** — never at OB edge.
8. **Never trade M5 OB Type 3 (SMT⚠)** — it has no inducement and will be run as liquidity.

---

## Backtest & Learning Notes

- Run on **1m charts** for entries after identifying setup on 5m/15m
- Asia class determination fires at Frankfurt open (10:00 EAT) — check M2 at that time
- MMM windows (11:30, 12:30, 16:30, 17:30 EAT) are statistically the highest-probability entry moments
- KNN improves meaningfully after 50+ logged episodes; becomes reliable at 200+
- Ping-Pong mode (M3 `WithinRange` cycle): allow both buy and sell signals alternately within HTF range extremes

---

*PIE-v1 | Absolute Dollar Intelligence | Built for the ADI War Room*
*Based on VectorFX 2-Phase Inducement Trap Theorem © 2022*
*All Rights Reserved — ADI Internal Use Only*
