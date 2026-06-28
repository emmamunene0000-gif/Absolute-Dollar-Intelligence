# PIE-v1 — 2-Phase Inducement Engine
### Absolute Dollar Intelligence (ADI) | Emmanuel, Nairobi EAT/UTC+3

> *"The more inducement respected, the more liquidity to take out, the bigger the move."*
> — VectorFX 2-Phase Inducement Trap Theorem

---

## What PIE-v1 Actually Does

PIE-v1 is a **reading agent** — it reads price the way a trained human analyst would, top-down, across timeframes. It does not predict. It narrates in real time what the market has done, what it is doing, and what the next probable move is given the current context. Every label, line, and dashboard row is a chapter in that narrative.

The sequence it tracks is always the same:

```
1. Asia builds liquidity (range)
2. HTF bias established (4H structure)
3. Manipulation: Phase 1 sweep takes liquidity beyond Asia extremes or swing highs/lows
4. Price returns to valid Orderblock (OB) — the trap door
5. Vector Level interaction confirms smart money repositioned
6. Market Structure Shift (MSS) — old swing broken, new direction locked
7. Phase 2 sweep clears remaining liquidity
8. Entry signal fires — reversal or IPB continuation
9. Distribution: TP1 (1:1) → TP2 (1:2) → TP3 (1:3)
```

If any step in that chain is missing, PIE-v1 waits. There is no signal until the full sequence is read.

---

## Installation (Single File)

1. Open TradingView → Pine Script Editor
2. Paste the entire `PIE_v1.pine` contents → Save as **"PIE-v1"** → Add to chart
3. Set chart timeframe to your **execution timeframe** (M5 or M15 recommended)
4. The indicator auto-requests 4H data for HTF bias — no second script needed

---

## The Multi-Timeframe Workflow

PIE-v1 is designed around a **4-layer top-down read**. Each timeframe has a specific job. You should not trade from a single timeframe view.

---

### H4 — The Compass (Context, Never Entries)

**What you are looking for:**
- **HTF Bias**: Is the 4H making higher highs/higher lows (bull) or lower highs/lower lows (bear)?
- **P/D Gate**: Is current price in Premium (above the 20-bar HTF midpoint) or Discount (below)?
- **The Big OB**: Where is the major unfilled orderblock from the last impulsive leg?
- **The Big Swing**: Which highs/lows has price targeted and which are still untouched?

**What PIE-v1 shows on H4:**
- Large OB boxes (green = demand, red = supply) — these are the HTF zones that govern all lower timeframe setups
- Asia range box (grey) — built during 03:00–10:00 EAT, visible from Frankfurt open
- Session separator lines (cyan = London 11:00 EAT, purple = NY 16:00 EAT)
- The dashboard shows HTF bias in **Cycle** row: `BULLISH | DownRun | BrkRetest CT✓` means bias is bull, momentum is strong, Asia was a break-then-retest, countertrend confirmed
- **P/D Gate** row: `SUPPRESS ⛔ (>50%)` means price is in the wrong half of the HTF range — no trades from this timeframe until it corrects

**Your job on H4:** Decide which side you're on (bull or bear) and where the next major draw on liquidity is. That draw is your TP3 target.

---

### H1 — The Blueprint (Structure, OBs, Phase Levels)

**What you are looking for:**
- The actual swing highs/lows being created (these become Phase 1 targets)
- The Orderblock that price will return to after the Phase 1 sweep
- The Vector Level — the OB low (bull) or OB high (bear) that MSS must breach
- The AMD cycle: are we in Accumulation, Manipulation, or Distribution?

