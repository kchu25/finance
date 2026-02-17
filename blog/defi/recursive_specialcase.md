@def title = "Recursive Collateralization: Special Case — 1000 LINK, \$2100 Already Borrowed"
@def published = "13 February 2026"
@def tags = ["defi", "quant"]

# Recursive Collateralization: Special Case
## 1000 LINK at \$8.40, with \$2100 USDC Already Borrowed

\newcommand{\LTV}{\text{LTV}}
\newcommand{\LT}{\text{LT}}
\newcommand{\HF}{\text{HF}}

@@toc@@

---

## 1. Your Current Position

You've already deposited **1000 LINK** as collateral on Aave and borrowed **\$2,100 USDC**. LINK is at \$8.40. This is *not* a fresh loop from zero — you're already mid-position.

| Metric | Value |
| --- | --- |
| Collateral | 1,000 LINK × \$8.40 = **\$8,400** |
| Debt | **\$2,100** USDC |
| Net Equity | **\$6,300** |
| Current LTV | $2100 / 8400 = $ **25.0%** |
| Health Factor | $\LT / \LTV = 0.83 / 0.25 = $ **3.32** |
| Effective Leverage | $8400 / 6300 = $ **1.33×** |
| Max Drop Tolerance | $1 - 1/\HF = 1 - 1/3.32 = $ **69.9%** |
| Liquidation Price | $D / (Q \times \LT) = 2100 / (1000 \times 0.83) = $ **\$2.53** |

> **Status**: This position is extremely safe. A **70% crash** (LINK to \$2.53) is needed for liquidation. Your HF of 3.32 is very healthy. You have a lot of room to add leverage if you want.

---

## 2. How This Differs from a Clean Loop

In the [standard recursive model](/blog/defi/recursive/), you start fresh: deposit $Q_0$ LINK, and every borrow is immediately cycled into more LINK. The resulting formulas are clean because everything scales with $\ell / (1 - \ell)$.

Here, you already have a **partial position**: 1000 LINK deposited, \$2,100 borrowed. The \$2,100 might have gone to anything — it doesn't matter. What matters now is:

$$\text{Remaining borrow capacity} = Q \cdot P \cdot \ell_{\text{target}} - D_{\text{existing}}$$

where $\ell_{\text{target}}$ is the LTV you want to loop at going forward.

### 2.1 The Key Formula Change

In a clean loop starting from $Q_0$ tokens:

$$D_{\text{total}} = \frac{Q_0 P \ell}{1 - \ell}, \qquad Q_{\text{total}} = \frac{Q_0}{1 - \ell}$$

In your case, the existing debt shifts the starting point. You have $Q_0 = 1000$ LINK and $D_0 = 2100$ already locked in. The remaining borrowing capacity at target LTV $\ell$ is:

$$\Delta D = Q_0 P \ell - D_0 = 8400\ell - 2100$$

This $\Delta D$ is what you can use to buy new LINK and start the recursive loop. The new LINK purchased in the first new round:

$$\Delta Q_1 = \frac{\Delta D}{P} = \frac{8400\ell - 2100}{8.40}$$

From there, the standard geometric series kicks in — each subsequent round gives you a factor of $\ell$ of the previous round's LINK. The total *new* LINK from looping:

$$\Delta Q_{\text{total}} = \frac{\Delta Q_1}{1 - \ell} = \frac{8400\ell - 2100}{8.40(1 - \ell)}$$

And the total *new* debt:

$$\Delta D_{\text{total}} = \frac{\Delta D}{1 - \ell} = \frac{8400\ell - 2100}{1 - \ell}$$

### 2.2 Final State After Full Loop

$$\boxed{Q_{\text{final}} = 1000 + \frac{8400\ell - 2100}{8.40(1 - \ell)}}$$

$$\boxed{D_{\text{final}} = 2100 + \frac{8400\ell - 2100}{1 - \ell}}$$

