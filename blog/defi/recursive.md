@def title = "Recursive Collateralization: The Looping Strategy"
@def published = "13 February 2026"
@def tags = ["crypto", "defi"]

# Recursive Collateralization: The Looping Strategy
## Deposit LINK → Borrow USDC → Buy LINK → Repeat

\newcommand{\LTV}{\text{LTV}}
\newcommand{\LT}{\text{LT}}
\newcommand{\HF}{\text{HF}}

@@toc@@

---

## 1. What Is Looping?

You start with some LINK. You deposit it as collateral on Aave, borrow USDC, buy more LINK, deposit that LINK too, borrow more, and keep going.

Each round you get a smaller increment, but the total adds up.

```text
Round 0:  1000 LINK → deposit as collateral
Round 1:  borrow USDC → buy ~600 LINK → deposit
Round 2:  borrow more USDC → buy ~360 LINK → deposit
Round 3:  borrow more → buy ~216 LINK → deposit
...
Final:    you control ~2500 LINK, owe ~\$12,750 USDC
```

This is leverage. Let's derive exactly how much.

---

## 2. The Math: Geometric Series

### 2.1 Setup

- $Q_0$ = initial LINK tokens (e.g., 1000)
- $P$ = current price per LINK
- $\ell$ = the LTV ratio you use each round (e.g., 0.60)
- $n$ = number of rounds

### 2.2 Each Round

| Round | LINK Deposited (This Round) | USDC Borrowed (This Round) | Cumulative LINK |
| --- | --- | --- | --- |
| 0 | $Q_0$ | — | $Q_0$ |
| 1 | $Q_0 \ell$ | $Q_0 P \ell$ | $Q_0(1 + \ell)$ |
| 2 | $Q_0 \ell^2$ | $Q_0 P \ell^2$ | $Q_0(1 + \ell + \ell^2)$ |
| 3 | $Q_0 \ell^3$ | $Q_0 P \ell^3$ | $Q_0(1 + \ell + \ell^2 + \ell^3)$ |
| $k$ | $Q_0 \ell^k$ | $Q_0 P \ell^k$ | $Q_0 \sum_{i=0}^{k} \ell^i$ |

Each round gives you a fraction $\ell$ of the previous round's tokens. It's a **geometric series**.

### 2.3 After $n$ Rounds

**Total LINK controlled:**

$$Q_n = Q_0 \sum_{k=0}^{n} \ell^k = Q_0 \cdot \frac{1 - \ell^{n+1}}{1 - \ell}$$

**Total debt (USDC):**

$$D_n = Q_0 P \sum_{k=1}^{n} \ell^k = Q_0 P \cdot \frac{\ell(1 - \ell^{n})}{1 - \ell}$$

### 2.4 The Infinite Limit (Full Loop)

As $n \to \infty$ (keep looping until increments are negligible):

$$\boxed{Q_\infty = \frac{Q_0}{1 - \ell}}$$

$$\boxed{D_\infty = \frac{Q_0 P \ell}{1 - \ell}}$$

**The leverage multiplier is simply:**

$$L = \frac{Q_\infty}{Q_0} = \frac{1}{1 - \ell}$$

### 2.5 Reference Table

Starting with **1000 LINK** at \$8.50 each (\$8,500 initial value):

| LTV ($\ell$) | Leverage | Total LINK | Total Debt | Net Equity |
| --- | --- | --- | --- | --- |
| 0.40 | 1.67x | 1,667 | \$5,667 | \$8,500 |
| 0.50 | 2.00x | 2,000 | \$8,500 | \$8,500 |
| 0.55 | 2.22x | 2,222 | \$10,389 | \$8,500 |
| 0.60 | 2.50x | 2,500 | \$12,750 | \$8,500 |
| 0.70 | 3.33x | 3,333 | \$19,833 | \$8,500 |
| 0.75 | 4.00x | 4,000 | \$25,500 | \$8,500 |