**What PIE-v1 shows on H1:**
| Visual | What It Means |
|---|---|
| Green/red box (OB) | Valid orderblock — Has Imbalance + Is Impulsive + Creates Inducement (all 3 rules passed). Label says `DEM ENG` / `SUP ENG` etc. |
| `DEM` / `SUP` prefix | Demand zone (bull OB) or Supply zone (bear OB) |
| `ENG` / `WCK` / `SMT⚠` | OB type: Engulfing candle / Wick/Hammer / Complex SMT — **never trade SMT⚠** |
| Orange dashed line `VL` | Vector Level — the OB edge that price must breach post-sweep to confirm MSS |
| Yellow circle `●` | Phase 1 evil candle — the exact bar whose extreme was swept to take liquidity |
| Dashed line `Ph1` | The Phase 1 level (the swept extreme) — drawn when Ph1 is confirmed swept |
| Solid line `Ph2` | The Phase 2 level — drawn when Ph2 sweep confirmed; this is the last liquidity cleared before entry |
| `MSS✓` label | Market Structure Shift confirmed — old swing broken, smart money repositioned. This is the green light. |
| Yellow background | MMM (Magic Minute Mitigation) window — 11:30, 12:30, 16:30, 17:30 EAT ±30 min |

**Your job on H1:** Identify the current setup — which OB is active, where Ph1 was swept, is MSS confirmed? Read the **Inducement** and **MSS/VL** rows in the dashboard to get the status without scanning the chart.

---

### M15 — The Setup Timeframe (Signal Confirmation)

**What you are looking for:**
- Is the signal `REVERSAL` or `IPB`? (Top of dashboard, large text)
- Is the P/D Gate clear? (`Clear ✓` in the gate row)
- Is AMD in `Manipulation` or `Distribution`? (Not `Accumulation`)
- Does the entry zone (OB box) sit at a logical point relative to the M15 structure?
- Is the KNN confidence ≥ 50%?

**What PIE-v1 shows on M15:**
| Visual | What It Means |
|---|---|
| `▲ REVERSAL` / `▼ REVERSAL` label | Full 2-Phase sequence complete, MSS valid, OB valid, P/D clear — highest quality signal |
| `▶ IPB` / `◀ IPB` label | In-Play Break — Ph1 swept, valid OB, price on correction leg — pre-MSS entry for aggressive traders |
| Shaded entry zone box | The valid OB boundaries — your limit order zone (buy at bottom, sell at top) |
| Solid red line `SL` | Stop loss level — ATR × 1.5 below/above the entry zone. Label shows pips. |
| Dashed line `TP1 1:1` | First target — 1× the SL distance beyond entry. Partial profits here. |
| Dashed line `TP2 1:2` | Second target — 2× risk. Scale out. |
| Solid line `TP3 1:3 ✦` | Primary target — 3× risk. This is the trade. |
| `ChoCh✓` in Structure row | Change of Character confirmed — structure has shifted, not just a BoS |
| `BoS▲` / `BoS▼` label | Break of Structure (off by default — toggle on to study structure) |
| Purple dot `DIV▲` / `DIV▼` | RSI divergence confluence — bullish/bearish divergence detected |

**Your job on M15:** Confirm the signal is valid and logical. Check all 5 rows in the dashboard: Cycle, Structure, OB, Inducement, MSS/VL. If any row is red/pending when you expect green, wait.

**REVERSAL signal checklist (M15):**
- [ ] `Ph1: swept✓` in Inducement row
- [ ] `Ph2: swept✓` in Inducement row
- [ ] `MSS✓ VL: [price]` in MSS/VL row (not `MSS?`)
- [ ] `Clear ✓ (<50%)` in P/D Gate row
- [ ] OB row not `None` and not `SMT⚠`
- [ ] Signal row shows `▲ REVERSAL BUY` or `▼ REVERSAL SELL`

---

### M5 — The Execution Timeframe (Entries and Timing)

**What you are looking for:**
- The entry zone box at M5 granularity — where exactly is the OB on this timeframe?
- Is price approaching the entry zone or already inside it?
- Is there an MMM window active (yellow background) coinciding with entry?
- What is the exact SL in pips and does the lot size make sense for your account?

