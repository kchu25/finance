@def title = "X LINK Bought with Other People's Money: The Compounding Race"
@def published = "15 February 2026"
@def tags = ["defi", "chainlink", "quant"]

# X LINK Bought with Other People's Money
## How Borrowed LINK Outpaces USDC Debt — and Why the Gap Only Widens

@@toc@@

---

## 1. The Trade

I borrowed \$22,000 USDC from Aave at 3.8% APR. With that capital, I acquired approximately
**X additional LINK** at \$9.14/token.

That's X LINK I didn't pay for with my own money. I used *someone else's* capital — Aave
liquidity providers — to buy a finite-supply asset that I believe will appreciate at 10–50%
per year.

This post answers one question: **does the borrowed LINK outpace the USDC debt?**

Spoiler: it's not even close.

---

## 2. The Two Growth Rates

This trade is a race between two compounding curves:

**Curve 1: The debt.** \$22,000 USDC growing at 3.8% per year (the borrow rate). This is what
I owe. It grows slowly, linearly-ish, predictably.

**Curve 2: The LINK.** X LINK appreciating at some annual rate. This is what I own. It
grows exponentially, unpredictably, but historically *fast*.

The question is whether Curve 2 outruns Curve 1. Let's find out.

### Debt growth: slow and predictable

| Year | Debt | Interest Accrued |
|:----:|:----:|:----------------:|
| 0 | \$22,000 | \$0 |
| 1 | \$22,836 | \$836 |
| 3 | \$24,605 | \$2,605 |
| 5 | \$26,510 | \$4,510 |
| 10 | \$31,945 | \$9,945 |
| 15 | \$38,493 | \$16,493 |
| 20 | \$46,384 | \$24,384 |
| 25 | \$55,893 | \$33,893 |

After 25 years, the debt has grown from \$22,000 to \$55,893. That's 2.5× — a crawl.

### LINK growth: fast and exponential

Here's where it gets interesting. Let's model the X LINK at four different annual growth
rates:

**Conservative (10%/yr) — "Crypto winter forever":**

| Year | LINK Price | X LINK Value | Debt | Net Gain | Ratio |
|:----:|:---------:|:----------------:|:----:|:--------:|:-----:|
| 1 | \$10.05 | \$24,130 | \$22,836 | \$1,294 | 1.1× |
| 5 | \$14.72 | \$35,328 | \$26,510 | \$8,818 | 1.3× |
| 10 | \$23.71 | \$56,896 | \$31,945 | \$24,952 | 1.8× |
| 15 | \$38.18 | \$91,632 | \$38,493 | \$53,139 | 2.4× |
| 25 | \$99.03 | \$237,670 | \$55,893 | \$181,777 | 4.3× |

Even in the *worst* case — LINK only growing at 10%/yr for 25 years — the borrowed LINK is
worth **4.3× the debt**. Net gain: \$181,777 on a \$22,000 borrow. That's an 826% return on
capital I never had.

**Base case (25%/yr) — "Chainlink becomes standard infrastructure":**

| Year | LINK Price | X LINK Value | Debt | Net Gain | Ratio |
|:----:|:---------:|:----------------:|:----:|:--------:|:-----:|
| 1 | \$11.43 | \$27,420 | \$22,836 | \$4,584 | 1.2× |
| 5 | \$27.89 | \$66,943 | \$26,510 | \$40,433 | 2.5× |
| 10 | \$85.12 | \$204,295 | \$31,945 | \$172,350 | 6.4× |
| 15 | \$259.77 | \$623,459 | \$38,493 | \$584,966 | 16.2× |
| 25 | \$2,419 | \$5,806,411 | \$55,893 | \$5,750,518 | 103.9× |

At 25%/yr, the X LINK are worth **104× the debt** by year 25. The \$22,000 borrowed becomes
\$5.75 million in net value. The debt (\$55,893) is a rounding error.

**Bull case (50%/yr) — "Crypto goes mainstream":**

| Year | LINK Price | X LINK Value | Debt | Net Gain | Ratio |
|:----:|:---------:|:----------------:|:----:|:--------:|:-----:|
| 1 | \$13.71 | \$32,904 | \$22,836 | \$10,068 | 1.4× |
| 5 | \$69.41 | \$166,576 | \$26,510 | \$140,067 | 6.3× |
| 10 | \$527.06 | \$1,264,940 | \$31,945 | \$1,232,996 | 39.6× |

The numbers get absurd fast. The debt can't keep up. It *never* keeps up.

---

## 3. The Breakeven Bar Is on the Floor

Here's the punchline. For this trade to break even — for the LINK to merely *equal* the debt —
LINK needs to appreciate at:

| Time Horizon | Breakeven Growth Rate |
|:------------:|:---------------------:|
| 1 year | 4.10%/yr |
| 3 years | 3.90%/yr |
| 5 years | 3.86%/yr |
| 10 years | 3.83%/yr |
| 25 years | 3.81%/yr |

**LINK needs to grow at just 3.83% per year to beat the debt.**