> **Notice**: Your net equity is always \$8,500 regardless of leverage. You're just deciding how many LINK tokens you control and how much debt you carry. The leverage amplifies both gains and losses.

---

## 3. Convergence: How Many Rounds Do You Actually Need?

You don't need to loop forever. The gains per round shrink exponentially.

At $\ell = 0.60$, starting with 1000 LINK:

| Round | LINK Added | Cumulative LINK | % of Final Total |
| --- | --- | --- | --- |
| 0 | 1000 | 1000 | 40.0% |
| 1 | 600 | 1600 | 64.0% |
| 2 | 360 | 1960 | 78.4% |
| 3 | 216 | 2176 | 87.0% |
| 4 | 130 | 2306 | 92.2% |
| 5 | 78 | 2383 | 95.3% |
| 6 | 47 | 2430 | 97.2% |
| ∞ | — | 2500 | 100% |

> **Practical rule**: 4-5 rounds gets you to ~92-95% of the theoretical maximum. After that, gas fees outweigh the incremental LINK. On L2s (Arbitrum, Optimism) where gas is cheap, you might do 6-7 rounds.

---

## 4. Liquidation Analysis

### 4.1 When Do You Get Liquidated?

Your total collateral and total debt after full looping:

$$V_c = Q_\infty \times P_{\text{current}} = \frac{Q_0 P_{\text{current}}}{1 - \ell}$$

$$V_d = D_\infty = \frac{Q_0 P_{\text{entry}} \ell}{1 - \ell}$$

