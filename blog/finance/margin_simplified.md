@def title = "Margin Trading: The Essential Guide"
@def published = "5 February 2026"
@def tags = ["finance"]

# Margin Trading: The Essential Guide

## The Core Concept

**Margin = borrowing money from your broker, using your existing securities as collateral.**

Your **marginable securities** (stocks, ETFs on major exchanges) act as collateral. You can borrow against them to buy more investments—whether marginable or non-marginable.

---

## The Two Critical Numbers

### 1. Your Equity

$$E = V_{\text{total}} - L$$

- $V_{\text{total}}$ = Total value of your **marginable securities only**
- $L$ = Your margin loan balance
- $E$ = Your equity (what you actually own)

### 2. Maintenance Requirement (30% at Fidelity)

$$E_{\text{required}} = V_{\text{total}} \times 0.30$$

**Margin call triggered when:** $E < E_{\text{required}}$

> **The Most Important Thing to Understand:**
> 
> Your margin call risk depends **entirely on your marginable securities dropping**—NOT on what happens to the asset you purchased with the loan.
> 
> - If your marginable securities drop → margin call risk increases
> - If the non-marginable asset you bought drops → nothing happens to your margin status (you just lost money on that investment)
> - If the non-marginable asset you bought goes up → it still doesn't help your margin status at all
> 
> **Your collateral (marginable securities) is the only thing that matters for margin calculations.**

---

## Understanding Fidelity's Buying Power Labels

Fidelity shows three different "buying power" numbers. Here's what they actually mean:

| Label | What It Means | Will You Pay Interest? |
|-------|---------------|----------------------|
| **Available Without Margin Impact** | Your **settled cash**. This is money you can spend without borrowing anything. | ❌ No |
| **Non-Margin Buying Power** | Cash + borrowing capacity against your existing marginable securities. Despite the name, using this **beyond your cash WILL create a margin loan**. | ✅ Yes (on amount above your cash) |
| **Margin Buying Power** | Your maximum purchasing power using full 2:1 leverage (Reg T allows borrowing up to 50% of purchase). | ✅ Yes |

> **Don't confuse these:**
> - **$V_{\text{marginable}}$** (in formulas) = The **current market value** of your marginable securities
> - **Margin Buying Power** = How much you can **purchase** (roughly 2× your marginable securities value if no existing loan)
> 
> To find your $V_{\text{marginable}}$, look at the market value of your stocks/ETFs—not the buying power numbers.

> **Why is my Margin Buying Power less than 2× my securities?**
> 
> Several factors reduce your buying power below the theoretical 2× leverage:
> - **Existing margin loan** — Reduces available capacity
> - **Higher-requirement securities** — Some stocks require 40%, 50%, or even 100% margin (volatile stocks, concentrated positions, leveraged ETFs)
> - **House requirements** — Fidelity may impose stricter limits than Reg T minimums
> - **Unsettled cash/trades** — Recent activity may not be reflected yet
> 
> Check your positions page for individual margin requirements on each holding.

### The Confusing Part

**"Non-Margin Buying Power" is a misleading name.** It doesn't mean "no margin loan"—it means you can buy *non-marginable securities* up to this amount. You're still borrowing against your marginable securities!

### The Simple Rule