That's less than the S&P 500 average return (10%). Less than inflation (3%). Less than the
yield on a savings account (4%).

Chainlink's historical CAGR is 30–80%. The breakeven bar is so low it's underground.

> The trade loses money *only* if LINK appreciates at less than 3.83% per year for 25 years
> straight. That means Chainlink — the dominant oracle network powering DeFi, CCIP, and
> tokenized assets — grows slower than a savings account. For a quarter century.

If you believe that scenario, you shouldn't own LINK at all. If you own LINK, you've already
implicitly accepted that it will outperform 3.83%/yr. And if it does, the borrow was free money.

---

## 4. Why the Debt Can Never Catch Up

This isn't luck or timing. It's structural. The debt *cannot* outpace the asset because of a
fundamental mathematical asymmetry:

### The debt grows linearly-ish

At 3.8% APR, the debt doubles every ~18.4 years:

$$t_{\text{double}} = \frac{\ln 2}{\ln 1.038} = 18.6 \text{ years}$$

That's glacial. One doubling in nearly two decades.

### The asset grows exponentially

At 25% CAGR, LINK doubles every ~3.1 years:

$$t_{\text{double}} = \frac{\ln 2}{\ln 1.25} = 3.1 \text{ years}$$

At 10% CAGR (bear case), LINK doubles every ~7.3 years — still 2.5× faster than the debt.

### The gap formula

The ratio of LINK value to debt value at time $t$:

$$\text{Ratio}(t) = \frac{V_{\text{LINK}}(t)}{D(t)} = \frac{2400 \times 9.14 \times (1 + g)^t}{22000 \times (1.038)^t} = 0.997 \times \bigg(\frac{1 + g}{1.038}\bigg)^t$$

where $g$ is LINK's annual growth rate.

As long as $g > 0.038$ (3.8%), the ratio grows exponentially. The gap *widens* every year.
It doesn't converge. It doesn't stabilize. It diverges — forever.

This is the core insight: **the spread between asset growth and debt growth compounds.** A small
annual difference becomes an enormous gap over time. At 25% LINK growth:

- Year 1: LINK is 1.2× the debt (barely ahead)
- Year 5: LINK is 2.5× the debt (pulling away)
- Year 10: LINK is 6.4× the debt (dominant)
- Year 15: LINK is 16.2× the debt (debt is noise)
- Year 25: LINK is 103.9× the debt (debt is a rounding error)

**The debt never catches up because it's running at 3.8% against a 25% headwind.** It's like a
bicycle racing a car. The bicycle starts at the same place, but every year the car pulls further
ahead.

---

## 5. The Effective Cost Per LINK

Another way to see this: what does each borrowed LINK *actually* cost, including all accumulated
interest?

| Year | Total Debt | Cost Per LINK |
|:----:|:----------:|:-------------:|
| 0 | \$22,000 | \$9.17 |
| 1 | \$22,836 | \$9.52 |
| 3 | \$24,605 | \$10.25 |
| 5 | \$26,510 | \$11.05 |
| 10 | \$31,945 | \$13.31 |
| 15 | \$38,493 | \$16.04 |
| 20 | \$46,384 | \$19.33 |
| 25 | \$55,893 | \$23.29 |

Even after **25 years** of compounding interest, each LINK cost me \$23.29.

If LINK is \$50 by then, I paid \$23.29 for a \$50 asset. If LINK is \$100, I paid \$23.29 for a
\$100 asset. If LINK is \$500 (not unreasonable over 25 years), I paid \$23.29 for a \$500 asset.

**The interest is a rounding error on the appreciation.** Even at 10%/yr (bear case), LINK
reaches \$99 by year 25. My all-in cost per token: \$23.29. The profit per token: \$75.71.

---

## 6. The 9.2% You'd Never Have

These X LINK represent **9.2% of my total 26,000 LINK stack.** This 9.2% was acquired
entirely with other people's money.

What is 9.2% of your stack worth at various LINK prices?

| LINK Price | X LINK Value | Context |
|:----------:|:----------------:|:--------|
| \$20 | \$48,000 | A car |
| \$50 | \$120,000 | A house down payment |
| \$100 | \$240,000 | A house |
| \$200 | \$480,000 | Early retirement supplement |
| \$500 | \$1,200,000 | Retirement |

Every single dollar of this was created from borrowed capital. You didn't earn it. You didn't
save it. You *leveraged* it into existence using the spread between borrow rate and asset
appreciation.

