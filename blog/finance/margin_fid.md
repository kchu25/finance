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

| Item | Value |
|------|-------|
| Stock A (existing) | \$15,000 |
| Stock B (new) | \$20,000 |
| **Total Securities** | **\$35,000** |
| Margin Loan | \$19,960 |
| **Your Equity** | **\$15,040** |

$$\text{Equity} = \$35,000 - \$19,960 = \$15,040$$

Maintenance requirement (30%):

$$\text{Required Equity} = \$35,000 \times 0.30 = \$10,500$$

You're safe! (\$15,040 > \$10,500) ✅

---

**Now Stock B Drops 30% (from \$20,000 to \$14,000):**

| Item | Value |
|------|-------|
| Stock A (unchanged) | \$15,000 |
| Stock B (dropped) | \$14,000 |
| **Total Securities** | **\$29,000** |
| Margin Loan (unchanged) | \$19,960 |
| **Your Equity** | **\$9,040** |

$$\text{Your Equity} = \$29,000 - \$19,960 = \$9,040$$

Required equity:

$$\text{Required Equity} = \$29,000 \times 0.30 = \$8,700$$

Still okay! (\$9,040 > \$8,700) ✅

---

**But What if Stock A ALSO Drops 20% (from \$15,000 to \$12,000)?**

| Item | Value |
|------|-------|
| Stock A (dropped) | \$12,000 |
| Stock B (dropped) | \$14,000 |
| **Total Securities** | **\$26,000** |
| Margin Loan (unchanged) | \$19,960 |
| **Your Equity** | **\$6,040** |

$$\text{Your Equity} = \$26,000 - \$19,960 = \$6,040$$

Required equity:

$$\text{Required Equity} = \$26,000 \times 0.30 = \$7,800$$

**MARGIN CALL!** ⚠️

$$\text{Shortfall} = \$7,800 - \$6,040 = \$1,760$$

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