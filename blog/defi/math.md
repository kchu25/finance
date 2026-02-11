@def title = "Crypto Lending & Leverage Math Cheat Sheet"
@def published = "10 February 2026"
@def tags = ["crypto", "defi"]

# Crypto Lending & Leverage Math Cheat Sheet

\newcommand{\CR}{\text{CR}}
\newcommand{\HF}{\text{HF}}
\newcommand{\LTV}{\text{LTV}}
\newcommand{\LT}{\text{LT}}
\newcommand{\APY}{\text{APY}}
\newcommand{\EV}{\text{EV}}

## Core Concept: Collateralization Ratio

The fundamental constraint in protocols like Aave:

$$
\CR = \frac{V_c}{V_d}
$$

where:
- $V_c$ = collateral value
- $V_d$ = debt value
- $\CR$ = collateralization ratio

**Your liquidation trigger:** If this ratio falls below the protocol's minimum (often 110-150%), you get liquidated.

**Example:** You deposit \$10,000 ETH, borrow \$6,000 USDC. Your ratio is $\frac{10000}{6000} = 1.67$ or 167%. If ETH drops and your collateral is worth \$8,000, you're at 133% - still safe if minimum is 125%.

---

## Health Factor (Aave-specific)

Aave uses a "health factor" which is essentially normalized collateralization:

$$
\HF = \frac{V_c \times \LT}{V_d}
$$

where $\LT$ = liquidation threshold (typically 0.75-0.85)

- **HF > 1:** You're safe
- **HF < 1:** Liquidation zone  
- **HF = 1.5+:** Comfortable buffer

The liquidation threshold is typically 75-85% (meaning you can borrow up to that % of collateral value).

---

## Loan-to-Value Ratio (LTV)

LTV is the **inverse perspective** of collateralization ratio — it measures debt as a fraction of collateral:

$$
\LTV = \frac{V_d}{V_c} = \frac{1}{\CR}
$$

