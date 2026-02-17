@def title = "Inflation Is a Debt Eraser: Why Borrowers Win and Savers Lose"
@def published = "15 February 2026"
@def tags = ["personal-finance", "macro"]

# Inflation Is a Debt Eraser
## Why Borrowers Win, Savers Lose, and the System Is Designed That Way

@@toc@@

---

## 1. The Deepest Reason to Carry Debt

The previous posts in this series covered [the math of leverage](/blog/finance/debt_finance/),
[the strategy for perpetual loans](/blog/finance/perpetual_debt/), and
[the intuition for why keeping debt feels wrong but is right](/blog/finance/debt_intuition/).

But there is a deeper force at work — one that makes debt even *more* attractive than the
spread alone would suggest. It's not a market phenomenon. It's not a trading strategy.
It's a *structural feature of the monetary system itself*.

**Inflation erodes debt.**

Not slowly. Not subtly. *Relentlessly.* Every year, every month, every day, the dollars you owe
become worth less. The number on your loan statement stays the same, but the *real weight* of
that number — what it costs you in labor, in goods, in opportunity — shrinks.

This is not a side effect. This is the system working *as designed*.

---

## 2. The Disappearing Dollar

The US dollar has lost 88% of its purchasing power since 1970.

\$1 in 1970 buys what \$0.12 buys today. Put another way: \$1 today is worth what \$0.12 was worth
to your grandparents.

This means a \$30,000 mortgage taken out in 1970 — a huge commitment at the time, roughly
equivalent to a \$242,000 mortgage today — shrinks in real terms every single year:

| Year | Nominal Debt | Real Value (1970 dollars) | Inflation Eroded |
|:----:|:------------:|:-------------------------:|:----------------:|
| 1970 | \$30,000 | \$30,000 | \$0 |
| 1980 | \$30,000 | \$20,661 | \$9,339 |
| 1990 | \$30,000 | \$14,229 | \$15,771 |
| 2000 | \$30,000 | \$9,799 | \$20,201 |
| 2010 | \$30,000 | \$6,749 | \$23,251 |
| 2026 | \$30,000 | \$3,716 | \$26,284 |

By 2026, that \$30,000 mortgage feels like owing \$3,716. **Inflation gifted the borrower \$26,284
in real terms.** The borrower didn't do anything clever. They just... waited. Inflation did the work.

The lender, meanwhile, got paid back in dollars that buy 88% less than the dollars they lent out.
They lost. The borrower won.

> **Every fixed-rate loan is a bet against the dollar. History shows: betting against the dollar
> always wins.**

---

## 3. The Real Borrow Rate

Here is the number that matters. Not the nominal rate on your loan — the **real** rate:

$$r_{\text{real}} = r_{\text{nominal}} - \pi$$

where $\pi$ is the inflation rate.

| Nominal Rate | Inflation 2% | Inflation 3% | Inflation 5% | Inflation 7% |
|:------------:|:------------:|:------------:|:------------:|:------------:|
| 3.0% | 1.0% | **0.0%** | **−2.0%** | **−4.0%** |
| 5.0% | 3.0% | 2.0% | **0.0%** | **−2.0%** |
| 6.5% | 4.5% | 3.5% | 1.5% | **−0.5%** |
| 8.0% | 6.0% | 5.0% | 3.0% | 1.0% |
| 10.0% | 8.0% | 7.0% | 5.0% | 3.0% |

**Bold** entries are free or negative — you are being *paid* to borrow in real terms.

