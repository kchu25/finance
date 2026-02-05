@def title = "Understanding Margin at Fidelity"
@def published = "5 February 2026"
@def tags = ["finance"]

# Understanding Margin at Fidelity

## What's Margin, Really?

Think of margin as a loan from Fidelity, using your investments as collateral. You can borrow money to buy more stocks or access cash—but you'll pay interest, and there are risks.

---

## Your Account Balances Explained

Let's decode those numbers you're seeing:

### **Available Without Margin Impact: \$40**

This is **settled cash** you can use without triggering any margin loan. If you spend only this, you pay zero interest.

### **Non-Margin Buying Power: \$10,000**

This is **NOT** just your own money—this is a bit misleading! It actually includes:
- Your \$40 in settled cash
- **Margin surplus from securities you already own**

> **Margin Surplus**: The excess equity you have in your marginable securities beyond what's required for maintenance. If you own \$20,000 in stocks and Fidelity requires 30% maintenance (\$6,000), your margin surplus is \$14,000. This surplus can be borrowed against.

**Important**: Using your non-margin buying power beyond the \$40 **will likely create a margin loan** and trigger interest charges! The name is confusing—it doesn't mean "no margin loan."



### **Margin Buying Power: \$20,000**

This is your **maximum** purchasing power if you're willing to borrow from Fidelity. Here's the key: **you can buy MORE than the value of what you currently own!**

$$\text{Margin Buying Power} = \text{Your Equity} \times 2$$

With \$10,000 in equity, Regulation T allows you to buy up to \$20,000 worth of securities through **2:1 leverage**.

**What this means:**
- You put up: \$10,000
- Fidelity lends: \$10,000
- Total buying power: \$20,000

**After buying \$20,000 in stock:**
- Securities value: \$20,000
- Margin loan: \$10,000
- Your equity: \$10,000 (exactly 50% — the initial requirement)

> **Warning**: This leverage amplifies BOTH gains and losses by 2x!
> 
> **Stock up 10%**: Your \$20,000 becomes \$22,000 → Your equity becomes \$12,000 → **You gained 20%** ✅
> 
> **Stock down 10%**: Your \$20,000 becomes \$18,000 → Your equity becomes \$8,000 → **You lost 20%** ❌

**Margin Call Risk:**

If your \$20,000 investment drops to \$14,000:
- Your equity: \$14,000 - \$10,000 = \$4,000
- Required equity (30%): \$14,000 × 0.30 = \$4,200
- **MARGIN CALL** — you're \$200 short!

---

## What Happens If You Buy More Than \$40?

Here's the breakdown:

### **Scenario 1: You buy \$100 worth of stock**

- **You'll use**: Your \$40 of settled cash + **\$60 borrowed against your existing securities**
- **Margin loan triggered?** **Yes!** 
- **Will you pay interest?** **Yes**—on the \$60 (currently ~10.575% annual rate at Fidelity)

The key is that "non-margin buying power" is confusing—it doesn't mean no borrowing. It means you're borrowing against your marginable securities to buy something (even non-marginable securities).

### **Scenario 2: You buy \$12,000 worth of stock**

- **You'll use**: Your \$40 cash + **\$11,960 borrowed on margin**
- **Margin loan triggered?** **Yes**
- **Interest charged?** **Yes**—on the **\$11,960** borrowed (currently ~10.575% annual rate at Fidelity)

**Important clarification**: The \$10,000 "non-margin buying power" doesn't mean you have \$10,000 to spend interest-free! It means you have enough collateral (existing securities) to support borrowing up to that amount. You're still borrowing almost the full purchase price!

### **The Real Rule of Thumb**

