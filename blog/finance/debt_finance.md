@def title = "The Mathematics of Debt in Personal Finance"
@def published = "13 February 2026"
@def tags = ["math", "finance"]

# The Mathematics of Debt in Personal Finance
## When to Borrow, When to Be Debt-Free, and Why the Math Is Not Obvious

@@toc@@

---

## 1. The Two Camps

**Camp A: "Debt is evil."** Pay off everything. Dave Ramsey. Sleep well at night. Never owe anyone anything.

**Camp B: "Debt is a tool."** Leverage cheap capital. Your money should work harder than the interest you're paying. Rich people borrow; poor people save.

Both camps have a point. But only one has the math. Let's work through it.

---

## 2. The Fundamental Inequality

Debt makes sense when and only when:

$$\boxed{r_{\text{invest}} > r_{\text{borrow}}}$$

If you can earn 10% on your investments but borrow at 6%, every dollar you borrow instead of paying off earns you 4% spread. Over time, this compounds into real wealth.

But this simple inequality hides three traps:
1. $r_{\text{invest}}$ is uncertain; $r_{\text{borrow}}$ is fixed
2. **Volatility drag** means leveraged returns aren't just $L \times r$
3. **Ruin risk** — leverage can wipe you out before the long run arrives

---

## 3. The Kelly Criterion: Optimal Leverage from First Principles

### 3.1 The Setup

You have access to an investment with:
- Expected excess return: $\mu - r_f$ (above risk-free rate)
- Volatility: $\sigma$
- Borrow rate: $r$ (could be different from $r_f$)

You can choose your leverage $f$ — how many dollars of exposure per dollar of equity. $f = 1$ means no leverage. $f = 2$ means 2:1 leverage (borrowed as much as you own).

### 3.2 The Growth Rate Formula

Your long-run compound growth rate (geometric return) as a function of leverage:

$$g(f) = r_f + f(\mu - r_f) - \frac{1}{2}f^2\sigma^2$$

The first term is the risk-free rate. The second is the levered excess return. The third is the **volatility drag** — and it grows as the *square* of leverage. This is the killer.

### 3.3 The Optimal Leverage (Kelly Fraction)

Take the derivative, set to zero:

$$g'(f) = (\mu - r_f) - f\sigma^2 = 0$$

$$\boxed{f^* = \frac{\mu - r_f}{\sigma^2}}$$

This is the **Kelly criterion** for continuous-time investing. It tells you the leverage that maximizes your long-run compound wealth growth.

### 3.4 What Kelly Says About Real Investments

| Investment | $\mu$ | $\sigma$ | $r$ (borrow) | Kelly $f^*$ | Interpretation |
| --- | --- | --- | --- | --- | --- |
| S\&P 500 (margin at 6%) | 10% | 16% | 6% | **1.56×** | Slight leverage is optimal |
| S\&P 500 (margin at 8%) | 10% | 16% | 8% | **0.78×** | No leverage — hold less than 100% stocks! |
| Real estate (mortgage 3%) | 7.5%\* | 5% | 3% | **18×** | Leverage aggressively (capped by bank at 5×) |
| Real estate (mortgage 6.5%) | 7.5%\* | 5% | 6.5% | **4×** | Still leverage, but less |
| LINK (borrow at 5%) | 30% | 80% | 5% | **0.39×** | Hold only 39% of net worth in LINK |
| Treasury arb (borrow at 4%) | 5% | 2% | 4% | **25×** | Huge leverage — low vol makes it safe |

*\*Real estate total return includes imputed rent / rental yield (~4%) plus appreciation (~3.5%)*

### 3.5 Key Insights

**1. Low volatility makes leverage safe.** Real estate and treasury arbitrage support high leverage because their volatility is low. The $\sigma^2$ in the denominator is what matters.

**2. High volatility kills leverage.** LINK with 80% vol has Kelly of 0.39× — the math says hold *less than half* your net worth in LINK, even if you expect 30% annual returns. The volatility drag at higher leverage destroys wealth.

