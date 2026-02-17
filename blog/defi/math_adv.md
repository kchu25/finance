@def title = "Crypto Lending Risk Analysis: Advanced Playbook"
@def published = "13 February 2026"
@def tags = ["defi"]

# Crypto Lending Risk Analysis: Advanced Playbook
## Practical Tricks for "Deposit A, Borrow Stablecoin, Buy B"

This builds on the [math cheat sheet](/blog/defi/math/). That doc covers the formulas. This one covers **how to think about risk** when your actual goal is: deposit token A as collateral, borrow stablecoins, buy token B.

@@toc@@

---

## 1. The Setup: What You're Actually Doing

The most common DeFi lending play:

1. You own token A (e.g., ETH)
2. Deposit A as collateral into Aave/Compound
3. Borrow USDC (stablecoin)
4. Buy token B (e.g., LINK) with the USDC

**Your P\&L has three independent legs:**

| Leg | Exposure | Helps You | Hurts You |
| --- | --- | --- | --- |
| Token A (collateral) | Long | A goes up (more health) | A goes down (closer to liquidation) |
| Stablecoin debt | Short | N/A (stable, but interest accrues) | Interest cost |
| Token B (purchased) | Long | B goes up (that's the whole point) | B goes down (you lose money) |

> **The critical asymmetry**: Token B going up makes you money but does NOT improve your health factor. Token A going down triggers liquidation even if Token B is mooning.

---

## 2. The Correlation Question

### 2.1 Why It's the Most Important Factor

Your **real risk** isn't just "how much can A drop?" — it's "how much can A drop while B also drops?"

If A and B are highly correlated (both crypto), the nightmare scenario is:
- A drops 30% → you get liquidated
- B also dropped 30% → the asset you bought is now underwater too
- You lost collateral AND the investment

If A and B are uncorrelated or negatively correlated, a drop in A doesn't necessarily mean B dropped too.

### 2.2 Correlation Buckets

| Collateral A → Buy B | Correlation | Risk Level | Notes |
| --- | --- | --- | --- |
| ETH → buy LINK | High (~0.7-0.9) | ⚠️ High | Both follow crypto market cycles |
| ETH → buy BTC | High (~0.8) | ⚠️ High | Slightly safer since BTC is less volatile |
| ETH → buy tokenized gold | Low (~0.1) | ✅ Lower | Gold doesn't track crypto |
| ETH → buy stablecoin yield | Zero | ✅ Lowest | B can't go down (but yield is small) |
| stETH → buy ETH | ~1.0 | Special case | Near-zero liquidation risk (same asset) |

### 2.3 The Practical Rule

> **If A and B are correlated (both crypto)**: Assume the worst case is A drops X% and B drops ~X% too. Your total loss in a crash is:
> 
> $$\text{Loss} = \underbrace{V_c \times x}_{\text{collateral loss}} + \underbrace{V_B \times x}_{\text{investment loss}}$$
> 
> Both sides of the trade go against you simultaneously.

> **If A and B are uncorrelated**: You can lose on one side without losing on the other. This is strictly better risk management.

### 2.4 How to Use This

**Before opening a position, ask:** "In a crypto crash, will both my collateral and my investment drop together?"

If yes → you need a much larger safety buffer (lower LTV).

If no → your stated LTV buffer is closer to your actual risk.

---

## 3. The "Borrow Stable, Buy Volatile" Structure

### 3.1 Why This Is the Standard Play

Borrowing a stablecoin (USDC, DAI) to buy a volatile asset means your **debt is fixed in dollar terms**. This is important:

- If you borrow 10,000 USDC → you always owe 10,000 USDC (plus interest)
- Your debt doesn't fluctuate with the market
- Only your collateral side moves

This is much simpler than borrowing a volatile asset (where debt value also changes).

### 3.2 Why You (Almost) Never Borrow Volatile to Buy Volatile

Borrowing ETH to buy LINK means:
- Collateral (say, WBTC) can drop → liquidation
- Debt (ETH) can go *up* → liquidation (you owe more!)
- Now you have **two ways to get liquidated** instead of one

The health factor becomes:

$$\text{HF} = \frac{V_c \times \text{LT}}{V_d}$$

If $V_c$ drops **or** $V_d$ rises, you're in trouble.

**Exception**: Borrowing ETH against stETH. Since stETH ≈ ETH in price, both sides move together and your LTV stays roughly constant. This is a "carry trade" — you earn the staking yield spread.

---

## 4. Position Sizing: The Pre-Trade Checklist

Before entering any "deposit A, borrow stable, buy B" position:

### Step 1: Decide Your Max Tolerable Drop

How much can token A realistically drop in a single crash?

| Token Type | Historical Max Drawdown | Suggested Buffer |
| --- | --- | --- |
| BTC | ~75% (2022) | Plan for 50%+ |
| ETH | ~80% (2022) | Plan for 50-60% |
| Large-cap alt (LINK, SOL) | ~85-90% | Plan for 60-70% |
| Small-cap alt | ~95%+ | Don't use as collateral |

### Step 2: Calculate Your LTV From the Buffer

Using the formula from the math sheet:

$$\text{LTV}_{\text{safe}} = \text{LT} \times (1 - x_{\text{buffer}})$$

| Buffer (survive this drop) | LT = 0.80 | LT = 0.75 |
| --- | --- | --- |
| 25% | 0.60 | 0.56 |
| 33% | 0.53 | 0.50 |
| 50% | 0.40 | 0.375 |
| 60% | 0.32 | 0.30 |

> **Example**: You want to survive a 50% drop in ETH collateral with LT = 0.80. Your safe LTV is $0.80 \times 0.50 = 0.40$. On \$10,000 ETH, borrow at most \$4,000.

### Step 3: Size the Purchase Based on Your Conviction

This is where it becomes personal. The LTV tells you how much you *can* borrow safely. Whether you *should* borrow that much depends on your expected return on B.

**Rough framework:**

| Expected Annual Return on B | Max Reasonable Leverage |
| --- | --- |
| < borrow rate | Don't borrow. Period. |
| 1-2x borrow rate | Minimal (LTV < 0.30) |
| 2-5x borrow rate | Moderate (LTV 0.30-0.50) |
| > 5x borrow rate (high conviction) | Aggressive (LTV 0.50-0.60) |

---

## 5. Monitoring: What to Watch and When to Act

### 5.1 The Three Alerts You Need

Set alerts for these **on your collateral token A**, not on B:

| Alert | Threshold | Action |
| --- | --- | --- |
| **Warning** | HF drops below 2.0 | Start watching closely |
| **Danger** | HF drops below 1.5 | Prepare to add collateral or repay |
| **Emergency** | HF drops below 1.2 | Act immediately: repay or add collateral |

### 5.2 Why You Monitor A, Not B

Your liquidation depends entirely on A. B could go to zero and your health factor doesn't change. B could 10x and your health factor doesn't change.

> **Common mistake**: People watch the price of the token they bought (B) and ignore the collateral (A). The collateral is the only thing that can kill your position.

### 5.3 The Asymmetry of Intervention

When HF is dropping, you have two options:

**Option 1: Add more collateral A**
- Increases $V_c$ → increases HF
- Costs you more capital
- Good if you think A is temporarily dipping

**Option 2: Repay some debt**
- Decreases $V_d$ → increases HF
- Requires selling some of B (or using other funds)
- Good if you think the decline is sustained

**Which is better?** It depends on whether you'd rather own more of A at the dip price or keep your B position intact. There's no universal answer.

---

## 6. The "Partial Liquidation" Trick

### 6.1 How Liquidation Actually Works

Most people think liquidation = lose everything. On Aave, it's usually **partial**:

- A liquidator repays up to **50% of your debt**
- They receive your collateral at a **discount** (typically 5-10%)
- Your remaining position has a **higher health factor** afterward

### 6.2 What This Means Strategically

If you're at HF = 0.95 (just below liquidation):

1. A liquidator repays 50% of your debt
2. They take collateral worth 105-110% of that debt
3. Your remaining debt is halved, your remaining collateral takes a ~5% haircut
4. Your HF is now back above 1

**You lost**: the liquidation penalty (5-10% of the liquidated amount)

**You kept**: roughly half your position, now at a healthier ratio

### 6.3 The Implication

**Liquidation isn't binary — it's a tax on poor risk management.** A partial liquidation on a large position might cost you 2-5% of total value, which hurts but isn't catastrophic.

This means: for large positions, being slightly aggressive on LTV is **less dangerous than most people think**, because you lose a penalty, not everything.

> **But**: don't rely on this. In extreme crashes, cascading liquidations can push prices down further, causing repeated partial liquidations that compound losses.

---

## 7. Flash Crash Protection: The Stablecoin Buffer

### 7.1 The Problem

Crypto can drop 20-40% in a single day. Your HF might be fine at 2.0 in the morning and at 1.1 by afternoon. You might not have time to react.

### 7.2 The Trick

Instead of depositing 100% of your capital as collateral A:

- Deposit 80% as collateral A
- Keep 20% as stablecoin (USDC/USDT) **in your wallet, not deposited**

When A crashes, you can **immediately swap the stablecoins to A at the dip price** and add to collateral. You're buying the dip and saving your position simultaneously.

### 7.3 The Math

Say you have \$10,000 total capital. Two strategies:

**Strategy 1: All-in collateral**
- Deposit \$10,000 ETH, borrow \$5,000 USDC (LTV = 0.50)
- ETH drops 40%: collateral = \$6,000, LTV = 0.83 → **liquidated** (if LT = 0.80)

**Strategy 2: Stablecoin buffer**
- Deposit \$8,000 ETH, borrow \$4,000 USDC (LTV = 0.50)
- Keep \$2,000 USDC in wallet
- ETH drops 40%: collateral = \$4,800, LTV = 0.83 → danger!
- **Immediately**: swap \$2,000 USDC for ETH (now cheaper), add as collateral
- New collateral: \$4,800 + \$2,000 = \$6,800, debt = \$4,000, LTV = 0.59 → **safe**

> The trade-off: you earn less supply APY on the portion not deposited. But you survive crashes that would have liquidated you.

---

## 8. The Time Dimension: Interest Accrual

### 8.1 Your Debt Grows Over Time

This is easy to forget: your debt is not static.

$$V_d(t) = V_d(0) \times (1 + r)^t$$

At 8% borrow rate:
- After 1 month: debt grows by ~0.67%
- After 6 months: ~4%
- After 1 year: ~8%

This means your **LTV creeps up over time even if prices don't move**.

### 8.2 How Fast Does LTV Drift?

Starting at LTV = 0.50 with 8% borrow rate, no price movement:

| Time | Debt Growth | New LTV | HF (LT=0.80) |
| --- | --- | --- | --- |
| Start | — | 0.500 | 1.60 |
| 3 months | +2% | 0.510 | 1.57 |
| 6 months | +4% | 0.520 | 1.54 |
| 1 year | +8% | 0.540 | 1.48 |
| 2 years | +17% | 0.583 | 1.37 |
| 3 years | +26% | 0.630 | 1.27 |

> Even with zero price movement, a 0.50 LTV position drifts to 0.63 in 3 years. That's a meaningful increase in risk.

### 8.3 The Implication

**Long-duration positions need periodic maintenance.** Either:
- Repay some debt periodically to reset LTV
- Add collateral periodically
- Or accept that your buffer is shrinking over time

> **Rule of thumb**: Check your position at least monthly. Repay enough to bring LTV back to your target every quarter.

---

## 9. Scenario Analysis: Build a Grid

### 9.1 The Two-Dimensional Grid

Before entering any position, build a grid of "what happens if A moves X% and B moves Y%":

**Setup**: Deposit \$10,000 ETH, borrow \$4,000 USDC (LTV = 0.40), buy \$4,000 of LINK

| | LINK −30% | LINK 0% | LINK +30% | LINK +100% |
| --- | --- | --- | --- | --- |
| **ETH −30%** | Collateral: \$7k, HF=1.40. LINK: \$2.8k. **Net: −\$4.2k** | HF=1.40. LINK: \$4k. **Net: −\$3k** | HF=1.40. LINK: \$5.2k. **Net: −\$1.8k** | HF=1.40. LINK: \$8k. **Net: +\$1k** |
| **ETH 0%** | HF=2.00. LINK: \$2.8k. **Net: −\$1.2k** | HF=2.00. LINK: \$4k. **Net: \$0** | HF=2.00. LINK: \$5.2k. **Net: +\$1.2k** | HF=2.00. LINK: \$8k. **Net: +\$4k** |
| **ETH +30%** | HF=2.60. LINK: \$2.8k. **Net: +\$1.8k** | HF=2.60. LINK: \$4k. **Net: +\$3k** | HF=2.60. LINK: \$5.2k. **Net: +\$4.2k** | HF=2.60. LINK: \$8k. **Net: +\$7k** |

*(Net = change in total equity including collateral appreciation, LINK value, minus the fixed \$4k debt. Ignoring interest for simplicity.)*

### 9.2 What the Grid Tells You

1. **The worst cell** (ETH −30%, LINK −30%): You lose \$4.2k but you're NOT liquidated (HF = 1.40). The conservative LTV saved you.

2. **LINK performance dominates P\&L**, but **ETH performance dominates survival**. Look at the rows: HF is the same across each row regardless of LINK.

3. **The high-conviction case**: Even if ETH drops 30%, if LINK does 100% you still make money. This is the scenario where borrowing to buy an asymmetric bet makes sense.

### 9.3 Build Your Own Grid

For any position:
1. Pick 3-4 scenarios for A (−40%, −20%, 0%, +20%)
2. Pick 3-4 scenarios for B (−30%, 0%, +30%, +100%)
3. For each cell, calculate HF and net P\&L
4. Check: **is there any cell where you get liquidated?** If yes, lower your LTV.

---

## 10. Exit Strategy: When to Close

### 10.1 Take-Profit Rules

If B goes up a lot, don't just sit there — your **absolute risk is unchanged** (HF depends on A, not B).

| B Performance | Action |
| --- | --- |
| B +50% | Consider selling 20-30% of B to repay part of debt |
| B +100% | Sell enough to repay full debt. **Free ride:** remaining B is now house money |
| B +200%+ | You already repaid. Enjoy the position risk-free. |

### 10.2 The "Free Ride" Target

The magic moment: B has gone up enough that selling *part* of it repays the entire loan.

$$B_{\text{free}} = B_{\text{initial}} \times \frac{V_d}{V_B}$$

If you borrowed \$4,000 to buy LINK at \$10 (400 LINK), and LINK goes to \$20:
- LINK position worth \$8,000
- Sell 200 LINK (\$4,000) → repay entire loan
- You still hold 200 LINK (\$4,000) at zero cost basis (relative to debt)

> **This is the real goal of leveraged buying.** Get to the free ride as fast as possible, then let the position run.

### 10.3 Stop-Loss Rules

If B goes down, the question is: cut loss or hold?

**Math-based approach**: If your expected return on B has changed (thesis broken), sell B, repay debt, recover collateral. Don't let a thesis trade become a hope trade.

**Time-based approach**: Set a deadline. "If B hasn't hit my target in 6 months, I close the position." This prevents indefinite interest bleed.

---

## 11. The Complete Checklist

Before entering a "deposit A, borrow stablecoins, buy B" position:

| # | Question | How to Answer |
| --- | --- | --- |
| 1 | What's my max expected drop for A? | Historical drawdown tables |
| 2 | What LTV keeps me safe through that drop? | $\text{LTV}_{\text{safe}} = \text{LT} \times (1 - x_{\text{drop}})$ |
| 3 | Does my expected return on B exceed the borrow rate? | $E[r_B] > r_{\text{borrow}}$ |
| 4 | Are A and B correlated? | If yes, assume both crash together |
| 5 | How long do I plan to hold? | Factor in interest drift on LTV |
| 6 | What's my free-ride price for B? | $P_{\text{free}} = P_{\text{entry}} \times \frac{V_d}{V_{B,\text{initial}}} + P_{\text{entry}}$ |
| 7 | What's my stop-loss? | Price or time-based |
| 8 | Do I have a stablecoin buffer for flash crashes? | 10-20% of capital as dry powder |
| 9 | Have I built the scenario grid? | A scenarios × B scenarios |
| 10 | Am I monitoring A (not just B)? | Set HF alerts at 2.0, 1.5, 1.2 |

---

## 12. Summary

The [math cheat sheet](/blog/defi/math/) gives you the formulas. Here's what to do with them:

1. **Correlation is everything.** If A and B crash together, your scenario analysis needs to reflect that.
2. **Borrow stablecoins, not volatile tokens.** One moving part (collateral) is enough.
3. **Size by max drop, not by max borrowing power.** Use $\text{LTV}_{\text{safe}} = \text{LT} \times (1 - x)$.
4. **Keep a stablecoin buffer.** 10-20% of capital not deposited, ready to save your position in a crash.
5. **Interest makes your LTV drift.** Check quarterly, repay periodically.
6. **Target the free ride.** Once B doubles, sell half to repay the loan entirely.
7. **Monitor A, not B.** B is your P\&L. A is your survival.
8. **Build the grid.** If any cell liquidates you, lower your LTV.
9. **Partial liquidation isn't death.** It's a 5-10% penalty, not a total loss. But don't rely on it.
10. **Set an exit.** Price-based or time-based. Don't let interest bleed indefinitely.