Liquidation when $\LTV_{\text{current}} > \LT$ (the protocol's liquidation threshold):

$$\frac{V_d}{V_c} > \LT$$

$$\frac{Q_0 P_{\text{entry}} \ell / (1 - \ell)}{Q_0 P_{\text{current}} / (1 - \ell)} > \LT$$

The $(1 - \ell)$ and $Q_0$ cancel:

$$\frac{P_{\text{entry}} \cdot \ell}{P_{\text{current}}} > \LT$$

Solving for liquidation price:

$$\boxed{P_{\text{liq}} = P_{\text{entry}} \times \frac{\ell}{\LT}}$$

### 4.2 This Is Remarkably Clean

The liquidation price depends only on:
- Your entry price
- The LTV you used for looping
- The protocol's liquidation threshold

It does **not** depend on how many tokens you started with or how many rounds you did. The recursive structure collapses.

### 4.3 Liquidation Price Table

Entry price: \$8.50. Aave LINK liquidation threshold: $\LT = 0.71$.

| Loop LTV ($\ell$) | Liquidation Price | Drop Required |
| --- | --- | --- |
| 0.40 | \$4.79 | 44% |
| 0.45 | \$5.39 | 37% |
| 0.50 | \$5.99 | 30% |
| 0.55 | \$6.58 | 23% |
| 0.60 | \$7.18 | 16% |
| 0.65 | \$7.78 | 8% |

### 4.4 Max Drop Tolerance

Rearranging:

$$x_{\max} = 1 - \frac{\ell}{\LT}$$

| Loop LTV ($\ell$) | Max Drop Before Liquidation |
| --- | --- |
| 0.40 | **44%** |
| 0.45 | **37%** |
| 0.50 | **30%** |
| 0.55 | **23%** |
| 0.60 | **16%** |
| 0.65 | **8%** |

---

## 5. P\&L: How Much Do You Make (or Lose)?

### 5.1 The Amplified Return

If LINK moves by $r$% (e.g., +50% means $r = 0.50$):

$$\text{P\&L} = Q_\infty \times P_{\text{entry}} \times r - D_\infty \times r_{\text{borrow}} \times t$$

Your **net return on equity** after time $t$ (in years):

$$R_{\text{net}} = \underbrace{L \times r}_{\text{amplified return}} - \underbrace{\frac{\ell}{1 - \ell} \times r_{\text{borrow}} \times t}_{\text{interest cost}}$$

where $L = \frac{1}{1 - \ell}$ is the leverage multiplier.

### 5.2 Return Table

Starting with 1000 LINK at \$8.50, borrowing at 5% APR, holding for 1 year:

| Loop LTV | Leverage | LINK +50% | LINK +100% | LINK +200% | LINK −20% |
| --- | --- | --- | --- | --- | --- |
| 0.40 | 1.67x | **+80%** | **+163%** | **+330%** | −37% |
| 0.45 | 1.82x | **+87%** | **+178%** | **+360%** | −40% |
| 0.50 | 2.00x | **+95%** | **+195%** | **+395%** | −45% |
| 0.55 | 2.22x | **+106%** | **+218%** | **+440%** | −49% |
| 0.60 | 2.50x | **+118%** | **+243%** | **+493%** | ⚠️ liquidated |

*(Returns are on your original \$8,500 equity. Interest cost deducted. LINK −20% at 0.60 LTV crosses the 16% liquidation threshold.)*

### 5.3 The Break-Even Move

How much does LINK need to rise just to cover the borrow cost?

$$r_{\text{break-even}} = \frac{\ell \times r_{\text{borrow}} \times t}{1}$$

Wait — that's just the interest on your debt divided by your total exposure. More precisely:

$$r_{\text{break-even}} = \frac{D_\infty \times r_{\text{borrow}} \times t}{Q_\infty \times P} = \ell \times r_{\text{borrow}} \times t$$

At 0.60 LTV, 5% borrow rate, 1 year:

$$r_{\text{break-even}} = 0.60 \times 0.05 \times 1 = 3\%$$

LINK only needs to go up **3% in a year** to cover your borrowing cost. At 0.70 LTV: 3.5%. These are low hurdles.

---

## 6. Should You Do This With LINK at \$8.50?

### 6.1 The Case FOR Looping LINK Right Now

**1. You're near the historical floor.**

LINK's all-time high was ~\$52. It spent most of 2024-2025 between \$10-25. At \$8.50 you're at or near the lowest levels in years. This means:

$$x_{\text{further downside}} \text{ is bounded}$$

How much lower can LINK realistically go? To \$5? \$3? LINK has a functioning ecosystem, \$28T in transaction value enabled, institutional integrations. A drop below \$5 implies existential failure of the project, which is a low-probability event.

**2. Asymmetric risk/reward at the floor.**

At \$8.50:
- **Downside to \$4 (53% drop):** You lose your position (at 0.60 LTV you get liquidated at ~\$7.18, so actually less)
- **Upside to \$20 (135% gain):** Your equity roughly triples at 2.5x leverage
- **Upside to \$50 (488% gain):** Your equity does ~12x at 2.5x leverage

The distribution is skewed: limited downside (floor is nearby), large upside (return to prior levels).

**3. Borrow rates are manageable.**

5-8% APR on stablecoin borrows is a small cost relative to the potential move. LINK going from \$8.50 to \$15 (76% up) makes the 5% borrow cost irrelevant.

**4. The macro thesis supports timing.**

GENIUS Act, institutional tokenization, CCIP adoption — the [investment thesis](/blog/chainlink/oracle_platform/) suggests structural demand growth. If the thesis is right, buying near the floor with moderate leverage is optimal timing.

### 6.2 The Case AGAINST Looping LINK Right Now

**1. "Historical floor" is a narrative, not a guarantee.**

There is no law of physics that prevents LINK from going to \$3 or \$2 or \$1. "It's at the floor" has been said at every price on the way down. The 2022 bear market took LINK from \$50 to \$5.

**2. Crypto correlations spike in crashes.**

In a broad crypto crash, LINK drops with everything else. If the market enters another bear cycle, LINK could easily drop 50-70% from here — and your looped position gets liquidated.

**3. Interest accrues regardless.**

At 2.5x leverage (0.60 LTV) with 5% borrow rate:
- You owe \$12,750 in debt
- Interest: ~\$637/year (\$53/month)
- If LINK goes sideways for 2 years, you've paid ~\$1,274 in interest (15% of equity) for nothing

**4. Looping is same-asset exposure: no diversification.**

Your collateral IS your investment. If LINK drops, both your collateral and your investment drop simultaneously. There's no hedge. This is the maximum correlation scenario ($\rho = 1$).

**5. Smart contract risk is real.**

Your entire position lives on Aave. A smart contract exploit, oracle manipulation, or governance attack could cause losses beyond what the math predicts.

### 6.3 The Honest Assessment

| Factor | Verdict |
| --- | --- |
| Current price relative to history | ✅ Strong — near multi-year lows |
| Fundamental thesis | ✅ Strong — institutional adoption is real |
| Downside protection from floor | ⚠️ Moderate — floors can break |
| Same-asset correlation ($\rho = 1$) | ❌ Maximum risk — no hedge |
| Interest cost at moderate LTV | ✅ Low — easily covered by small move |
| Liquidation risk at 0.40-0.50 LTV | ✅ Manageable — requires 30-44% drop |
| Liquidation risk at 0.60+ LTV | ❌ Dangerous — only 16% buffer or less |

### 6.4 Recommendation

> **If you're going to loop LINK at \$8.50:**
> 
> 1. **Use LTV ≤ 0.45** (1.82x leverage, survives a 37% drop to ~\$5.39)
> 2. **Keep a stablecoin buffer** (10-20% of position value) outside Aave for emergency collateral top-ups
> 3. **Set a time limit** (6-12 months). If the thesis hasn't played out, unwind.
> 4. **Set a free-ride target**: LINK doubles to \$17 → sell half the looped LINK → repay all debt → rest is free
> 5. **Do NOT use LTV > 0.55.** At \$8.50, a dip to \$7 (18% drop) is entirely possible in a bad week, and 0.60 LTV gets liquidated at just a 16% drop.

---

## 7. Comparison: Loop at the Floor vs. Loop at ATH

This is why *when* you loop matters as much as *how much*:

| | Loop at \$8.50 (floor) | Loop at \$40 (near ATH) |
| --- | --- | --- |
| **Downside to \$5** | 41% drop | 88% drop |
| **Upside to \$50** | 488% gain | 25% gain |
| **Risk/reward at 2x leverage** | Lose ~82% or gain ~976% | Lose ~176% (liquidated) or gain ~50% |
| **Liquidation price (0.50 LTV)** | \$5.99 | \$28.17 |
| **Probability of liquidation** | Low (need to break historical support) | High (normal crypto volatility) |

> **The key insight**: Looping is **least dangerous near the floor** because:
> 1. The percentage drop to liquidation is a larger absolute move
> 2. The upside is much larger than the downside
> 3. Buying near support means you're leveraging into the asymmetry

This is the opposite of what most people do (they loop after big runs, near the top, when they're most excited and the risk/reward is worst).

---

## 8. The Full Picture

### 8.1 Summary of Formulas

$$\boxed{
\begin{aligned}
\text{Total LINK} &= \frac{Q_0}{1 - \ell} \\[6pt]
\text{Total Debt} &= \frac{Q_0 P \ell}{1 - \ell} \\[6pt]
\text{Leverage} &= \frac{1}{1 - \ell} \\[6pt]
\text{Liquidation Price} &= P_{\text{entry}} \times \frac{\ell}{\LT} \\[6pt]
\text{Max Drop} &= 1 - \frac{\ell}{\LT} \\[6pt]
\text{Net Return} &= \frac{r}{1 - \ell} - \frac{\ell \cdot r_{\text{borrow}} \cdot t}{1 - \ell}
\end{aligned}
}
$$

### 8.2 The One-Sentence Version

Recursive collateralization is a geometric series that converges to $\frac{1}{1-\ell}$ leverage. At \$8.50 near the historical floor, moderate looping (LTV ≤ 0.45) gives you ~1.8x exposure with a 37% drop buffer — reasonable if you believe the thesis and accept the smart contract risk. Higher LTV is asking to get liquidated on a bad week.