At 3% inflation (the Fed's approximate long-run target), a 3% mortgage is **free money**. A 5%
mortgage costs you only 2% in real terms. Even a 6.5% mortgage only costs 3.5% in real purchasing
power.

And during inflationary spikes (5–7%, as in 2021–2023), even relatively high nominal rates
become cheap or free in real terms.

### What this means for DeFi

If you borrow USDC at 5% on Aave and inflation runs at 3%, your real borrow rate is 2%. You're
renting capital for 2% per year in real terms. Any asset that appreciates faster than 2% real
(not 5% nominal) justifies the debt.

**Inflation lowers the bar for profitable leverage.**

---

## 4. Why Wages Make Debt Shrink

Here is an angle most people miss entirely.

Your debt is fixed in nominal dollars. Your income grows with inflation (plus real wage growth).
Over time, a fixed debt payment becomes a smaller and smaller fraction of your income.

A \$50,000 salary growing at 4% per year (3% inflation + 1% real growth) against a fixed
\$13,000/yr mortgage payment (6.5% on \$200,000):

| Year | Salary | Mortgage Payment | % of Income |
|:----:|:------:|:----------------:|:-----------:|
| 0 | \$50,000 | \$13,000 | 26.0% |
| 5 | \$60,833 | \$13,000 | 21.4% |
| 10 | \$74,012 | \$13,000 | 17.6% |
| 15 | \$90,047 | \$13,000 | 14.4% |
| 20 | \$109,556 | \$13,000 | 11.9% |
| 25 | \$133,292 | \$13,000 | 9.8% |
| 30 | \$162,170 | \$13,000 | 8.0% |

The payment that consumed 26% of your income in year 1 consumes only 8% by year 30. You didn't
pay anything extra. You didn't refinance. Inflation and wage growth did it for you.

**This is why the first years of a mortgage feel crushing and the last years feel trivial.** Not
because you got richer (though you may have). Because the dollars got lighter.

> The psychological trick of "I need to pay this off early" is strongest precisely when the debt
> is heaviest in real terms — and that's when paying it off is *most expensive*.

This is the same [time inversion](/blog/finance/debt_intuition/#mental_model_5_the_time_inversion)
from the intuition post: urgency runs backwards. The moment the debt feels most burdensome is the
moment repaying costs you the most in real terms.

---

## 5. Assets Inflate. Debt Doesn't.

This is the asymmetry that makes borrowers rich.

A \$300,000 house with a \$240,000 mortgage (80% LTV). The house appreciates at 3.5% per year
(roughly tracking inflation plus a small real return). The mortgage stays fixed:

| Year | House Value | Mortgage | Equity | LTV |
|:----:|:-----------:|:--------:|:------:|:---:|
| 0 | \$300,000 | \$240,000 | \$60,000 | 80.0% |
| 5 | \$356,306 | \$240,000 | \$116,306 | 67.4% |
| 10 | \$423,180 | \$240,000 | \$183,180 | 56.7% |
| 15 | \$502,605 | \$240,000 | \$262,605 | 47.8% |
| 20 | \$596,937 | \$240,000 | \$356,937 | 40.2% |
| 30 | \$842,038 | \$240,000 | \$602,038 | 28.5% |

You started with \$60,000 in equity. Thirty years later, you have \$602,038 — a **10× gain** on
your initial \$60,000 down payment. The house only went up 2.8× in total. But because you used
leverage and inflation eroded the debt, your *equity* grew 10×.

This is the **leverage amplifier**: inflation pushes asset prices up while leaving debt fixed.
The gap between the two — your equity — widens every year.

### The same principle in crypto, amplified

Crypto assets don't just track inflation — they compound at rates that dwarf it. LINK, BTC, ETH
appreciate because of *adoption*, not just monetary debasement. So the inflation tailwind is
layered on top of an already-appreciating asset.

\$6,000 debt at 5% APR. 5,353 LINK at \$8.80:

| Scenario | Year 5 Portfolio | Year 5 Debt | Debt as % |
|:--------:|:----------------:|:-----------:|:---------:|
| Bear (10%/yr) | \$75,865 | \$7,658 | 10.1% |
| Base (25%/yr) | \$143,757 | \$7,658 | 5.3% |
| Bull (50%/yr) | \$357,714 | \$7,658 | 2.1% |

Even in the bear case, the debt shrinks to 10% of the portfolio in 5 years. In the bull case,
it's noise — 2.1%. **The fixed-dollar debt can't keep up with an appreciating asset.** Inflation
makes it worse (for the lender). Adoption makes it worse (for the lender). Time makes it worse
(for the lender).

You are on the right side of this trade.

---

## 6. The Government Is the Biggest Debtor

Here is the part that seals the argument.

The US government owes \$34+ trillion. It can never repay this in real terms. It doesn't intend
to. The *only* way to manage sovereign debt at this scale is inflation — slowly eroding the real
value of the debt while nominally "honoring" every obligation.

This is not conspiracy. It's arithmetic. It's also explicit policy:

- The Fed targets 2–3% inflation, not 0%. Why? Because 0% inflation would make government debt
  heavier every year.
- Quantitative easing (money printing) dilutes the dollar. Every dollar printed makes existing
  dollars — including the ones you owe — worth less.
- Interest rates are set by the Fed, not the market. The Fed has every incentive to keep real
  rates low or negative.

**When you borrow, you are aligned with the most powerful economic force on the planet:
sovereign monetary policy.**

The government *needs* inflation. It *creates* inflation. And inflation *benefits debtors*.
You, as a borrower, are riding the same wave as the US Treasury.

> The savers — the ones hoarding cash, paying off every loan, keeping money in savings accounts
> at 4% — are on the wrong side. They are lending to a system designed to erode the value of
> their loans.

---

## 7. The Saver's Trap

This is the cruel irony of conventional financial wisdom.

**"Save money. Pay off debt. Build an emergency fund. Put money in a savings account."**

Every piece of this advice pushes you to the *wrong side* of the inflation trade:

| Action | Inflation Effect | Who Benefits |
|:-------|:-----------------|:-------------|
| Save cash | Purchasing power erodes at 3%/yr | Erodes YOU |
| Pay off 6.5% mortgage | Lose inflation tailwind on debt | You lose the free erosion |
| Hold bonds | Fixed income eroded by inflation | Erodes YOU |
| Borrow at fixed rate | Debt eroded by inflation | Benefits YOU |
| Buy assets (house, stocks, crypto) | Assets appreciate with inflation | Benefits YOU |

The standard financial playbook — save and de-lever — is designed for a world without inflation.
We don't live in that world. We live in a world where the dollar loses 2–5% of its value every
year, by design, forever.

**Saving in dollars is a guaranteed losing trade.** Borrowing in dollars is a guaranteed winning
trade (in real terms, at reasonable rates). The difference is which side of inflation you're on.

### Why is this the standard advice?

Because it's *safe*. No one ever went bankrupt from saving too much. No one ever got liquidated
from having too little debt. The advice minimizes catastrophic downside — which is genuinely
valuable for people without financial literacy.

But for anyone who understands inflation, leverage, and risk management, the standard advice is
a wealth tax. You're paying 3% per year in lost purchasing power for the privilege of feeling
secure.

---

## 8. The Inflation Stack

Let's put the full picture together. When you hold debt against an appreciating asset, you benefit
from **three** compounding forces simultaneously:

### Force 1: The Spread

Your asset returns $\mu$ per year. Your debt costs $r$ per year. The spread $\mu - r$ compounds
in your favor. (This is the core argument from [The Mathematics of Debt](/blog/finance/debt_finance/).)

### Force 2: Inflation Erosion

Inflation $\pi$ erodes your debt at $\pi$% per year. Your real borrow rate is $r - \pi$, not $r$.
A 5% nominal rate at 3% inflation is only 2% real.

### Force 3: Wage/Income Growth

Your income grows at (at least) the inflation rate. Your debt payment stays fixed. The burden
shrinks every year as a percentage of your income.

**These three forces stack multiplicatively:**

$$\text{Wealth creation rate} = \underbrace{(\mu - r)}_{\text{spread}} + \underbrace{\pi}_{\text{inflation erosion}} + \underbrace{g_{\text{income}}}_{\text{wage growth}}$$

Even if the spread is small (say, asset return barely beats borrow rate), inflation and wage growth
add another 3–5% per year of real debt erosion. The total benefit of carrying debt is far larger
than the spread alone suggests.

---

## 9. Why This Is Not Taught

This is the question that should make you angry.

Why doesn't school teach this? Why doesn't any standard personal finance book explain the
inflation mechanics of debt?

**Three reasons:**

**1. Complexity bias.** "Pay off debt" is one sentence. "Carry debt strategically while managing
leverage, monitoring real rates, and investing the freed capital in assets that outpace inflation"
is a paragraph. Media and education optimize for simplicity. The simple answer is wrong, but it
fits on a bumper sticker.

**2. Institutional incentives.** Banks want you to save (they lend out your deposits at higher
rates — you are subsidizing *their* leverage). Schools are funded by governments that benefit from
a docile, saving population. No institution has an incentive to teach you to think like a borrower.

**3. Survivorship bias in advice.** The people who give financial advice tend to be people who
*survived* financially. Many of them survived by being conservative — paying off debt, saving
aggressively. They attribute their success to conservatism, not to the bull market that lifted all
boats. They teach what worked *for them*, not what the math says is optimal.

The result: an entire population trained to be on the wrong side of the most important trade in
personal finance.

---

## 10. The One-Page Summary

| Principle | Implication |
|:----------|:------------|
| Inflation erodes the dollar at 2–5%/yr | Every dollar you owe gets lighter every year |
| Debt is fixed in nominal terms | \$6,000 today will feel like \$3,000 in 15 years |
| Assets appreciate with inflation | Your collateral grows; your debt doesn't |
| Wages grow with inflation | Debt payments shrink as % of income over time |
| Real borrow rate = nominal − inflation | A 5% loan at 3% inflation only costs 2% real |
| The government is the biggest debtor | Monetary policy is designed to benefit borrowers |
| Saving cash = lending to an inflating system | Savers subsidize borrowers — including the government |
| The standard advice ("pay off debt") | Optimizes for safety, not wealth. Fine for survival. Terrible for compounding. |

---

## 11. The Final Intuition

Close your eyes and imagine two futures:

**Future A:** You paid off all your debt in 2026. You saved diligently. You put money in a savings
account earning 4%. By 2046, you have a nice nest egg. But inflation ate 3% per year. Your real
return was 1%. In 20 years, your purchasing power barely moved.

**Future B:** You kept your debt. You let inflation erode it. You invested your freed capital in
assets that compound at 10–30% real. By 2046, your debt is a rounding error — the \$6,000 you
owed feels like \$3,000 in today's dollars. Your assets are worth 10–50× what they were. The
compounding curve went exponential while your debt flatlined.

**The gap between these two futures is not small. It is generational.**

The difference between middle class and wealthy is not income. It's not education. It's not luck.
It's understanding which side of inflation to be on.

Borrowers inherit the future. Savers subsidize it.

---

## Related

- [The Mathematics of Debt](/blog/finance/debt_finance/) — the Kelly criterion framework
- [The Perpetual Debt Playbook](/blog/finance/perpetual_debt/) — managing no-maturity DeFi loans
- [Why Keeping Debt Feels Wrong But Is Right](/blog/finance/debt_intuition/) — five mental models