**Interpretation:**
- $\LTV = 0.50$ (50%) means you borrowed half the value of your collateral
- $\LTV = 0.75$ (75%) means you borrowed 3/4 of your collateral value
- $\LTV = 0$ means no debt (you just deposited, didn't borrow)
- $\LTV = 1.0$ (100%) would mean debt equals collateral — this is the liquidation point!

**Example:** Deposit \$10,000 ETH, borrow \$6,000 USDC:
- Your $\CR = \frac{10000}{6000} = 1.67$ (167%)
- Your $\LTV = \frac{6000}{10000} = 0.60$ (60%)

**Key relationship:**

$$
\text{If } \CR = 1.67 \implies \LTV = \frac{1}{1.67} = 0.60
$$

**Maximum LTV:** The liquidation threshold $\LT$ sets the maximum LTV:

$$
\LTV_{\max} = \LT
$$

If $\LT = 0.80$ (80%), you can borrow up to 80% of collateral value before liquidation.

**Safe LTV:** Most experienced users stay much lower:

$$
\LTV_{\text{safe}} = 0.50 \text{ to } 0.60
$$

This gives you a cushion for price volatility.

---

## Maximum Borrowing Power

If liquidation threshold is 80%:

$$
B_{\max} = V_c \times \LT
$$

But **never max it out**. Leave a safety margin. A good rule:

$$
B_{\text{safe}} = V_c \times (0.50 \text{ to } 0.60)
$$

---

## Effective Interest Rate with Leverage

You're not just paying borrow APY - you need to account for what you're earning:

$$
\APY_{\text{net}} = r_{\text{yield}} - r_{\text{borrow}}
$$

where:
- $r_{\text{yield}}$ = yield on invested borrowed funds
- $r_{\text{borrow}}$ = borrowing rate

**Reality check:** If you borrow USDC at 8% to buy more ETH staking at 4%, you're losing 4% per year *plus* taking liquidation risk.

**When it makes sense:** Borrow at 5% to earn 12% yield farming = 7% net gain (ignoring gas, risks, etc.)

---

## Leverage Multiplier

If you loop (borrow → deposit → borrow again):

$$
L = \frac{1}{1 - \LTV}
$$

where $\LTV$ = loan-to-value ratio (how much you borrow relative to collateral)

**Example:** With 75% LTV:
$$
L = \frac{1}{1 - 0.75} = 4x
$$

Starting with \$10k, you could control \$40k worth of assets. *Very risky.*

---

## Unified Framework: How Everything Relates

All the metrics ($\CR$, $\HF$, $\LTV$, liquidation) are different views of the same underlying relationship. Here's the unifying math:

### The Core Variables

You have only **two fundamental quantities**:
- $V_c$ = collateral value
- $V_d$ = debt value

Everything else is derived from these two.

### The Four Key Metrics

| Metric | Formula | Meaning | Safe Range |
|--------|---------|---------|------------|
| **Collateralization Ratio** | $\CR = \frac{V_c}{V_d}$ | How much collateral per dollar of debt | > 1.5 |
| **Loan-to-Value** | $\LTV = \frac{V_d}{V_c} = \frac{1}{\CR}$ | How much debt per dollar of collateral | < 0.60 |
| **Health Factor** | $\HF = \frac{V_c \times \LT}{V_d} = \CR \times \LT$ | Distance to liquidation | > 1.5 |
| **Liquidation Threshold** | $\LT$ (constant) | Protocol-defined max LTV | 0.75-0.85 |

### The Relationships

**Converting between CR and LTV:**

$$
\CR = \frac{1}{\LTV} \quad \text{and} \quad \LTV = \frac{1}{\CR}
$$

**Health Factor in terms of LTV:**

$$
\HF = \frac{\LT}{\LTV}
$$

**Liquidation condition (all equivalent):**

$$
\begin{aligned}
\CR &< \frac{1}{\LT} \\
\LTV &> \LT \\
\HF &< 1
\end{aligned}
$$

### Example: One Position, Four Views

You deposit \$10,000 ETH, borrow \$6,000 USDC. Protocol has $\LT = 0.80$.

| Metric | Calculation | Value | Safe? |
|--------|-------------|-------|-------|
| $\CR$ | $\frac{10000}{6000}$ | 1.67 | ✅ (> 1.25) |
| $\LTV$ | $\frac{6000}{10000}$ | 0.60 | ✅ (< 0.80) |
| $\HF$ | $\frac{10000 \times 0.80}{6000}$ | 1.33 | ⚠️ (barely > 1) |
| Liquidation? | $\LTV < \LT$ ? | $0.60 < 0.80$ | ✅ Safe |

**If ETH drops 20% to \$8,000:**

| Metric | New Value | Safe? |
|--------|-----------|-------|
| $\CR$ | $\frac{8000}{6000} = 1.33$ | ⚠️ Danger |
| $\LTV$ | $\frac{6000}{8000} = 0.75$ | ⚠️ Close to limit |
| $\HF$ | $\frac{8000 \times 0.80}{6000} = 1.07$ | ⚠️ Very close to 1 |
| Liquidation? | $0.75 < 0.80$ | ✅ Still safe (barely) |

**If ETH drops 30% to \$7,000:**

| Metric | New Value | Safe? |
|--------|-----------|-------|
| $\CR$ | $\frac{7000}{6000} = 1.17$ | ❌ Below threshold |
| $\LTV$ | $\frac{6000}{7000} = 0.857$ | ❌ Exceeds $\LT$ |
| $\HF$ | $\frac{7000 \times 0.80}{6000} = 0.93$ | ❌ Below 1 |
| Liquidation? | $0.857 > 0.80$ | ❌ **LIQUIDATED** |

### The General Rule

For any position, you can convert between all metrics using these relationships:

$$
\boxed{
\begin{aligned}
\LTV &= \frac{1}{\CR} \\
\HF &= \CR \times \LT = \frac{\LT}{\LTV} \\
\text{Safe} &\iff \LTV < \LT \iff \CR > \frac{1}{\LT} \iff \HF > 1
\end{aligned}
}
$$

**Which metric to use?**
- **LTV** is most intuitive for thinking about borrowing ("I borrowed 60% of my collateral")
- **CR** is traditional finance language ("167% collateralized")
- **HF** is Aave-specific but useful (tells you distance to liquidation threshold)

They're all equivalent — use whichever makes most sense to you.

### How Much Can Collateral Drop?

Given your current LTV and liquidation threshold $\LT$, the maximum tolerable price drop is:

$$
x_{\max} = 1 - \frac{\LTV}{\LT} = 1 - \frac{1}{\HF}
$$

**Examples:**

| Current LTV | $\LT$ | HF | Max Drop | Calculation |
|-------------|-------|----|---------:|-------------|
| 0.60 | 0.80 | 1.33 | **25%** | $1 - \frac{0.60}{0.80}$ |
| 0.50 | 0.80 | 1.60 | **37.5%** | $1 - \frac{0.50}{0.80}$ |
| 0.40 | 0.80 | 2.00 | **50%** | $1 - \frac{0.40}{0.80}$ |
| 0.75 | 0.80 | 1.07 | **6.25%** | $1 - \frac{0.75}{0.80}$ |

> **Key insight**: A health factor of 1.33 does NOT mean you can drop 33%. It means you're at 60% LTV with an 80% threshold, so you can drop **25%** before liquidation.
>
> The formula: **Max drop = $1 - \frac{1}{\text{HF}}$**

---

## Liquidation Price

The price at which your collateral falls below the minimum ratio:

$$
P_{\text{liq}} = P_{\text{entry}} \times \frac{V_d}{Q_c \times \LT}
$$

where:
- $P_{\text{entry}}$ = entry price per unit of collateral
- $Q_c$ = quantity of collateral  
- $V_d$ = total debt value

**Example:** You deposit 10 ETH at \$2,000 each (\$20k collateral), borrow \$12k USDC. With 75% liquidation threshold:

$$
P_{\text{liq}} = 2000 \times \frac{12000}{10 \times 2000 \times 0.75} = 2000 \times 0.8 = \$1,600
$$

If ETH drops to \$1,600, you're toast.

---

## Should You Pay Off High-Interest Debt?

The decision framework:

$$
\text{Pay off debt if: } r_{\text{debt}} > \mathbb{E}[r_{\text{alt}}]
$$

where:
- $r_{\text{debt}}$ = debt interest rate (guaranteed savings)
- $\mathbb{E}[r_{\text{alt}}]$ = expected return on alternative investment

But adjust for **risk and liquidity**:

$$
r_{\text{debt}} \text{ vs } (\mathbb{E}[r_{\text{alt}}] - \pi)
$$

where $\pi$ = risk premium

**Example:** 
- Credit card debt: 22% APR (guaranteed savings)
- Staking ETH: 4% yield (uncertain, lockup, smart contract risk)

**Math says:** Pay off the 22% debt. You'd need to earn 22%+ consistently to break even, and crypto yields aren't guaranteed.

**Nuance:** If debt is 3% student loans vs 8% DeFi yields, the math is closer. Factor in:
- Tax implications
- Liquidation risk
- Your risk tolerance
- Opportunity cost of locked capital

---

## Staking vs Lending Returns

**Simple staking yield:**
$$
R_{\text{annual}} = V_{\text{stake}} \times \APY_{\text{stake}}
$$

**Lending with collateral (if you don't borrow):**
$$
R_{\text{annual}} = V_{\text{deposit}} \times \APY_{\text{supply}}
$$

**The catch:** Supply APY on Aave is often 0.5-3%, while staking is 3-8%. But lending gives you *borrowing power*.

---

## The Leverage Decision Matrix

You use leverage when:

$$
(\mathbb{E}[\text{ROI}] - r_{\text{borrow}}) \times P(\text{success}) > P(\text{liq}) \times L_{\text{liq}}
$$

where:
- $P(\text{success})$ = probability of success
- $P(\text{liq})$ = probability of liquidation
- $L_{\text{liq}}$ = liquidation loss

This is more art than science, but the math scaffolding:

**Expected Value:**
$$
\EV = P(\text{win}) \times G - P(\text{liq}) \times L - r_{\text{borrow}}
$$

where $G$ = gain, $L$ = loss

**Example:**
- 70% chance ETH goes up 20%: $0.70 \times 0.20 = 0.14$
- 30% chance you get liquidated, lose 15%: $0.30 \times 0.15 = 0.045$
- Borrow cost: 5% = $0.05$

$$
\EV = 0.14 - 0.045 - 0.05 = 0.045 = 4.5\%
$$

Positive EV, but is 4.5% worth the stress and smart contract risk?

---

## Quick Mental Models

**The Conservative Approach:**
- Max 50% LTV
- Only borrow if you're earning 2x+ the borrow rate
- Keep health factor > 2.0

**The "I'm Paying Off Debt" Rule:**
- If debt interest > 10%: Pay it off first, no question
- If debt interest 5-10%: Depends on risk tolerance
- If debt interest < 5%: Consider leveraging *only* if you have stable income and emergency fund

**The Liquidation Safety Margin:**

$$
\text{Safe Buffer} = \frac{P_{\text{liq}}}{P_{\text{current}}} < 0.70
$$

If liquidation price is 70%+ of current price, you're too exposed.

---

## Symbol Reference

| Symbol | Meaning |
|--------|---------|
| $\CR$ | Collateralization Ratio |
| $\HF$ | Health Factor |
| $\LTV$ | Loan-to-Value Ratio |
| $\LT$ | Liquidation Threshold |
| $V_c$ | Collateral Value |
| $V_d$ | Debt Value |
| $Q_c$ | Quantity of Collateral |
| $P_{\text{liq}}$ | Liquidation Price |
| $P_{\text{entry}}$ | Entry Price |
| $r_{\text{borrow}}$ | Borrow Rate |
| $r_{\text{yield}}$ | Yield Rate |
| $r_{\text{debt}}$ | Debt Interest Rate |
| $\mathbb{E}[r]$ | Expected Return |
| $\pi$ | Risk Premium |
| $L$ | Leverage Multiplier |
| $\EV$ | Expected Value |
| $P(\cdot)$ | Probability |

---

## Key Takeaway

The math is straightforward, but **crypto volatility** makes it dangerous. A 20% drop in ETH can wipe out months of yields. Always stress test:

> "If my collateral drops 30% overnight, am I liquidated?"

If yes, you're over-leveraged. If no, check:

> "If I'm earning 8% but borrowing at 6%, is 2% net worth the liquidation risk?"

Usually? No. The exception is if you have other income sources and treat this as a calculated portfolio allocation, not your entire net worth.