This is the [magic seed](/blog/finance/debt_intuition/#mental_model_1_the_magic_seed) from
the intuition post, made real.

---

## 7. The Opportunity Cost of Not Borrowing

The flip side: what if you *hadn't* borrowed? What would you have missed?

**Conservative (10%/yr):**

| Year | Net Value You Would Have Missed |
|:----:|:-------------------------------:|
| 5 | \$8,818 |
| 10 | \$24,952 |
| 15 | \$53,139 |
| 20 | \$101,190 |
| 25 | \$181,777 |

**Base case (25%/yr):**

| Year | Net Value You Would Have Missed |
|:----:|:-------------------------------:|
| 5 | \$40,433 |
| 10 | \$172,350 |
| 15 | \$584,966 |
| 20 | \$1,856,261 |
| 25 | \$5,750,518 |

In the base case, not borrowing would have cost you **\$5.75 million** over 25 years. That's
the opportunity cost of being debt-free. That's what "financial prudence" actually costs when
your asset outperforms your borrow rate.

The standard advice — "don't borrow to invest" — would have cost you millions. Not hypothetically.
Not theoretically. In *this specific position*, with *these specific numbers*.

---

## 8. Why This Only Works with the Right Asset

A critical caveat: this analysis works because LINK has specific properties that make it a
suitable collateral asset for leveraged compounding:

### 1. Finite supply

LINK has a hard cap of 1 billion tokens. Unlike dollars (which the Fed prints), LINK cannot
be inflated away. Your X LINK will always be 0.00024% of all LINK that will ever exist.
The denominator is fixed; only the price can change.

### 2. Real utility

Chainlink isn't a meme. It's oracle infrastructure. CCIP. Data feeds. Proof of reserve.
Randomness (VRF). These are *essential services* for on-chain finance. As DeFi, tokenized
assets, and cross-chain communication grow, demand for LINK grows with it.

### 3. Survived multiple cycles

LINK has been through 2018 (ICO crash), 2020 (COVID crash), 2022 (Luna/FTX crash) and
recovered each time. It's not untested. The asset has a track record of resilience.

### 4. Not correlated with the debt

Your debt is in USDC (a dollar-pegged stablecoin). Your asset is LINK (a crypto asset).
These have different drivers. USDC debt grows at a fixed rate. LINK growth is driven by
adoption, not interest rates. The correlation between your cost (debt) and your return
(LINK appreciation) is near zero — which is exactly what you want in a leveraged position.

### What this wouldn't work with

- **Memecoins:** No utility, no floor, no recovery guarantee. Leverage on a meme is suicide.
- **Highly correlated assets:** Borrowing USD to buy a USD-pegged asset (e.g., yield farming
  stablecoins) has a tiny spread and no compounding upside.
- **Assets with no supply cap:** If the token can be infinitely minted, the supply dilutes
  your position. The growth rate may not outpace the borrow rate.

---

## 9. The Psychological Trap

Here's what makes this trade emotionally difficult:

**Day 1:** You borrow \$22,000 and buy X LINK. The LINK is worth \$21,936. The debt is
\$22,000. You're *underwater* by \$64. Your brain screams: "You just lost money borrowing
money to buy something worth less than what you borrowed."

**Day 365:** LINK is up 10%. Your LINK is worth \$24,130. Your debt is \$22,836. You're up
\$1,294. But it *feels* like nothing. The debt feels heavy. The gain feels fragile.

**Year 5:** LINK is up 25%/yr. Your LINK is worth \$66,943. Your debt is \$26,510. You're up
\$40,433. Now the debt feels small. But you remember the anxiety of year 1.

**Year 10:** Your LINK is worth \$204,295. Your debt is \$31,945. The debt is 15.6% of the
LINK value. It's noise. You wonder why you were ever worried.

The trap is that the first 1–2 years feel terrible. The spread is small, the debt feels real,
and the LINK appreciation hasn't had time to compound. **Most people give up during this
window.** They repay the debt, sell the LINK, and feel relieved — having forfeited hundreds
of thousands in future compounding.

The whole game is surviving years 1–3 emotionally. After that, the math takes over and the
debt becomes irrelevant.

---

## 10. The Bottom Line

| Metric | Value |
|:-------|:------|
| LINK acquired with borrowed capital | X tokens |
| Percentage of total stack | 9.2% |
| Borrow cost | 3.8% APR |
| Breakeven LINK growth rate | 3.83%/yr |
| Expected LINK growth rate | 10–50%/yr |
| Spread (excess return) | 6.2–46.2%/yr |

The spread between what LINK earns and what the debt costs **compounds exponentially** in your
favor. Every year, the gap widens. Every year, the debt becomes more irrelevant. Every year,
the X LINK — bought with other people's money — become worth more.

The debt can never catch up. It's mathematically impossible as long as LINK grows faster than
3.83% per year. And if you believe LINK will grow slower than a savings account for 25 years
straight, you shouldn't own it at all.

You own it. So act accordingly.

> These X LINK didn't cost you anything. They cost Aave's liquidity providers \$22,000.
> You're paying them \$2.29 per day for the privilege. And the LINK will be worth more than
> the total accumulated interest within the first year.

---

## Related

- [My Aave LINK Position](/blog/defi/aave_link_position/) — full position breakdown and stress test
- [The Mathematics of Debt](/blog/finance/debt_finance/) — Kelly criterion framework
- [The Perpetual Debt Playbook](/blog/finance/perpetual_debt/) — managing no-maturity DeFi loans
- [Inflation Is a Debt Eraser](/blog/finance/inflation_debt/) — why inflation favors borrowers
- [Why Keeping Debt Feels Wrong But Is Right](/blog/finance/debt_intuition/) — five mental models