$$\text{If Purchase Amount} > \text{Available Without Margin Impact} \implies \text{You're likely borrowing on margin}$$

To truly avoid margin interest, stay within your **\$40 "available without margin impact"**—not your \$10,000 non-margin buying power!

---

## How Margin Requirements Work

### **Initial Requirement (Reg T): 50%**

When you buy on margin, you must put up at least 50% of the purchase price:

$$\text{Your Cash Required} = 0.50 \times \text{Purchase Price}$$

**Example**: Want to buy \$20,000 of stock?
- You need: \$10,000 of your own money
- Fidelity lends: \$10,000

### **Maintenance Requirement: 30% (Fidelity) or 25% (FINRA minimum)**

You must maintain at least 30% equity in your account:

$$\text{Account Equity} \geq 0.30 \times \text{Total Market Value}$$

**What's equity?** 

$$\text{Equity} = \text{Market Value of Securities} - \text{Margin Loan}$$

---

## Margin Calls: What Triggers Them?

A **margin call** happens when your **total account equity** drops below the maintenance requirement. 

### **Key Variables & Formulas**

Let's use symbols to make this clearer:

**Account Components:**
- $V_{\text{total}}$ = Total market value of your **marginable** securities
- $L$ = Your margin loan balance (what you owe Fidelity)  
- $E$ = Your equity (what you actually own)

> **Important**: $V_{\text{total}}$ only includes **marginable securities** — not all securities can be used as collateral! 
> 
> **Marginable securities** typically include:
> - Most stocks trading above \$3 on major exchanges (NYSE, NASDAQ)
> - Many ETFs
> - Some corporate bonds and municipal bonds
> 
> **Non-marginable securities** (cannot be used as collateral):
> - Penny stocks (typically under \$3)
> - OTC Bulletin Board stocks
> - Most IPO stocks (for first 30 days)
> - Options (these have their own margin rules)
> - Many leveraged and inverse ETFs
> - Cryptocurrency
> 
> If you own non-marginable securities in your margin account, they don't count toward $V_{\text{total}}$ for margin calculations, though they still belong to you!

**The Fundamental Equation:**

$$E = V_{\text{total}} - L$$

Your equity is simply the total value of your marginable securities minus what you owe.

**Maintenance Requirement:**

$$E_{\text{required}} = V_{\text{total}} \times m$$

where $m$ = maintenance margin rate (typically 0.30 or 30% at Fidelity)

**Margin Call Condition:**

A margin call is triggered when:

$$E < E_{\text{required}}$$

Or equivalently:

$$V_{\text{total}} - L < V_{\text{total}} \times m$$

**Critical Threshold:**

Solving for when you're safe:

$$V_{\text{total}} - L \geq V_{\text{total}} \times m$$

$$V_{\text{total}}(1 - m) \geq L$$

$$V_{\text{total}} \geq \frac{L}{1 - m}$$

**For Fidelity (m = 0.30):**

$$V_{\text{total}} \geq \frac{L}{0.70} \approx 1.43 \times L$$

**This means your securities must be worth at least 1.43 times your loan to avoid a margin call!**

---

### **Complete Numerical Example**

**Starting Position:**
- You own Stock A: \$15,000 (fully paid, no loan)
- Cash: \$40
- Total equity: \$15,040
- Margin loan: \$0

**You decide to buy Stock B for \$20,000:**

Since you only have \$40 cash, you borrow:

$$\text{Margin Loan} = \$20,000 - \$40 = \$19,960$$

**Your Account Right After Purchase:**

| Item | Value | Formula |
|------|-------|--------|
| Stock A (existing) | \$15,000 | |
| Stock B (new) | \$20,000 | |
| **Total Securities** ($V_{\text{total}}$) | **\$35,000** | $\$15,000 + \$20,000$ |
| Margin Loan ($L$) | \$19,960 | $\$20,000 - \$40$ |
| **Your Equity** ($E$) | **\$15,040** | $V_{\text{total}} - L = \$35,000 - \$19,960$ |

**Check Margin Requirement:**

$$E_{\text{required}} = V_{\text{total}} \times 0.30 = \$35,000 \times 0.30 = \$10,500$$

$$E = \$15,040 > \$10,500 = E_{\text{required}}$$

You're safe! ✅

---

**Now Stock B Drops 30% (from \$20,000 to \$14,000):**

| Item | Value | Formula |
|------|-------|--------|
| Stock A (unchanged) | \$15,000 | |
| Stock B (dropped) | \$14,000 | $\$20,000 \times 0.70$ |
| **Total Securities** ($V_{\text{total}}$) | **\$29,000** | $\$15,000 + \$14,000$ |
| Margin Loan ($L$) | \$19,960 | unchanged |
| **Your Equity** ($E$) | **\$9,040** | $V_{\text{total}} - L = \$29,000 - \$19,960$ |

**Check Margin Requirement:**

$$E_{\text{required}} = V_{\text{total}} \times 0.30 = \$29,000 \times 0.30 = \$8,700$$

$$E = \$9,040 > \$8,700 = E_{\text{required}}$$

Still okay! ✅

---

**But What if Stock A ALSO Drops 20% (from \$15,000 to \$12,000)?**

| Item | Value | Formula |
|------|-------|--------|
| Stock A (dropped) | \$12,000 | $\$15,000 \times 0.80$ |
| Stock B (dropped) | \$14,000 | $\$20,000 \times 0.70$ |
| **Total Securities** ($V_{\text{total}}$) | **\$26,000** | $\$12,000 + \$14,000$ |
| Margin Loan ($L$) | \$19,960 | unchanged |
| **Your Equity** ($E$) | **\$6,040** | $V_{\text{total}} - L = \$26,000 - \$19,960$ |

**Check Margin Requirement:**

$$E_{\text{required}} = V_{\text{total}} \times 0.30 = \$26,000 \times 0.30 = \$7,800$$

$$E = \$6,040 < \$7,800 = E_{\text{required}}$$

**MARGIN CALL!** ⚠️

$$\text{Shortfall} = E_{\text{required}} - E = \$7,800 - \$6,040 = \$1,760$$

### **Summary in Symbolic Form**

Using our variables from earlier:

**Initial State:**  
$V_{\text{total}} = \$35,000$, $L = \$19,960$, $E = \$15,040$

**After Both Stocks Drop:**  
$V_{\text{total}} = \$26,000$, $L = \$19,960$ (unchanged), $E = \$6,040$

**Check against requirement:**

$$E_{\text{required}} = V_{\text{total}} \times 0.30 = \$26,000 \times 0.30 = \$7,800$$

$$E = \$6,040 < \$7,800 = E_{\text{required}}$$

**Margin call triggered!** ⚠️

**Shortfall:**

$$\Delta E = E_{\text{required}} - E = \$7,800 - \$6,040 = \$1,760$$

### **Key Insight**

Notice how the margin loan **stays constant** at \$19,960 (i.e., $L$ doesn't change), but your equity shrinks as your securities lose value. The maintenance requirement is based on your **total portfolio value** ($V_{\text{total}}$), not just the stock you bought on margin!

---

## What Actually Happens During a Margin Call?

When you receive a margin call, here's the timeline and your options:

### **Step 1: Notification**

Fidelity will contact you (usually by email and in your account messages) telling you:
- How much your equity is short
- The deadline to meet the call (typically 5 business days, but can be immediate for large deficiencies)
- Your options to resolve it

### **Step 2: Your Options**

You have several ways to meet the margin call:

**Option A: Deposit Cash**

Simply transfer \$1,760 (or more) into your account.

$$E_{\text{new}} = E_{\text{old}} + \text{Cash Deposited}$$

If you deposit \$1,760:

$$E_{\text{new}} = \$6,040 + \$1,760 = \$7,800 \geq E_{\text{required}}$$ ✅

**Option B: Deposit Marginable Securities**

Transfer stocks/ETFs from another account. If you deposit securities worth $S$:

$$V_{\text{total, new}} = V_{\text{total, old}} + S$$

$$E_{\text{new}} = V_{\text{total, new}} - L$$

To meet the call, you need:

$$E_{\text{new}} \geq V_{\text{total, new}} \times 0.30$$

**Option C: Sell Securities**

This is tricky! When you sell, you:
1. Reduce $V_{\text{total}}$ (less securities)
2. Reduce $L$ (pay down the loan)
3. Change $E_{\text{required}}$ (because it depends on $V_{\text{total}}$)

Let's say you sell $X$ worth of securities:

$$V_{\text{total, new}} = V_{\text{total, old}} - X = \$26,000 - X$$

$$L_{\text{new}} = L - X = \$19,960 - X$$

$$E_{\text{new}} = V_{\text{total, new}} - L_{\text{new}} = (\$26,000 - X) - (\$19,960 - X) = \$6,040$$

**Wait, your equity stays the same!** But the required equity changes:

$$E_{\text{required, new}} = V_{\text{total, new}} \times 0.30 = (\$26,000 - X) \times 0.30$$

To meet the call:

$$\$6,040 \geq (\$26,000 - X) \times 0.30$$

$$\$6,040 \geq \$7,800 - 0.30X$$

$$0.30X \geq \$1,760$$

$$X \geq \$5,867$$

**You need to sell at least \$5,867 worth of securities!**

### **Step 3: If You Don't Act**

If you don't meet the margin call by the deadline:

1. **Fidelity liquidates positions** — They will sell your securities (starting with the most liquid) to bring your account back into compliance
2. **You don't control what gets sold** — They might sell your favorite long-term holdings
3. **Forced selling at bad prices** — If the market is down, you're selling at the bottom
4. **You're still responsible** — If the sales don't cover your loan, you still owe the difference

### **Step 4: Account Restrictions**

After a margin call (even if met), Fidelity may:
- Increase your maintenance requirements
- Restrict your trading
- Close your margin privileges

---

## Getting Started with Margin

### **Requirements**

- Minimum **\$2,000** in account equity
- Complete a margin agreement (acknowledges risks)
- Find it under: **Accounts & Trade → Update Accounts/Features → Margin and Options**

---

## Interest: The Cost of Borrowing

### **Current Rates (as of Dec 2025)**

| Balance Borrowed | Annual Rate |
|-----------------|-------------|
| < \$25,000 | 10.575% |
| \$25,000 - \$49,999 | 10.325% |
| \$50,000 - \$99,999 | 10.075% |
| \$1,000,000+ | 7.50% |

### **How It's Calculated**

Interest accrues **daily** on your margin loan:

$$\text{Daily Interest} = \frac{\text{Margin Loan} \times \text{Annual Rate}}{360}$$

Charged monthly (21st to 20th cycle).

### **How to Pay Back Your Margin Loan**

> **Paying Down Your Margin Loan: The Basics**
> 
> Your margin loan gets paid back automatically in these situations:
> 
> **1. Deposit Cash**
> - Transfer money into your account
> - The cash immediately reduces your margin loan balance
> - Interest stops accruing on the amount you paid back
> 
> **2. Sell Securities**
> - When you sell stocks/ETFs in your margin account
> - Proceeds automatically go toward paying down your margin loan first
> - Any excess becomes available cash
> 
> **3. Dividends & Interest Payments**
> - Dividends from stocks you own
> - Interest from bonds or money market funds
> - These automatically reduce your margin loan balance
> 
> **Example:** If you have a \$10,000 margin loan and deposit \$3,000 cash, your loan instantly drops to \$7,000. If you sell \$5,000 worth of stock, your loan becomes \$2,000.
> 
> **Important:** There's no monthly "payment" like a credit card—you can pay it back anytime, in any amount. The loan stays open until you reduce it to zero or close your margin account.

---

## How Much Should You Margin? The Risk-Based Approach

### **The Core Question**

*"If I expect the stock could drop by X%, how much can I safely borrow without triggering a margin call?"*

This is the **right** way to think about margin—working backwards from your risk tolerance.

### **The Math**

Let's say you're buying \$10,000 worth of stock and want to protect against a drop of $x$ percent (expressed as a decimal, e.g., 0.30 for 30%).

**Variables:**
- $V_0$ = Initial value of securities **you're purchasing** = \$10,000
  - *Note: This is just the new purchase amount, NOT including any existing securities you already own*
  - *The formula calculates how much you can safely borrow for THIS purchase specifically*
- $x$ = Maximum expected drop (as decimal)
- $m$ = Maintenance margin rate = 0.30 (Fidelity's requirement)
- $L$ = Maximum safe margin loan **for this purchase** (what we're solving for)

> **Important Clarification:** This analysis assumes you're starting fresh or analyzing this purchase in isolation. If you already own marginable securities with existing margin loans, the total margin call risk depends on your **entire portfolio**. The formula below helps you determine safe borrowing for a specific new purchase, assuming that purchase could drop independently.

**After the drop:**

$$V_{\text{after}} = V_0(1 - x)$$

**Your equity after the drop:**

$$E_{\text{after}} = V_{\text{after}} - L = V_0(1 - x) - L$$

**To avoid a margin call, you need:**

$$E_{\text{after}} \geq V_{\text{after}} \times m$$

$$V_0(1 - x) - L \geq V_0(1 - x) \times m$$

$$V_0(1 - x) - L \geq V_0(1 - x) \times 0.30$$

$$V_0(1 - x)(1 - 0.30) \geq L$$

$$L \leq V_0(1 - x) \times 0.70$$

### **The Formula**

$$\boxed{L_{\text{max}} = V_0 \times (1 - x) \times 0.70}$$

Or as a percentage of your initial purchase:

$$\boxed{\text{Max Loan as % of Purchase} = (1 - x) \times 70\%}$$

### **Practical Examples**

Let's calculate the maximum safe loan for a \$10,000 stock purchase under different drop scenarios:

| Expected Max Drop | $(1 - x)$ | Max Safe Loan | % of Purchase | Your Cash Needed |
|------------------|-----------|---------------|---------------|------------------|
| 10% | 0.90 | \$6,300 | 63% | \$3,700 |
| 20% | 0.80 | \$5,600 | 56% | \$4,400 |
| 30% | 0.70 | \$4,900 | 49% | \$5,100 |
| 40% | 0.60 | \$4,200 | 42% | \$5,800 |
| 50% | 0.50 | \$3,500 | 35% | \$6,500 |

**Key Insight:** The more the stock could drop, the less you should borrow!

### **Detailed Walkthrough: 30% Drop Scenario**

You want to buy \$10,000 of stock and protect against a 30% drop.

**Maximum safe loan:**

$$L_{\text{max}} = \$10,000 \times (1 - 0.30) \times 0.70 = \$10,000 \times 0.70 \times 0.70 = \$4,900$$

**Your investment structure:**
- Total purchase: \$10,000
- Your cash: \$5,100
- Margin loan: \$4,900

**Verification—what happens if stock drops 30%?**

After drop:

$$V_{\text{after}} = \$10,000 \times 0.70 = \$7,000$$

Your equity:

$$E = V_{\text{after}} - L = \$7,000 - \$4,900 = \$2,100$$

Required equity:

$$E_{\text{required}} = V_{\text{after}} \times 0.30 = \$7,000 \times 0.30 = \$2,100$$

**Exactly at the margin requirement!** ✅ (Any more borrowing would trigger a call)

### **Converting to Leverage Ratios**

Some investors think in terms of leverage (how much you're buying vs. your own money):

$$\text{Leverage Ratio} = \frac{V_0}{\text{Your Cash}} = \frac{V_0}{V_0 - L}$$

Using our formula $L = V_0(1-x) \times 0.70$:

$$\text{Leverage Ratio} = \frac{1}{1 - (1-x) \times 0.70}$$

| Expected Max Drop | Max Safe Loan % | Leverage Ratio |
|------------------|----------------|----------------|
| 10% | 63% | 2.7× |
| 20% | 56% | 2.3× |
| 30% | 49% | 2.0× |
| 40% | 42% | 1.7× |
| 50% | 35% | 1.5× |

**Example:** With a 30% max drop tolerance, you can safely use 2.0× leverage (buy \$10,000 with \$5,000 of your own money).

### **What About Existing Securities?**

**The short answer:** If you already own marginable securities, they provide additional collateral that can help absorb losses, but they also introduce correlation risk.

**Scenario: You own \$15,000 in Stock A (fully paid, no loan) and want to buy \$10,000 of Stock B on margin**

**Option 1: Conservative (Treat as isolated)**
- Use the formula above: Max loan = \$10,000 × (1 - x) × 0.70
- For 30% drop protection on Stock B: Max loan = \$4,900
- **Assumes Stock B could drop 30% while Stock A stays stable**

**Option 2: Aggressive (Leverage existing securities)**
- Your existing \$15,000 provides margin capacity
- Available margin surplus from Stock A: \$15,000 - (\$15,000 × 0.30) = \$10,500
- You could theoretically borrow more against Stock A to fund Stock B

**The Hidden Risk: Correlation**
If Stock A and Stock B are correlated (e.g., both tech stocks), they could drop together:

**What happens if BOTH drop 20%?**

| Item | Value | Formula |
|------|-------|---------|
| Stock A (dropped) | \$12,000 | \$15,000 × 0.80 |
| Stock B (dropped) | \$8,000 | \$10,000 × 0.80 |
| **Total Securities** ($V_{\text{total}}$) | **\$20,000** | \$12,000 + \$8,000 |
| Margin Loan | \$4,900 | unchanged |
| **Your Equity** ($E$) | **\$15,100** | \$20,000 - \$4,900 |

**Check requirement:**

$$E_{\text{required}} = \$20,000 \times 0.30 = \$6,000$$

$$E = \$15,100 > \$6,000$$ ✅ Still safe!

**But what if BOTH drop 30%?**

| Item | Value | Formula |
|------|-------|---------|
| Stock A (dropped) | \$10,500 | \$15,000 × 0.70 |
| Stock B (dropped) | \$7,000 | \$10,000 × 0.70 |
| **Total Securities** ($V_{\text{total}}$) | **\$17,500** | \$10,500 + \$7,000 |
| Margin Loan | \$4,900 | unchanged |
| **Your Equity** ($E$) | **\$12,600** | \$17,500 - \$4,900 |

**Check requirement:**

$$E_{\text{required}} = \$17,500 \times 0.30 = \$5,250$$

$$E = \$12,600 > \$5,250$$ ✅ Still safe because Stock A provides cushion!

**Key Insight:** Your existing equity in Stock A acts as a buffer. Even though you calculated the max loan based on Stock B alone, your fully-paid Stock A provides extra protection.

**Practical Guidance:**

1. **If your holdings are diversified** (low correlation): Your existing securities provide a real safety buffer
2. **If your holdings are correlated** (same sector/style): Don't count on existing securities for protection—use the conservative formula
3. **Best practice**: Calculate the max loan for each new purchase assuming it could drop independently, but monitor your **total account** equity regularly

### **Reality Check & Safety Margins**

**This formula assumes you're exactly at the margin call threshold after the drop.** In practice, you want a buffer:

**Conservative approach:** Use 80-90% of the calculated max loan

$$L_{\text{conservative}} = V_0 \times (1 - x) \times 0.70 \times 0.85$$

For a 30% drop scenario with \$10,000 purchase:

$$L_{\text{conservative}} = \$10,000 \times 0.70 \times 0.70 \times 0.85 = \$4,165$$

This gives you a cushion above the maintenance requirement even if the stock drops the full 30%.

### **Quick Reference Calculator**

**Step 1:** Estimate maximum realistic drop percentage  
**Step 2:** Calculate safe loan percentage: $(1 - \text{drop%}) \times 70\%$  
**Step 3:** Apply safety factor if desired (multiply by 0.85)  
**Step 4:** Calculate loan amount: $\text{Purchase Price} \times \text{Safe Loan %}$

**Example:** Buying \$5,000 of SPY, expecting max 25% drop with 15% safety cushion:

$$\text{Safe Loan %} = (1 - 0.25) \times 0.70 \times 0.85 = 0.75 \times 0.70 \times 0.85 = 44.6\%$$

$$\text{Max Safe Loan} = \$5,000 \times 0.446 = \$2,230$$

$$\text{Your Cash Needed} = \$5,000 - \$2,230 = \$2,770$$

---

## Pattern Day Trading (PDT) Rules

If you make **4+ day trades in 5 business days**, you're flagged as a Pattern Day Trader:

- **Must maintain**: Minimum \$25,000 equity
- **Buying power**: 4× your maintenance margin excess
- **Restriction**: Can't day trade if you fall below \$25,000

---

## IRAs and "Limited Margin"

IRAs have **limited margin**, which means:
- ✅ Can trade with unsettled cash (avoids good faith violations)
- ❌ Cannot borrow money
- ❌ Cannot short sell

It's basically just a settlement convenience, not real borrowing power.

---

## Key Risks

1. **Amplified losses**: A 10% stock drop on a 50% margin position = 20% loss on your equity
2. **Margin calls**: Forced to deposit money or sell at the worst times
3. **Interest costs**: Accrues whether you're winning or losing
4. **Liquidation without notice**: Fidelity can sell your stuff if you're in a margin call

---

## Pro Tips

### **Use Fidelity's Margin Calculator**
Available 6 AM to market close—model trades before making them.

### **Watch the Right Balance**
- **Trading without interest?** Monitor "Available without margin impact"
- **Want max buying power?** Check "Margin buying power"
- **Day trading?** Use "Intraday buying power"

### **Keep a Cushion**
Don't max out your margin—leave room for market volatility. Aim to stay well above the 30% maintenance requirement.

### **Understand What You're Buying**
Some securities (penny stocks, certain ETFs) have **higher margin requirements** or aren't marginable at all.

---

## Bottom Line

Margin is a powerful tool that can amplify both gains and losses. It's best used by experienced investors who:
- Understand the math
- Can handle the volatility
- Have a plan for margin calls
- Monitor their accounts closely

If you're just starting out, consider sticking with cash until you're comfortable with the mechanics and risks.

---

## Your Specific Question Answered

**"What if I purchase an asset worth more than \$40?"**

If you buy something for **\$100**:
- The \$40 "available without margin impact" gets used first
- The remaining \$60 is **borrowed as a margin loan** against your existing securities
- **You WILL trigger a margin loan** ⚠️
- **Interest WILL be charged** on that \$60 ❌

If you buy something for **\$12,000**:
- You'll use your \$40 cash
- You'll borrow **\$11,960** on margin (nearly the full amount!)
- **Interest starts accruing** on the \$11,960 borrowed ❌
- Your non-margin buying power of \$10,000 simply means you have enough collateral to support this loan
- Your margin buying power allows this because \$12,000 < \$20,000

**The magic threshold to avoid ALL interest is your "Available Without Margin Impact" (\$40)**—anything beyond that, and you're borrowing the difference and paying interest on it!