**3. The borrow rate matters enormously.** For the S&P 500, the difference between borrowing at 6% and 8% takes optimal leverage from 1.56× to 0.78×. Two percentage points on the borrow rate flips the answer from "leverage" to "don't leverage."

---

## 4. Volatility Drag: The Hidden Tax on Leverage

### 4.1 The Intuition

A +50% gain followed by a −50% loss doesn't break even:

$$\$100 \xrightarrow{+50\%} \$150 \xrightarrow{-50\%} \$75$$

You lost 25%. At 2× leverage:

$$\$100 \xrightarrow{+100\%} \$200 \xrightarrow{-100\%} \$0$$

You're wiped out.

### 4.2 The Math

The arithmetic mean of returns doesn't equal the geometric mean (what you actually earn):

$$g = \bar{r} - \frac{1}{2}\sigma^2$$

where $\bar{r}$ is the arithmetic average return and $\sigma^2$ is the variance. The $\frac{1}{2}\sigma^2$ term is the **volatility drag**.

With leverage $f$:
- Arithmetic return scales as $f \times \bar{r}$ — linear
- Volatility drag scales as $\frac{1}{2} f^2 \sigma^2$ — **quadratic**

At some point, the quadratic penalty overwhelms the linear benefit. That crossover is the Kelly fraction.

### 4.3 Example: Alternating +20% / −15%

The arithmetic average return is $+2.5\%$ per period. Sounds positive! But:

| Leverage | After 10 Periods | Total Return |
| --- | --- | --- |
| 1× (no leverage) | \$110.4 | **+10.4%** |
| 2× | \$90.4 | **−9.6%** |
| 3× | \$52.8 | **−47.2%** |

> At 2× leverage, a seemingly profitable investment **loses money**. At 3×, it loses nearly half your capital. This is volatility drag in action. The arithmetic return is positive, but the geometric return at high leverage is negative.

### 4.4 The Growth Rate Curve for S&P 500

With $\mu = 10\%$, $\sigma = 16\%$, $r_f = 4.5\%$:

| Leverage $f$ | Annual Growth Rate $g(f)$ |
| --- | --- |
| 0.5× | 6.93% |
| 1.0× (unleveraged) | 8.72% |
| 1.5× | 9.87% |
| **2.15×** (Kelly) | **10.38%** |
| 2.5× | 10.25% |
| 3.0× | 9.48% |
| 4.0× | 6.02% |
| 5.0× | 0.00% |

> At 5× leverage on the S\&P 500, your expected compound growth is **zero** — you're spinning your wheels despite a 10% expected return. This is why 3× leveraged ETFs (like TQQQ) underperform what people expect over long holding periods.

---

## 5. The Half-Kelly Wisdom

Professional traders and quants almost universally use **half-Kelly** ($f = f^*/2$) instead of full Kelly. Why?

### 5.1 Kelly Is Fragile

The Kelly fraction assumes you know $\mu$ and $\sigma$ exactly. You don't. If your estimate of $\mu$ is off by even a little bit, the Kelly fraction can be way off — and overleveraging is catastrophic.

### 5.2 Half-Kelly Gives 75% of the Growth at Half the Risk

The growth rate at half-Kelly:

$$g(f^*/2) = \frac{3}{4} \cdot g(f^*)$$

You lose only 25% of the optimal growth rate, but your maximum drawdowns and probability of ruin are dramatically lower.

### 5.3 Practical Rule

$$\boxed{f_{\text{practical}} = \frac{f^*}{2} = \frac{\mu - r}{2\sigma^2}}$$

For the S\&P 500 with margin at 6%: $f_{\text{practical}} = 1.56/2 = 0.78\times$ — basically no leverage. The math says that for most people investing in stocks, **the optimal amount of leverage is approximately zero**.

---

## 6. When Debt IS Optimal: The Three Good Debts

### 6.1 Mortgage Debt (Low Rate Environment)

At 3% mortgage rate, real estate with 7.5% total return:

$$f^* = \frac{0.075 - 0.03}{0.05^2} = 18\times$$