$$\text{If Purchase} > \text{Available Without Margin Impact} \implies \text{You're borrowing and paying interest}$$

> **Example:** If your "Available Without Margin Impact" is \$40 and you buy \$100 of something:
> - \$40 comes from your cash (no interest)
> - \$60 is borrowed on margin (interest charged at ~10.5%)
> 
> This is true even if your "Non-Margin Buying Power" shows \$10,000!

---

## Tax Treatment of Margin Interest

**Yes, margin interest may be tax-deductible—but with limits.**

| Situation | Deductible? |
|-----------|-------------|
| Interest on margin used to buy **taxable investments** | ✅ Yes, up to your net investment income |
| Interest exceeds your investment income | ⏳ Carry forward to future years |
| Margin used to buy **tax-exempt securities** (municipal bonds) | ❌ No |

**Key rules:**

1. **Investment Interest Deduction** — Margin interest counts as "investment interest expense" under IRS rules
2. **Limited to investment income** — You can only deduct up to your net investment income (dividends, interest, short-term capital gains)
3. **Must itemize** — You need to itemize deductions (Schedule A) to claim this; doesn't work with standard deduction
4. **Form 4952** — Use this form to calculate your deductible investment interest

> **Example:** You paid \$1,000 in margin interest and earned \$800 in dividends. You can deduct \$800 this year and carry forward the remaining \$200 to next year.

**Consult a tax professional** for your specific situation.

---

## Buying Non-Marginable Securities on Margin

**Key insight:** When you buy a **non-marginable security** (penny stocks, some ETFs, crypto, IPOs), it does NOT count toward $V_{\text{total}}$ for margin calculations, but you still owe the loan!

### Example: You Own \$15,000 in Marginable Stock A

**Starting position:**
- Stock A (marginable): \$15,000
- Margin loan: \$0
- Equity: \$15,000

**You buy \$5,000 of Non-Marginable Asset X using margin:**

| Item | Value | Counts as Collateral? |
|------|-------|----------------------|
| Stock A (marginable) | \$15,000 | ✅ Yes |
| Asset X (non-marginable) | \$5,000 | ❌ No |
| **Total Holdings** | **\$20,000** | |
| **Marginable Securities** ($V_{\text{total}}$) | **\$15,000** | ← Only this matters for margin! |
| Margin Loan ($L$) | \$5,000 | |
| **Your Equity** ($E$) | **\$10,000** | $V_{\text{total}} - L = \$15,000 - \$5,000$ |

**Check margin requirement:**

$$E_{\text{required}} = \$15,000 \times 0.30 = \$4,500$$

$$E = \$10,000 > \$4,500$$ ✅ Safe

---

## The Danger: Your Marginable Securities Drop

**What happens if Stock A drops 30%?**

| Item | Value | Notes |
|------|-------|-------|
| Stock A (dropped) | \$10,500 | \$15,000 × 0.70 |
| Asset X (unchanged) | \$5,000 | Doesn't help your margin! |
| **Marginable Securities** ($V_{\text{total}}$) | **\$10,500** | |
| Margin Loan ($L$) | \$5,000 | unchanged |
| **Your Equity** ($E$) | **\$5,500** | \$10,500 - \$5,000 |

**Check margin requirement:**

$$E_{\text{required}} = \$10,500 \times 0.30 = \$3,150$$

$$E = \$5,500 > \$3,150$$ ✅ Still safe

**What if Stock A drops 50%?**

| Item | Value | Notes |
|------|-------|-------|
| Stock A (dropped) | \$7,500 | \$15,000 × 0.50 |
| Asset X (unchanged) | \$5,000 | Still doesn't help! |
| **Marginable Securities** ($V_{\text{total}}$) | **\$7,500** | |
| Margin Loan ($L$) | \$5,000 | unchanged |
| **Your Equity** ($E$) | **\$2,500** | \$7,500 - \$5,000 |

**Check margin requirement:**

$$E_{\text{required}} = \$7,500 \times 0.30 = \$2,250$$

$$E = \$2,500 > \$2,250$$ ✅ Barely safe!

**What if Stock A drops 60%?**

| Item | Value | Notes |
|------|-------|-------|
| Stock A (dropped) | \$6,000 | \$15,000 × 0.40 |
| Asset X (unchanged) | \$5,000 | |
| **Marginable Securities** ($V_{\text{total}}$) | **\$6,000** | |
| Margin Loan ($L$) | \$5,000 | |
| **Your Equity** ($E$) | **\$1,000** | \$6,000 - \$5,000 |

**Check margin requirement:**

$$E_{\text{required}} = \$6,000 \times 0.30 = \$1,800$$

$$E = \$1,000 < \$1,800$$ ❌ **MARGIN CALL!**

---

## The Formula: How Much Can You Safely Borrow?

When buying **non-marginable securities**, your margin loan is backed ONLY by your existing marginable securities. 

**To survive a drop of $x$% in your marginable securities:**

$$L_{\text{max}} = V_{\text{marginable}} \times (1 - x) \times 0.70$$

Where:
- $V_{\text{marginable}}$ = Current value of your marginable securities
- $x$ = Maximum expected drop (as decimal)
- $0.70 = 1 - 0.30$ (inverse of maintenance requirement)

### Quick Reference Table

If your marginable securities are worth \$15,000:

| Max Expected Drop | Max Safe Loan | Calculation |
|------------------|---------------|-------------|
| 20% | \$8,400 | \$15,000 × 0.80 × 0.70 |
| 30% | \$7,350 | \$15,000 × 0.70 × 0.70 |
| 40% | \$6,300 | \$15,000 × 0.60 × 0.70 |
| 50% | \$5,250 | \$15,000 × 0.50 × 0.70 |
| 60% | \$4,200 | \$15,000 × 0.40 × 0.70 |

### Verification: \$5,000 Loan Protecting Against 50% Drop

Using the formula:

$$L_{\text{max}} = \$15,000 \times (1 - 0.50) \times 0.70 = \$15,000 \times 0.50 \times 0.70 = \$5,250$$

Your \$5,000 loan is just under \$5,250, so you're protected against a 50% drop in Stock A. ✅

---

## Margin Call: What Happens & How to Resolve

**When triggered:** Your equity falls below 30% of your marginable securities.

**Your options:**

1. **Deposit cash** → Directly reduces your loan
2. **Deposit marginable securities** → Increases $V_{\text{total}}$
3. **Sell securities** → Proceeds pay down loan

**If you don't act:** Fidelity liquidates your positions to bring you back into compliance.

---

## Paying Back the Margin Loan

There's no monthly payment. Your loan decreases automatically when you:

- Deposit cash
- Sell any securities (proceeds go to loan first)
- Receive dividends

**Interest accrues daily** at ~10.5% annually for balances under \$25,000.

---

## Key Takeaways

1. **Only marginable securities count as collateral** for calculating your equity and margin requirements

2. **Non-marginable purchases increase your loan without increasing your collateral** — this is riskier than buying marginable securities on margin

3. **Your margin call risk depends entirely on your marginable securities dropping**, not on what you bought with the loan

4. **The formula:** $L_{\text{max}} = V_{\text{marginable}} \times (1 - x) \times 0.70$ tells you how much you can borrow to survive a drop of $x$%

5. **Add a safety buffer** — use 80-90% of the calculated max loan to give yourself room for error

---

## Quick Decision Framework

Before using margin to buy a non-marginable security, ask:

1. **What's my marginable securities total?** → $V_{\text{marginable}}$
2. **What's the worst-case drop I should protect against?** → $x$
3. **Calculate max safe loan:** $V_{\text{marginable}} \times (1 - x) \times 0.70$
4. **Is my purchase under that amount?**
   - ✅ Yes → Proceed with caution
   - ❌ No → Reduce purchase or add more cash/marginable securities first