**What PIE-v1 shows on M5:**
| Visual | What It Means |
|---|---|
| Entry zone box (green/yellow shaded) | Your limit order range — place limit at zone top (bull) or zone bottom (bear) |
| `SL` line (solid red) | Hard stop — 1.5× ATR below entry zone for buys, above for sells |
| `TP3 1:3 ✦` line (solid green) | Your primary take-profit — the whole reason you entered |
| `TP1` and `TP2` (dashed) | Scaling-out levels — book 30–50% at each |
| `Ph1` dashed line | Where the manipulation sweep happened — context for where SM took the liquidity |
| `Ph2` solid line | The last sweep before entry — confirms liquidity above/below entry is cleared |
| `VL` orange dashed | Vector Level — the OB edge that was confirmed mitigated. Below this = bulls in control. |
| Dashboard `SL | Lots` row | Exact lot size calculated: `dollar_risk / (sl_pips × pip_value)` |

**Your job on M5:** Execute. Once M15 confirms the signal, drop to M5 to time the entry into the zone. Use a limit order at the zone boundary. SL and TP levels are already drawn.

---

## Dashboard Row-by-Row Reference

The top-right table shows every module's live state. Read it top to bottom.

| Row | What It Shows | Green Means | Red/Yellow Means |
|---|---|---|---|
| **PIE-v1 \| ADI** | Header | — | — |
| **Signal** | Current signal type | REVERSAL or IPB active | Watching (no signal) |
| **AMD** | Power of 3 phase | Distribution (ready) | Accumulation (building) |
| **Session** | Current EAT session + MMM flag | London/NY active | Off-Hours / Asia |
| **Asia** | Asia range class + pip size | Hi/Lo or Imp (clear intention) | AWS (both sides swept, skip) |
| **Cycle** | HTF bias + daily variation | Bullish DownRun CT✓ | Ranging (no clear bias) |
| **Structure** | Current market structure event | ChoCh✓ or MSS | SMT (danger) |
| **OB** | Orderblock type | ENG or WCK | None or SMT⚠ (don't trade) |
| **Inducement** | Ph1/Ph2 type + count | Ph1:swept✓ Ph2:swept✓ | Ph1:pending (wait) |
| **MSS / VL** | MSS validity + VL price | MSS✓ | MSS? (not yet) |
| **P/D Gate** | 50% equilibrium gate | Clear ✓ (<50%) | SUPPRESS ⛔ — no trades |
| **Entry Zone** | OB hi/lo prices | Price shown | — (no OB) |
| **SL \| Lots** | ATR-based SL level + lot size | — | Red = bearish SL |
| **TP1/2/3** | Three take-profit levels | — | — |
| **KNN** | Confidence % + pattern + wins | ≥70% green | <50% red (half risk) |
| **Entry Style** | How aggressive to be | LIMIT — near-zero post-tap | Wait 5s/15s S/D fail |
| **Week \| Episodes** | Week phase + KNN memory count | Tue–Thu Real | Mon Fake / Fri Accum |
| **Public** | Simplified signal text | Signal description | No signal |

---

## Every Visual Element Explained

### Lines

| Line | Style | Color | Meaning |
|---|---|---|---|
| Cyan vertical | Dashed | Cyan | London Open (11:00 EAT) |
| Purple vertical | Dashed | Purple | NY Open (16:00 EAT) |
| `Ph1` horizontal | Dashed, thick | Bull/bear color | Phase 1 inducement level — the swept extreme |
| `Ph2` horizontal | Solid, thick | Bull/bear color | Phase 2 inducement level — second liquidity cleared |
| `VL` horizontal | Dashed | Orange | Vector Level — OB edge, must be mitigated for MSS |
| `SL` horizontal | Solid, thick | Red | Stop loss — ATR × 1.5 from entry zone |
| `TP1 1:1` horizontal | Dashed, thin | Green | Take profit 1 — 1× risk |
| `TP2 1:2` horizontal | Dashed, thin | Green (lighter) | Take profit 2 — 2× risk |
| `TP3 1:3 ✦` horizontal | Solid, thick | Green | Take profit 3 — 3× risk (primary target) |

### Boxes

| Box | Color | Meaning |
|---|---|---|
| Grey box | Semi-transparent grey | Asia session range (03:00–10:00 EAT) with midline |
| Green box (OB) | Semi-transparent green | Valid bull orderblock — demand zone |
| Red box (OB) | Semi-transparent red | Valid bear orderblock — supply zone |
| Green/Yellow entry box | Semi-transparent, signal color | Current entry zone — your limit order window |

### Labels

| Label | Meaning |
|---|---|
| `▲ REVERSAL` / `▼ REVERSAL` | Full 2-Phase REVERSAL signal — highest quality |
| `▶ IPB` / `◀ IPB` | In-Play Break — valid but pre-MSS, more aggressive |
| `MSS✓` | Market Structure Shift confirmed — green light for reversal |
| `DEM ENG` / `DEM WCK` | Demand OB type: Engulfing / Wick |
| `SUP ENG` / `SUP WCK` | Supply OB type: Engulfing / Wick |
| `DEM SMT⚠` / `SUP SMT⚠` | Complex SMT zone — **do not trade** |
| `●` (yellow circle) | Evil candle — Phase 1 inducement sweep bar |
| `Ph1` | Phase 1 level text label |
| `Ph2` | Phase 2 level text label |
| `VL` | Vector Level label |
| `DIV▲` / `DIV▼` | RSI divergence confluence (purple) |
| `BoS▲` / `BoS▼` | Break of Structure (hidden by default) |

### Backgrounds

| Background | Meaning |
|---|---|
| Yellow | MMM window active (11:30, 12:30, 16:30, 17:30 EAT ±30 min) — highest probability timing |

---

## Signal Logic

### REVERSAL (Highest Quality)

All of the following must be true simultaneously on a confirmed bar close:

1. Phase 1 swept (manipulation confirmed)
2. Phase 2 swept (second liquidity cleared)
3. Valid Orderblock exists (all 3 OB rules passed)
4. MSS valid (Vector Level mitigated)
5. P/D Gate clear (price NOT past 50% of HTF range in wrong direction)

### IPB — In-Play Break (Aggressive, Pre-MSS)

All of the following must be true:

1. Phase 1 swept (manipulation confirmed)
2. Valid Orderblock exists
3. Price is on the corrective leg (retracing toward OB)
4. MSS not yet valid (you're entering before full confirmation)
5. P/D Gate clear

> **IPB is not a full signal.** It is for advanced traders who read the structure and want early positioning. If MSS fails to materialise after IPB entry, exit.

---

## The Three OB Rules (Binary Gate)

**All 3 must pass. Zero tolerance for partial passes.**

| Rule | Test | Failure = |
|---|---|---|
| 1. Has Imbalance | FVG detectable (high[i+1] < low[i-1] or inverse) | Zone rejected |
| 2. Be Impulsive | Candle body > 65% of ATR(14) | Zone rejected |
| 3. Creates Inducement | Swing extreme exists beyond zone | Zone rejected |

OB Types that can pass:
- `ENG` (Engulfed) — strongest, body engulfs previous candle
- `WCK` (Wick/Hammer) — valid, wick creates the inducement
- `SMT⚠` — **never trade**. No inducement, will be used as liquidity.

---

## ATR-Based Position Sizing

SL is always `ATR(14) × SL Multiplier` (default 1.5×). This makes it timeframe-aware — M5 SL will be tighter than H1 SL automatically.

```
sl_distance  = ATR(14) × 1.5
sl_level     = entry_zone_low − sl_distance   (bull)
               entry_zone_high + sl_distance  (bear)
sl_pips      = sl_distance / (mintick × 10)

lot_size = dollar_risk / (sl_pips × pip_value_per_lot)
```

TP levels:
```
TP1 = entry + 1 × sl_distance  (1:1)
TP2 = entry + 2 × sl_distance  (1:2)
TP3 = entry + 3 × sl_distance  (1:3)  ← primary target
```

---

## Input Reference

### Risk

| Input | Default | Description |
|---|---|---|
| Dollar Risk ($) | 50 | Base risk in USD per trade |
| ATR SL Multiplier | 1.5 | ATR × this = SL distance. Increase for volatile instruments. |
| KNN Max Episodes | 500 | Maximum trade memories stored |
| KNN k Neighbors | 7 | Nearest-neighbor count for confidence scoring |
| Log Outcome | 9 (Skip) | 0=Loss, 1=Win, 2=Partial — log after trade closes, reset to 9 |

### Sessions

| Input | Default | Description |
|---|---|---|
| Show Asia Box | true | Renders the Asia range rectangle |
| Show MMM Window | true | Yellow background during MMM windows |

### Structure

| Input | Default | Description |
|---|---|---|
| Auto Swing (TF-adaptive) | true | M1/M5→5, M15/M30→7, H1/H4→10, D+→15 |
| Swing Lookback (manual) | 10 | Only used when Auto Swing is off |
| OB Lookback | 20 | How many bars back to scan for valid OBs |

### HTF

| Input | Default | Description |
|---|---|---|
| HTF Timeframe | 240 (4H) | HTF for bias detection |
| Bias Override | Auto | Force Bullish/Bearish/Ranging if Auto is wrong |

### Instrument

| Input | Default | Description |
|---|---|---|
| Broker | Pepperstone | Affects pip/lot calculation |
| Instrument | Auto | Auto from ticker; override for Deriv synthetics |

### Confluence

| Input | Default | Description |
|---|---|---|
| Divergence Confluence | true | RSI divergence adds +5 to KNN confidence |
| RSI Length | 14 | RSI period |

### Labels (Toggle Visibility)

| Input | Default | Description |
|---|---|---|
| Show BoS Labels | false | BoS▲/▼ on every structural break — off by default to reduce clutter |
| Show MSS Label | true | MSS✓ when market structure shifts |
| Show OB Zone Label | true | DEM/SUP label on OB boxes |
| Show Inducement Dot | true | Yellow ● on Phase 1 evil candle |
| Show Position Tool | true | SL + TP1/2/3 lines on chart |

---

## KNN Episodic Memory

The KNN does not predict the future. It answers: **"Of the past setups most similar to this one, how many were winners?"**

12 features stored per episode:

| Dim | Feature | Weight |
|---|---|---|
| 0 | Session (Asia=0, FFT=1, Ldn=2, NY=3...) | ×1 |
| 1 | Cycle type (DownRun=0, Slight=1, Range=2) | ×1 |
| 2 | Asia class (0–6) | ×1 |
| 3 | Phase 1 type (Minor/Medium/Major by TF) | ×1 |
| 4 | Phase 2 sub-type (ChoCh/RstLiq/2Ph1/2ndMs) | ×1 |
| 5 | OB type (ENG/WCK/SMT) | ×1 |
| 6 | P/D index (premium=0, discount=1) | ×1 |
| **7** | **Inducement count** | **×2** |
| 8 | Asia pip range (normalised 0–1) | ×1 |
| 9 | MMM window (0/1) | ×1 |
| 10 | Divergence present (0/1) | ×1 |
| 11 | Outcome (stored, not compared) | — |

**Inducement count (dim 7) is weighted ×2** — the single most predictive feature. More sweeps = more liquidity cleared = larger expected move.

**KNN Risk Multiplier:**
- ≥70% confidence → 1.5× risk
- 50–69% → 1.0× risk
- <50% → 0.5× risk

**Logging outcomes** (how to train KNN):
1. After trade closes, set **Log Outcome** to `0` (Loss), `1` (Win), or `2` (Partial)
2. Wait 1 bar for it to register
3. Set back to `9` (Skip)
4. KNN memory improves after 50+ episodes. Becomes reliable at 200+.

---

## Session Times (EAT = UTC+3, No DST)

| Session | EAT | UTC |
|---|---|---|
| Asia | 03:00–10:00 | 00:00–07:00 |
| Frankfurt (FFT) | 10:00–11:00 | 07:00–08:00 |
| London Open | 11:00–12:00 | 08:00–09:00 |
| NY Open | 16:00–17:00 | 13:00–14:00 |
| NY Trap | 17:00–18:00 | 14:00–15:00 |
| London Close | 20:00–21:00 | 17:00–18:00 |

**MMM Windows** (±30 min):
- 11:30 EAT (London Open kill zone)
- 12:30 EAT (Post-London)
- 16:30 EAT (NY Open kill zone)
- 17:30 EAT (NY Trap)

---

## ADI Instrument Reference

| Instrument | Broker | Pip Value / Lot | Min Lot |
|---|---|---|---|
| XAUUSD | Pepperstone | $10.00/pip | 0.01 |
| XAUUSD | Deriv | $0.10/pt | 1 unit |
| GBPUSD | Pepperstone | $10.00/pip | 0.01 |
| Volatility 75 | Deriv | $1.00/pt | 1 unit |
| Volatility 50 | Deriv | $1.00/pt | 1 unit |
| Volatility 25 | Deriv | $0.10/pt | 1 unit |
| Volatility 10 | Deriv | $0.10/pt | 1 unit |
| Step Index | Deriv | $1.00/pt | 1 unit |

---

## Non-Negotiable Rules

1. **3-Rule OB Gate is binary** — any rule fails = zone dead. No scoring, no partial credit.
2. **50% P/D Gate is a hard stop** — `SUPPRESS ⛔` on dashboard = no entries from that bias direction.
3. **Never trade OB Type SMT⚠** — it has no inducement and will be targeted as liquidity.
4. **MSS must be VALID for REVERSAL signals** — if MSS row shows `MSS?`, that is IPB territory only.
5. **IPB is aggressive** — if MSS does not confirm after an IPB entry, exit the position.
6. **KNN scales risk only** — it never blocks a signal. 30% confidence = 0.5× risk, still a valid trade.
7. **Position tool is replaced on every new signal** — only the most recent SL/TP set is shown.
8. **Zero repaint** — all signals use `barstate.isconfirmed`. Structure pivots confirm `sw_eff` bars late by design.

---

## Zero Repaint Guarantee

PIE-v1 is structurally zero-repaint:
- All signals are gated by `barstate.isconfirmed` — labels appear only after the bar closes
- Structure detection uses `ta.pivothigh/low` which by design confirms `sw_eff` bars after the pivot bar — those bars are already history
- `ta.atr(14)` is computed at script scope every bar — no conditional series calls
- HTF data uses `lookahead=barmerge.lookahead_off` — no future data leakage
- `var` state variables only update on confirmed bars

---

## Color Reference

| Color | Element |
|---|---|
| #00e676 Green | Bullish OBs, TP lines, bull signals |
| #ff1744 Red | Bearish OBs, SL line, bear signals |
| #ffd600 Yellow | MMM background, neutral labels |
| #ff9800 Orange | Vector Level line |
| #546e7a Gray | Asia range box |
| Purple | RSI divergence labels |
| Cyan vertical | London Open separator |
| Purple vertical | NY Open separator |

---

*PIE-v1 | Absolute Dollar Intelligence*
*Based on VectorFX 2-Phase Inducement Trap Theorem*
*ADI Internal Use Only — Emmanuel, Nairobi EAT/UTC+3*