Banks cap you at 5× (20% down). You're *under-levered* relative to Kelly! This is why mortgages at low rates are the best deal in personal finance — the math says you should be borrowing *more* than the bank allows.

Even at 6.5% mortgage rates, the Kelly is still ~4× — a standard mortgage is mathematically justified.

**Why mortgages are special:**
- **Low volatility**: Housing prices fluctuate ~5% annually, not 16% like stocks or 80% like crypto
- **Non-callable**: The bank can't margin-call your house\*
- **Tax-deductible interest**: Lowers effective borrow rate
- **Inflation hedge**: Your debt is fixed; inflation erodes it
- **Forced savings**: Builds equity even if you'd otherwise spend

*\*Unless you stop paying, but that's a different failure mode.*

### 6.2 Business Debt

If you run a business earning 20% ROE with 8% volatility, borrowing at 8%:

$$f^* = \frac{0.20 - 0.08}{0.08^2} = 18.75\times$$

Established businesses with stable cash flows support enormous leverage. This is why corporate debt exists — and why private equity works (lever stable businesses at 4-6×).

### 6.3 Spread Trades (Borrow Low, Invest Higher)

If you can borrow at a fixed rate below your expected return on a low-volatility investment, the Kelly fraction is huge. Examples:
- Borrow at 4% via mortgage, invest freed-up cash in index funds at 10%
- Borrow at 5% via HELOC, invest in dividend stocks at 7-8%
- Borrow at 3% in a 0% interest promo, park in money market at 5%

---

## 7. When Debt Is Destructive: The Three Bad Debts

### 7.1 Consumer Debt (Credit Cards, Car Loans)

Credit card: $r_{\text{borrow}} = 24\%$. What investment reliably returns 24%? None.

$$r_{\text{invest}} < r_{\text{borrow}} \implies \text{always pay off first}$$

There is no mathematical argument for carrying 24% debt. Every dollar you owe at 24% is a guaranteed 24% return when you pay it off. No investment beats that risk-adjusted.

### 7.2 High-Rate Margin Debt

Borrowing at 8-12% on margin to buy stocks with 10% expected return and 16% volatility:

$$f^* = \frac{0.10 - 0.10}{0.16^2} = 0$$

At 10% borrow rate, the optimal leverage is **zero**. The spread is gone, but the volatility risk remains. You're paying for the privilege of losing money faster.

### 7.3 Overleveraged Anything

Even the best investment becomes destructive at too-high leverage. The growth rate formula:

$$g(f) = r_f + f(\mu - r_f) - \frac{1}{2}f^2\sigma^2$$

becomes negative when:

$$f > \frac{2(\mu - r_f)}{\sigma^2}$$

This is **twice Kelly**. Beyond 2× Kelly, your expected *compound* wealth **shrinks**. You are literally expected to go broke over time.

> **Rule**: If $f > 2 f^*$, you are mathematically guaranteed to lose wealth in the long run, regardless of the expected return.

---

## 8. The Cost of Being Debt-Free

This is the part Dave Ramsey doesn't tell you. Being debt-free has a cost — the **opportunity cost** of capital that could be working for you.

### 8.1 Example: Prepay Mortgage vs. Invest

You have \$200,000. Two choices:
1. **Pay off** your 6.5% mortgage
2. **Invest** in S\&P 500 at ~10% expected return

After 20 years:

| Strategy | Outcome |
| --- | --- |
| Pay off mortgage | Save \$704,729 in total payments\* |
| Invest in S\&P 500 | Grow to \$1,345,500 |
| **Difference** | **\$640,771** |

*\*Total value of 6.5% compounded over 20 years on \$200k*

> By choosing to be debt-free, you gave up **\$640,000** in expected wealth. That's the price of sleeping well.

### 8.2 But Wait — Risk Adjustment

The S&P could crash. The mortgage payment is guaranteed savings. Risk-adjusted, the picture is muddier:

- **If you have a 30-year time horizon**: invest. The probability of stocks beating 6.5% over 30 years is historically >90%.
- **If you might need the money in 5 years**: pay off the mortgage. The probability of stocks beating 6.5% over 5 years is only ~65%.
- **If the volatility keeps you up at night**: pay off the mortgage. Mental health has real economic value.

### 8.3 The Framework

$$\text{Cost of debt-free} = (r_{\text{invest}} - r_{\text{borrow}}) \times \text{capital} \times \text{time}$$

If the spread $(r_{\text{invest}} - r_{\text{borrow}})$ is positive and your time horizon is long enough to ride out volatility, carrying debt is mathematically superior.

---

## 9. The Wisdom: A Decision Framework

### 9.1 The Flow Chart

**Step 1**: Is $r_{\text{borrow}} > 10\%$? → **Pay it off. No exceptions.**

**Step 2**: Is $r_{\text{borrow}}$ < $r_{\text{risk-free}}$? → **Carry the debt. Invest the freed capital in anything safe.**

**Step 3**: Compute the Kelly fraction:

$$f^* = \frac{\mu_{\text{invest}} - r_{\text{borrow}}}{\sigma_{\text{invest}}^2}$$

- If $f^* > 1$: leverage is optimal. Keep the debt and invest.
- If $0.5 < f^* < 1$: borderline. Use half-Kelly. Maybe carry some debt.
- If $f^* < 0.5$: pay off the debt. The risk isn't worth the spread.

**Step 4**: Is the debt callable (margin loan, variable rate)? → **Reduce $f^*$ by 50%.** Callable debt can kill you at the worst moment.

**Step 5**: What's your time horizon?
- \> 10 years: trust the math. Carry the debt if Kelly says so.
- 3-10 years: use half-Kelly at most.
- < 3 years: pay it off.

### 9.2 The Rules of Thumb

