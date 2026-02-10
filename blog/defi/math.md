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