**Equity check**: Your equity should remain \$6,300 throughout (looping doesn't create or destroy equity):

$$Q_{\text{final}} \times P - D_{\text{final}} = 6300 \quad \checkmark$$

---

## 3. What Happens at Each Target LTV

Starting from 1000 LINK / \$2,100 debt, looping the remaining capacity:

### 3.1 Results Table

| Target LTV ($\ell$) | Remaining Capacity | Final LINK | Final Debt | Leverage | Liq Price | Max Drop |
| --- | --- | --- | --- | --- | --- | --- |
| 0.25 (stay put) | \$0 | 1,000 | \$2,100 | 1.33× | \$2.53 | 69.9% |
| 0.40 | \$1,260 | 1,250 | \$4,200 | 1.67× | \$4.05 | 51.8% |
| 0.50 | \$2,100 | 1,500 | \$6,300 | 2.00× | \$5.06 | 39.8% |
| 0.55 | \$2,520 | 1,667 | \$7,700 | 2.22× | \$5.57 | 33.7% |
| 0.60 | \$2,940 | 1,875 | \$9,450 | 2.50× | \$6.07 | 27.7% |

### 3.2 Interpretation

At your current LTV of 25%, you're barely leveraged (1.33×). You could:

- **Stay at 25%**: Sleep peacefully. Liquidation at \$2.53 is almost impossible.
- **Loop to 40%**: Modest 1.67× leverage, survives a 52% crash (LINK to \$4.05). Very conservative.
- **Loop to 50%**: 2× leverage, survives 40% crash (LINK to \$5.06). This is the [recommended sweet spot](/blog/defi/recursive/#the-honest-assessment).
- **Loop to 60%**: 2.5× leverage, but only survives 28% crash (LINK to \$6.07). Getting risky.

---

## 4. Step-by-Step: Looping to 50% LTV

Since LTV 0.50 is the recommended target, here's the round-by-round breakdown.

**Starting state**: 1000 LINK deposited, \$2,100 debt

**Remaining capacity**: $1000 \times 8.40 \times 0.50 - 2100 = \$2,100$

| Round | Action | LINK Added | New Debt | Cumulative LINK | Cumulative Debt |
| --- | --- | --- | --- | --- | --- |
| — | Starting position | — | — | 1,000 | \$2,100 |
| 1 | Borrow \$2,100 → buy 250 LINK → deposit | 250 | \$2,100 | 1,250 | \$4,200 |
| 2 | Borrow \$1,050 → buy 125 LINK → deposit | 125 | \$1,050 | 1,375 | \$5,250 |
| 3 | Borrow \$525 → buy 63 LINK → deposit | 63 | \$525 | 1,438 | \$5,775 |
| 4 | Borrow \$263 → buy 31 LINK → deposit | 31 | \$263 | 1,469 | \$6,038 |
| 5 | Borrow \$131 → buy 16 LINK → deposit | 16 | \$131 | 1,484 | \$6,169 |
| ∞ | (converged) | — | — | **1,500** | **\$6,300** |

> After 3 rounds you're at 96% of the theoretical maximum. After 4 rounds, 98%. In practice, 3–4 rounds is enough.

---

## 5. P\&L Scenarios

### 5.1 Current Position (No Additional Looping)

With 1000 LINK and \$2,100 debt, your equity is \$6,300:

| LINK Price | Equity | P\&L on \$6,300 | HF |
| --- | --- | --- | --- |
| \$4.00 | \$1,900 | **−69.8%** | 1.58 |
| \$5.00 | \$2,900 | **−54.0%** | 1.98 |
| \$6.00 | \$3,900 | **−38.1%** | 2.37 |
| \$7.00 | \$4,900 | **−22.2%** | 2.77 |
| \$8.00 | \$5,900 | **−6.3%** | 3.16 |
| \$10.00 | \$7,900 | **+25.4%** | 3.95 |
| \$12.00 | \$9,900 | **+57.1%** | 4.74 |
| \$15.00 | \$12,900 | **+104.8%** | 5.93 |
| \$20.00 | \$17,900 | **+184.1%** | 7.90 |
| \$30.00 | \$27,900 | **+342.9%** | 11.86 |
| \$50.00 | \$47,900 | **+660.3%** | 19.76 |

### 5.2 After Looping to 50% LTV (1500 LINK, \$6,300 Debt)

| LINK Price | Equity | P\&L on \$6,300 | HF | Status |
| --- | --- | --- | --- | --- |
| \$4.00 | −\$300 | **−104.8%** | 0.79 | ⚠️ Liquidated |
| \$5.00 | \$1,200 | **−81.0%** | 0.99 | ⚠️ Liquidated |
| \$6.00 | \$2,700 | **−57.1%** | 1.19 | Alive (barely) |
| \$7.00 | \$4,200 | **−33.3%** | 1.38 | ⚠️ Danger zone |
| \$8.00 | \$5,700 | **−9.5%** | 1.58 | OK |
| \$10.00 | \$8,700 | **+38.1%** | 1.98 | Healthy |
| \$12.00 | \$11,700 | **+85.7%** | 2.37 | ✅ Comfortable |
| \$15.00 | \$16,200 | **+157.1%** | 2.96 | ✅ Strong |
| \$20.00 | \$23,700 | **+276.2%** | 3.95 | ✅ Very strong |
| \$30.00 | \$38,700 | **+514.3%** | 5.93 | 🚀 |
| \$50.00 | \$68,700 | **+990.5%** | 9.88 | 🚀🚀 |

### 5.3 After Looping to 60% LTV (1875 LINK, \$9,450 Debt)

| LINK Price | Equity | P\&L on \$6,300 | HF | Status |
| --- | --- | --- | --- | --- |
| \$4.00 | −\$1,950 | **−131.0%** | 0.66 | ⚠️ Liquidated |
| \$5.00 | −\$75 | **−101.2%** | 0.82 | ⚠️ Liquidated |
| \$6.00 | \$1,800 | **−71.4%** | 0.99 | ⚠️ Liquidated |
| \$7.00 | \$3,675 | **−41.7%** | 1.15 | Alive (barely) |
| \$8.00 | \$5,550 | **−11.9%** | 1.32 | ⚠️ Low HF |
| \$10.00 | \$9,300 | **+47.6%** | 1.65 | OK |
| \$15.00 | \$18,675 | **+196.4%** | 2.47 | ✅ Strong |
| \$20.00 | \$28,050 | **+345.2%** | 3.29 | ✅ Very strong |
| \$50.00 | \$84,300 | **+1238.1%** | 8.23 | 🚀🚀🚀 |

### 5.4 Side-by-Side Comparison

At key LINK prices, return on \$6,300 equity:

| LINK Price | Stay (1.33×) | Loop 50% (2.0×) | Loop 60% (2.5×) |
| --- | --- | --- | --- |
| \$5.00 | −54% | ⚠️ Liq | ⚠️ Liq |
| \$6.00 | −38% | −57% | ⚠️ Liq |
| \$8.00 | −6% | −10% | −12% |
| \$12.00 | +57% | +86% | +107% |
| \$20.00 | +184% | +276% | +345% |
| \$50.00 | +660% | +991% | +1238% |

> The leverage amplifies both directions. At 2.0× you roughly double both gains and losses relative to 1.33×. At 2.5× you roughly triple them.

---

## 6. Free-Ride Exit Strategy

The [free-ride concept](/blog/defi/math_adv/): sell enough LINK to repay all debt, then the rest is yours — zero risk, pure upside.

### 6.1 Minimum Free-Ride Price

The minimum price to free-ride is your **effective cost basis** (total debt / total LINK):

| Position | Total LINK | Total Debt | Cost Basis | Min Free-Ride Price |
| --- | --- | --- | --- | --- |
| Stay (25% LTV) | 1,000 | \$2,100 | \$2.10 | **\$2.10** |
| Loop to 40% | 1,250 | \$4,200 | \$3.36 | **\$3.36** |
| Loop to 50% | 1,500 | \$6,300 | \$4.20 | **\$4.20** |
| Loop to 60% | 1,875 | \$9,450 | \$5.04 | **\$5.04** |

> Your current position has a cost basis of only **\$2.10/LINK**. Even at 50% LTV it's \$4.20. These are well below the current price, meaning you can free-ride at *any price above the cost basis*.

### 6.2 Free-Ride Outcomes at Target Prices

**After looping to 50% LTV** (1,500 LINK, \$6,300 debt):

| Sell at | LINK Sold | LINK Kept (Free) | Value of Free LINK |
| --- | --- | --- | --- |
| \$12 | 525 | **975** | **\$11,700** |
| \$15 | 420 | **1,080** | **\$16,200** |
| \$20 | 315 | **1,185** | **\$23,700** |
| \$30 | 210 | **1,290** | **\$38,700** |

**After looping to 60% LTV** (1,875 LINK, \$9,450 debt):

| Sell at | LINK Sold | LINK Kept (Free) | Value of Free LINK |
| --- | --- | --- | --- |
| \$12 | 788 | **1,088** | **\$13,050** |
| \$15 | 630 | **1,245** | **\$18,675** |
| \$20 | 473 | **1,402** | **\$28,050** |
| \$30 | 315 | **1,560** | **\$46,800** |

> At 50% LTV: if LINK hits \$20, you sell 315 LINK (21% of position) to repay all debt, and keep **1,185 LINK completely free**. That's worth \$23,700 with zero risk.
>
> At 60% LTV: same \$20 target, sell 473 LINK, keep **1,402 LINK free** worth \$28,050. More LINK kept, but you were closer to liquidation on the way there.

---

## 7. Interest Cost Analysis

At 5% APR borrow rate:

| Position | Debt | Monthly Interest | Annual Interest | % of Equity |
| --- | --- | --- | --- | --- |
| Stay (25% LTV) | \$2,100 | \$8.75 | \$105 | 1.7% |
| Loop to 40% | \$4,200 | \$17.50 | \$210 | 3.3% |
| Loop to 50% | \$6,300 | \$26.25 | \$315 | 5.0% |
| Loop to 60% | \$9,450 | \$39.38 | \$473 | 7.5% |

At your current 25% LTV, you're paying only \$8.75/month. Even at 50% LTV it's \$26.25/month — manageable.

**Break-even**: LINK needs to appreciate by the interest cost / position value to break even:

| Position | Annual Interest | Position Value | Break-Even Move |
| --- | --- | --- | --- |
| Stay (25% LTV) | \$105 | \$8,400 | **+1.2%** |
| Loop to 50% | \$315 | \$12,600 | **+2.5%** |
| Loop to 60% | \$473 | \$15,750 | **+3.0%** |

> These are tiny hurdles. LINK needs to go up just 2.5% in a year to cover the borrow cost at 50% LTV.

---

## 8. Liquidation Risk: Mapping to Probability

From the [probability analysis](/blog/defi/prob_link/), the estimated probability of LINK touching various prices within 1 year:

| Position | Liq Price | Drop | ~P(Liquidation, 1yr) |
| --- | --- | --- | --- |
| Stay (25% LTV) | \$2.53 | −70% | **~2%** |
| Loop to 40% | \$4.05 | −52% | **~10%** |
| Loop to 50% | \$5.06 | −40% | **~22%** |
| Loop to 55% | \$5.57 | −34% | **~30%** |
| Loop to 60% | \$6.07 | −28% | **~45%** |

> Your current position has roughly a **2% chance** of liquidation in the next year. Looping to 50% raises it to **~22%** — acceptable for high-conviction. Looping to 60% puts it at **~45%** — a coin flip.

---

## 9. The Generalized Formula

For any starting position with $Q$ tokens at price $P$, existing debt $D_0$, looping at target LTV $\ell$:

$$\boxed{
\begin{aligned}
\text{Remaining capacity} &= QP\ell - D_0 \\[6pt]
Q_{\text{final}} &= Q + \frac{QP\ell - D_0}{P(1 - \ell)} \\[6pt]
D_{\text{final}} &= D_0 + \frac{QP\ell - D_0}{1 - \ell} \\[6pt]
\text{Equity} &= QP - D_0 \quad \text{(unchanged by looping)} \\[6pt]
P_{\text{liq}} &= \frac{D_{\text{final}}}{Q_{\text{final}} \times \LT} \\[6pt]
\text{Leverage} &= \frac{Q_{\text{final}} \times P}{\text{Equity}} = \frac{Q_{\text{final}} \times P}{QP - D_0}
\end{aligned}
}$$

**Constraint**: You can only loop if $QP\ell > D_0$, i.e., the target LTV is above your current LTV:

$$\ell > \frac{D_0}{QP} = \LTV_{\text{current}}$$

### 9.1 Sanity Check

Plugging in $Q = 1000$, $P = 8.40$, $D_0 = 2100$, $\ell = 0.50$:

$$Q_{\text{final}} = 1000 + \frac{8400 \times 0.50 - 2100}{8.40 \times 0.50} = 1000 + \frac{2100}{4.20} = 1000 + 500 = 1500 \; \checkmark$$

$$D_{\text{final}} = 2100 + \frac{2100}{0.50} = 2100 + 4200 = 6300 \; \checkmark$$

$$P_{\text{liq}} = \frac{6300}{1500 \times 0.83} = \frac{6300}{1245} = \$5.06 \; \checkmark$$

---

## 10. Recommendation for This Specific Position

### 10.1 Option A: Do Nothing (Keep 25% LTV)

✅ Nearly zero liquidation risk (\$2.53 liq price — only 2% probability)

✅ Interest cost is only \$8.75/month

❌ Minimal leverage (1.33×) — not capturing much upside amplification

❌ The \$2,100 borrowed is costing you interest for very little benefit

**Best if**: You don't want any additional risk and are just holding LINK with a small borrow for other purposes.

### 10.2 Option B: Loop to 40–45% LTV

✅ Moderate leverage (1.67×), survives 52% crash to \$4.05

✅ Still very safe — liquidation probability ~10%

✅ Interest only \$17.50/month

**Best if**: You're bullish but cautious. This gets you meaningful upside amplification while keeping the liquidation price below the 2022 bear bottom.

### 10.3 Option C: Loop to 50% LTV ⭐ Recommended

✅ 2× leverage — doubles your effective LINK exposure to 1,500

✅ Survives 40% crash to \$5.06 (near the 2022 bottom)

✅ Free-ride at \$20: keep 1,185 LINK worth \$23,700

⚠️ Liquidation probability ~22% over 1 year — real but acceptable for high-conviction

⚠️ Interest \$26.25/month — need LINK +2.5% to break even

**Best if**: You believe the thesis (institutional adoption, GENIUS Act) and accept that there's roughly a 1-in-5 chance of getting liquidated over the next year.

### 10.4 Option D: Loop to 60% LTV

⚠️ 2.5× leverage — 1,875 LINK

❌ Liquidation at \$6.07 — only 28% below current price

❌ Liquidation probability ~45% — almost a coin flip

❌ A single bad month in crypto could wipe you out

**Best if**: You are extremely high conviction *and* have external capital to add collateral in a crash. Otherwise, don't.

### 10.5 The Verdict

> **Loop to 50% LTV.** You go from 1,000 to 1,500 LINK and from \$2,100 to \$6,300 debt. Your leverage doubles from 1.33× to 2.0×. Your liquidation price moves from \$2.53 to \$5.06 — still below the 2022 bear market bottom of \$5.30.
>
> You're already sitting on a very safe position. Capturing the upside thesis without going past the 50% LTV sweet spot is the right move.