$$\boxed{
\begin{aligned}
& \textbf{Always pay off:} && r_{\text{borrow}} > 10\% \\[6pt]
& \textbf{Always carry:} && r_{\text{borrow}} < 3\% \text{ (it's free money)} \\[6pt]
& \textbf{Use Kelly:} && 3\% < r_{\text{borrow}} < 10\% \\[6pt]
& \textbf{Never exceed:} && f = 2f^* \text{ (ruin boundary)} \\[6pt]
& \textbf{In practice:} && f = f^*/2 \text{ (half-Kelly)}
\end{aligned}
}$$

### 9.3 The Three Laws of Personal Debt

**Law 1: Debt is a bet on spread.**  
Every dollar of debt is a bet that your return on the freed capital exceeds the borrow cost. If the spread is negative (credit cards), you're guaranteed to lose. If positive, it's a question of magnitude and risk.

**Law 2: Volatility makes leverage dangerous.**  
The Kelly fraction scales as $1/\sigma^2$. Double the volatility, quarter the safe leverage. This is why borrowing to buy a house (low vol) is smart, but borrowing to buy crypto (high vol) requires extreme caution.

**Law 3: Ruin is permanent.**  
The expected return of a leveraged investment is irrelevant if you go bust before the expected value materializes. The geometric mean, not the arithmetic mean, determines your wealth. A 50% loss requires a 100% gain to recover. At high leverage, one bad year can erase a decade of good ones.

---

## 10. Applied: Your Personal Debt Audit

Ask yourself for each debt:

| Debt | Rate | Can I Invest Freed Capital At Higher Return? | Investment Vol | Kelly $f^*$ | Verdict |
| --- | --- | --- | --- | --- | --- |
| Credit card | 24% | No | — | — | ❌ Pay off immediately |
| Car loan | 7% | Maybe (S\&P ~10%) | 16% | 0.78× | ⚠️ Marginal — pay off if nervous |
| Student loan | 5% | Yes (S\&P ~10%) | 16% | 1.95× | ✅ Carry and invest |
| Mortgage (6.5%) | 6.5% | Yes (S\&P ~10%) | 16% | 1.37× | ✅ Carry and invest |
| Mortgage (3%) | 3% | Absolutely | 16% | 2.73× | ✅ Never pay off early |
| Margin loan (8%) | 8% | Barely (10% stocks) | 16% | 0.78× | ⚠️ Risky — half-Kelly says no leverage |
| Crypto borrow (5%) | 5% | If thesis is right | 80% | 0.39× | ⚠️ Only small fraction of portfolio |

---

## 11. The Meta-Lesson

The biggest insight from all this math:

> **The optimal amount of debt is almost never zero, and almost never "as much as possible."**

It's somewhere in between, determined by three numbers: the spread ($\mu - r$), the volatility ($\sigma$), and your time horizon. The Kelly formula encodes all of this into a single number.

Being completely debt-free is financially suboptimal for most people with stable income and long time horizons. But being overleveraged is catastrophic. The math points to a moderate middle:

- **Carry your mortgage** (especially at low rates)
- **Kill credit card debt** (always)
- **Use small leverage** on high-conviction, low-vol investments
- **Never exceed half-Kelly** on anything
- **Keep enough cash** that no market crash forces you to sell at the bottom

The Dave Ramseys of the world are wrong on the math but right on the psychology. If carrying debt causes you stress that impairs your decision-making, the mathematical optimum doesn't matter. **The best financial plan is the one you'll actually follow.**

But if you can handle the nuance: strategic debt is one of the most powerful tools in building wealth. The rich understand this. Now you have the math to understand why.

---

## 12. The Uncomfortable Truth: "Debt-Free" Is Often Wealth-Destroying

The math is unambiguous: **being debt-free is often wealth-destroying** when you have access to low-rate debt and long time horizons.

### 12.1 The Core Argument

Every dollar you use to pay off a 6.5% mortgage is a dollar that *could* be compounding at 10% in the S\&P. The spread — 3.5% per year — compounds over decades into enormous sums. That \$640,000 difference over 20 years from [Section 8](#the-cost-of-being-debt-free) isn't hypothetical; it's the mathematical consequence of $1.10^{20}$ vs $1.065^{20}$.

### 12.2 Why "Debt-Free" Feels Right But Isn't

The psychological appeal of debt-free is **certainty**. Paying off a 6.5% loan is a guaranteed 6.5% return. The S\&P's 10% is an *average* — some years it's −30%. Your brain weighs the certainty of debt reduction far more heavily than the *expected* investment gain. This is classic loss aversion.

But over 20–30 year horizons, the S\&P has beaten 6.5% in roughly **90%+ of rolling periods**. You're paying a massive premium — hundreds of thousands of dollars — for protection against a ~10% probability scenario.

### 12.3 The Real Kicker: Inflation

A fixed-rate mortgage is a **short position on the dollar**. If you borrow \$400k at 6.5% and inflation runs at 3%, your real borrow rate is ~3.5%. Inflation literally erodes your debt while your assets (house, stocks) rise with inflation. Paying off that debt early means *closing a winning trade*.

### 12.4 Where the Conventional Wisdom IS Right

- **Credit card debt (20%+)**: Pay it off immediately. No investment reliably beats 20%.
- **If you can't stomach volatility**: The psychological cost of seeing your portfolio crash 40% while owing \$300k on a mortgage is real. If it causes you to panic-sell stocks at the bottom, the math doesn't matter — you'll underperform anyway.
- **Variable-rate or callable debt**: Can blow up at the worst moment. A margin call during a crash forces you to sell low.

### 12.5 The One-Liner

> Dave Ramsey's advice maximizes **peace of mind**. The Kelly criterion maximizes **wealth**. They give different answers because they're optimizing different objectives.

Being debt-free at a 3% mortgage isn't conservative — it's *leaving the best risk-adjusted trade in personal finance on the table*. At 6.5% it's more debatable. At 24% credit card debt, yes, pay it off yesterday. The math depends entirely on the rate, the volatility of your investment, and your time horizon.

**The wealthy don't avoid debt — they use it strategically.** The question is never "should I have debt?" but "what is the optimal amount of debt given my spread, my volatility, and my time horizon?" The Kelly formula answers that question precisely.
