@def title = "The Perpetual Debt Playbook: Managing No-Maturity DeFi Loans"
@def published = "15 February 2026"
@def tags = ["math", "finance", "crypto"]

# The Perpetual Debt Playbook
## When Your Asset Outgrows Your Debt, Do You Still Repay?

@@toc@@

---

## 1. The Uncomfortable Setup

You have a DeFi loan — say on [Aave](https://aave.com/). There is no maturity date. No banker calls you.
No monthly payment schedule. The debt just... *sits there*, accruing interest at a variable rate.

Meanwhile, your collateral — the asset you deposited — is growing faster than that interest rate.
The math from [The Mathematics of Debt](/blog/finance/debt_finance/) says you should keep the debt.
The spreadsheets agree. The Kelly criterion agrees.

And yet something feels deeply wrong about carrying a loan *forever*.

This post is about resolving that tension — not by ignoring the math, but by building a *strategy*
on top of it.

---

## 2. Why Perpetual Debt Feels Wrong

Three psychological forces fight you:

**Loss aversion.** Owing \$6,000 *hurts* more than having \$6,000 *feels good*. Kahneman and Tversky
showed that losses loom roughly 2× larger than equivalent gains. The debt is a persistent "loss" on
your mental balance sheet, even though your equity is positive and growing.

**Ambiguity aversion.** With a mortgage, you know the schedule: 360 payments, done. With a perpetual
DeFi loan, there is no finish line. No countdown. Humans hate open-ended uncertainty more than they
hate known bad outcomes.

**Social signaling.** "I'm debt-free" is a status symbol. "I'm carrying a perpetual variable-rate
loan on a smart contract" is... not something you say at dinner parties.

None of these are mathematical arguments. They are *real*, but they are not *reasons to repay*.

---

## 3. What Actually Happens to Perpetual Debt

Let the asset price be $P_t$, the number of collateral tokens be $Q$, the debt at time $t$ be
$D_t = D_0 (1+r)^t$ where $r$ is the borrow APR, and the asset's annualized return be $\mu$.

The LTV (loan-to-value) at time $t$ is:

$$\text{LTV}(t) = \frac{D_0 (1+r)^t}{Q \cdot P_0 (1+\mu)^t} = \text{LTV}_0 \cdot \bigg(\frac{1+r}{1+\mu}\bigg)^t$$

If $\mu > r$ — the asset grows faster than the borrow rate — then:

$$\lim_{t \to \infty} \text{LTV}(t) = 0$$

**The debt doesn't just become manageable. It becomes *irrelevant*.** The LTV asymptotes to zero.
The debt shrinks relative to your portfolio every single day.

### Concrete example

Suppose 2,878 LINK as collateral, \$6,000 debt at 5% APR, LINK growing at 30%/yr:

| Year | LINK Price | Portfolio Value | Debt | LTV | Equity |
|:----:|:----------:|:--------------:|:----:|:---:|:------:|
| 0 | \$8.40 | \$44,965 | \$6,000 | 13.3% | \$38,965 |
| 1 | \$10.92 | \$58,455 | \$6,300 | 10.8% | \$52,155 |
| 2 | \$14.20 | \$75,991 | \$6,615 | 8.7% | \$69,376 |
| 3 | \$18.45 | \$98,789 | \$6,946 | 7.0% | \$91,843 |
| 5 | \$31.19 | \$166,953 | \$7,658 | 4.6% | \$159,295 |
| 10 | \$115.80 | \$619,883 | \$9,773 | 1.6% | \$610,110 |

By year 5, the debt is less than 5% of the portfolio. By year 10, it's noise — 1.6%.
You'd be paying off less than a rounding error.

### Even at 10% growth

| Year | LINK Price | Portfolio Value | Debt | LTV |
|:----:|:----------:|:--------------:|:----:|:---:|
| 0 | \$8.40 | \$44,965 | \$6,000 | 13.3% |
| 5 | \$13.53 | \$72,417 | \$7,658 | 10.6% |
| 10 | \$21.79 | \$116,628 | \$9,773 | 8.4% |

Still shrinking, just slower. The spread between 10% return and 5% borrow is only 5pp, but
compounding does its work.

---

## 4. The Asymmetry Argument

Here is the deepest reason not to rush to repay:

> **Debt is denominated in dollars. Your asset is not.**

Your \$6,000 debt is always \$6,000 (plus interest). It doesn't care what LINK does. But the *cost*
of repaying, measured in LINK, changes dramatically:

| LINK Price | LINK Needed to Repay \$6,000 | % of 5,353 LINK |
|:----------:|:--------------------------:|:---------------:|
| \$8.40 | 714 | 13.3% |
| \$16.80 | 357 | 6.7% |
| \$25.00 | 240 | 4.5% |
| \$50.00 | 120 | 2.2% |
| \$100.00 | 60 | 1.1% |
| \$500.00 | 12 | 0.2% |

At \$8.40, repaying costs you 714 LINK — a meaningful chunk of your stack.
At \$100, it costs 60 LINK — pocket change.

**If you believe the asset will appreciate, every day you wait makes the debt cheaper to repay
*in real terms*.** This is the mirror image of inflation eroding mortgage debt, but on
a much more aggressive timeline.

---

## 5. The Opportunity Cost of Repaying

Selling 714 LINK today at \$8.40 to clear \$6,000 of debt saves you \$300/yr in interest (at 5%).
But those 714 LINK, if LINK appreciates, are worth:

| Horizon | 10% Growth | 20% Growth | 30% Growth | 50% Growth |
|:-------:|:----------:|:----------:|:----------:|:----------:|
| 1 year | \$6,597 | \$7,197 | \$7,797 | \$8,996 |
| 3 years | \$7,983 | \$10,364 | \$13,177 | \$20,242 |
| 5 years | \$9,659 | \$14,924 | \$22,269 | \$45,544 |
| 10 years | \$15,556 | \$37,136 | \$82,682 | \$345,852 |

The interest you "save" by repaying is \$300–\$500/yr. The upside you *forfeit* by selling
those 714 LINK could be tens of thousands. The expected value of holding crushes the expected
value of repaying — **as long as $\mu > r$**.

---

## 6. So When *Should* You Repay?

The math says "never, as long as $\mu > r$." But the math assumes:

1. **You know $\mu > r$** — You don't. It's an estimate. Markets are uncertain.
2. **The rate $r$ stays stable** — On Aave, it doesn't. Variable rates can spike.
3. **You won't get liquidated** — The path matters, not just the destination.
4. **You can stomach the volatility** — Psychology is a real constraint.

These four caveats define the *actual* repayment strategy.

---

## 7. The Rate Monitor

Aave's variable borrow rate is the silent killer. Your \$6,000 debt costs:

| Borrow Rate | Annual Cost | Monthly | Daily |
|:-----------:|:-----------:|:-------:|:-----:|
| 3% | \$180 | \$15 | \$0.49 |
| 5% | \$300 | \$25 | \$0.82 |
| 8% | \$480 | \$40 | \$1.32 |
| 12% | \$720 | \$60 | \$1.97 |
| 20% | \$1,200 | \$100 | \$3.29 |

**Rule of thumb:** If the borrow rate exceeds your conservative estimate of asset returns *minus*
a risk premium, repay. For crypto with its ~80% annual volatility, you need a substantial risk premium.

The break-even required return at each borrow rate:

| Borrow Rate | No Risk Premium | 10% Risk Premium | 20% Risk Premium |
|:-----------:|:---------------:|:-----------------:|:-----------------:|
| 3% | 3% | 13% | 23% |
| 5% | 5% | 15% | 25% |
| 8% | 8% | 18% | 28% |
| 12% | 12% | 22% | 32% |
| 20% | 20% | 30% | 40% |

If borrow rates hit 12%+ and you're not confident LINK can return 22%+ annually, it's time to
de-lever.

---

## 8. The Debt Ratchet: A Practical Strategy

Here is the resolution to the "keep it forever" discomfort. Instead of binary (repay all vs. repay
nothing), use a **debt ratchet**:

> **Every time the asset price doubles, repay half the remaining debt.**

This is a *convex* strategy: you repay from a position of strength (price went up), using profits,
not principal. And each repayment makes your position *geometrically* safer.

### How it plays out

Starting: 2,878 LINK collateral, \$6,000 debt, LT = 0.71

| Trigger | Repay | Remaining Debt | New LTV | Liq Price | Drop Buffer |
|:-------:|:-----:|:--------------:|:-------:|:---------:|:-----------:|
| LINK → \$16.80 (2×) | \$3,000 | \$3,000 | 6.2% | \$1.47 | 91% |
| LINK → \$25 | \$1,500 | \$1,500 | 2.1% | \$0.73 | 97% |
| LINK → \$50 | \$750 | \$750 | 0.5% | \$0.37 | 99% |
| LINK → \$100 | \$375 | \$375 | 0.1% | \$0.18 | 99.8% |

After four ratchets, you've repaid \$5,625 of the original \$6,000, and the remaining \$375 is
a rounding error on a \$287,800 position. You could sneeze and pay it off.

### Why this works psychologically

- You *are* paying down debt → satisfies the "I'm making progress" instinct
- You only pay from *gains* → never selling at a loss
- Each ratchet makes liquidation impossible → removes the anxiety
- There's a clear rule → eliminates decision fatigue
- The debt shrinks *exponentially* → you can see the finish line

### Why this works mathematically

At each doubling, the debt has already been halved *in real terms* (relative to asset value).
You're halving it again in *nominal terms*. So after $k$ doublings, the LTV is:

$$\text{LTV}_k = \text{LTV}_0 \cdot \frac{1}{2^k} \cdot \frac{1}{2^k} = \text{LTV}_0 \cdot \frac{1}{4^k}$$

The first factor comes from the price doubling (denominator grows). The second comes from you
halving the debt (numerator shrinks). The LTV drops by 4× at each trigger. Starting at 13.3%:

- After 1st doubling: $13.3\% / 4 = 3.3\%$
- After 2nd doubling: $3.3\% / 4 = 0.8\%$
- After 3rd: $0.2\%$

Three doublings and the debt is a footnote.

---

## 9. Alternative Strategies

### 9a. Percentage-of-Profit Repayment

> Every time you realize profits (sell some LINK), allocate 20% to debt repayment.

**Pros:** Simple. Scales with your actual cash flow. Doesn't require you to time doublings.

**Cons:** If you never take profit, you never repay. Can lead to indefinite carrying.

### 9b. Time-Based Reduction

> Repay 10% of the outstanding debt every 6 months, regardless of price.

**Pros:** Predictable. You know the debt will be gone in ~5 years.

**Cons:** You might sell at bad prices. Ignores the asset's trajectory.

### 9c. Rate-Triggered Repayment

> If the borrow rate exceeds 8%, repay 50% of the debt immediately. If it exceeds 15%, repay all.

**Pros:** Directly addresses the biggest risk (rate spikes).

**Cons:** Requires monitoring. Reactive rather than proactive.

### 9d. LTV Ceiling

> Set a hard LTV ceiling (say 20%). If LTV rises above it (asset falls), repay to bring it back down.
> If LTV falls below it (asset rises), do nothing (or borrow more if you're aggressive).

**Pros:** Risk-focused. Keeps you from blowing up.

**Cons:** Forces selling at exactly the worst time (asset is falling). Anti-momentum.

---

## 10. The Optimal Hybrid

The best strategy combines elements:

1. **Set a rate ceiling** — If borrow APR > 10%, begin aggressive repayment.
2. **Use the debt ratchet** — On every price doubling, repay half.
3. **Set an LTV floor alert** — If LTV rises above 30%, add collateral or partially repay.
4. **Never repay from a drawdown** — Only repay when the asset is at or near highs.

This gives you:
- **Upside exposure** (you keep the debt while the asset is running)
- **Rate protection** (you de-lever when borrowing gets expensive)
- **Liquidation safety** (LTV floor keeps you far from the danger zone)
- **Psychological closure** (the ratchet shows the debt shrinking over time)

---

## 11. The Mathematical Framework

Let's formalize. Define the **debt carry value** at time $t$:

$$V_{\text{carry}}(t) = Q \cdot P_0 \bigg[(1+\mu)^t - 1\bigg] - D_0 \bigg[(1+r)^t - 1\bigg]$$

The first term is the appreciation of the asset you kept (instead of selling to repay). The second
is the accumulated interest cost. Carrying the debt is profitable when $V_{\text{carry}}(t) > 0$,
which holds when:

$$\frac{Q \cdot P_0}{D_0} > \frac{(1+r)^t - 1}{(1+\mu)^t - 1}$$

For $\mu > r$, the right side is less than 1 for all $t > 0$. Since the left side (portfolio/debt)
is typically much greater than 1, **carrying the debt is almost always profitable when $\mu > r$**.

The carry becomes *more* profitable over time, because the right side converges to
$(\frac{1+r}{1+\mu})^t \to 0$.

### When carrying *stops* being profitable

If the asset's return drops below the borrow rate ($\mu < r$), the carry value turns negative.
But it doesn't turn negative *immediately* — there's a lag from accumulated gains. This gives you
a window to de-lever before the carry becomes a drag.

**The monitoring rule:** Track the trailing 6-month return of your asset. If it drops below the
borrow rate for two consecutive quarters, begin repayment.

---

## 12. The Stagnation Scenario

What if the asset doesn't crash but just... goes sideways?

| Year | LINK Price | Portfolio | Debt (5% APR) | LTV | Equity Lost |
|:----:|:----------:|:---------:|:-------------:|:---:|:-----------:|
| 0 | \$8.40 | \$44,965 | \$6,000 | 13.3% | — |
| 1 | \$8.40 | \$44,965 | \$6,300 | 14.0% | \$300 |
| 3 | \$8.40 | \$44,965 | \$6,946 | 15.5% | \$946 |
| 5 | \$8.40 | \$44,965 | \$7,658 | 17.0% | \$1,658 |
| 10 | \$8.40 | \$44,965 | \$9,773 | 21.7% | \$3,773 |

In 10 years of stagnation, the debt grows from \$6,000 to \$9,773 — an increase of \$3,773. That's
bad, but it's not catastrophic. Your equity only drops from \$38,965 to \$35,192 — a loss of
\$3,773 on a \$39k position, or about 9.7% over *a decade*.

**Compare:** If you had sold 714 LINK at \$8.40 to repay the debt on day 1, you'd have:
- 4,639 LINK × \$8.40 = \$38,968 equity, zero debt → effectively the same as \$38,965.

In a stagnation scenario, repaying early and carrying the debt are *roughly equivalent*. You
don't gain much by repaying, and you don't lose much by carrying. The real cost of carrying is
\$300/yr in interest — the cost of optionality.

---

## 13. The Decision Flowchart

When you feel the urge to repay, ask these questions in order:

**Step 1: Is the borrow rate above 10%?**
- Yes → Repay at least 50%. High rates compound fast.
- No → Continue.

**Step 2: Is your LTV above 25%?**
- Yes → Repay or add collateral. You're too close to liquidation.
- No → Continue.

**Step 3: Has the asset doubled since your last ratchet?**
- Yes → Repay half the remaining debt. Lock in gains.
- No → Continue.

**Step 4: Has the asset underperformed the borrow rate for 6+ months?**
- Yes → Begin gradual repayment (10%/month).
- No → **Do nothing. The math is working. Let it work.**

Most days, you should reach Step 4 and stop. The debt is fine. You don't need to touch it.
The compulsion to repay is loss aversion talking, not arithmetic.

---

## 14. The Philosophical Resolution

The discomfort with perpetual debt comes from treating debt as a *moral* category rather than a
*financial* one. When you owe someone money, it feels like an obligation — a weight. But on
Aave, there is no "someone." There is a smart contract. It doesn't judge you. It doesn't call
you. It doesn't care if you repay in a day or a decade.

The debt is not a relationship. It's a *position*. Like being long a stock or short a future.
You manage it based on the numbers, not based on how it makes you feel.

The debt ratchet resolves the tension because it gives you a *plan* — a clear set of rules that
says "you will eventually be debt-free, just not today." The math tells you to carry it. The
ratchet tells you *how* to carry it without losing sleep.

> **Carry the debt. Monitor the rate. Ratchet on strength. Sleep well.**

---

## 15. Summary

| Question | Answer |
|:---------|:-------|
| Should I carry DeFi debt indefinitely? | Yes, as long as $\mu > r$ and LTV is safe |
| Won't the interest eat me alive? | At 5%, it's \$300/yr on \$6k. Your asset likely gains more in a week |
| What if rates spike? | Repay aggressively if borrow rate > 10% |
| What if the asset drops? | Add collateral or partially repay if LTV > 25% |
| When should I actually repay? | On each asset doubling, repay half the remaining debt |
| Will I ever be debt-free? | Yes — 3–4 doublings and the debt is a rounding error |
| What if the asset goes sideways? | You lose ~\$300/yr in interest — the cost of optionality |
| Is this psychologically sustainable? | The ratchet gives you visible progress + a finish line |

The perpetual loan is not a burden. It's a *position*. Manage it like one.
