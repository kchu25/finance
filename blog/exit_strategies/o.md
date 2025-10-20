@def title = "Optimal Stopping: A Discrete Approach"
@def published = "20 October 2025"
@def tags = ["exit-strategy"]

# Optimal Stopping: A Discrete Approach

## Why Work in Log Space?

When trading stocks, a \$1 move means very different things for a \$10 stock versus a \$1000 stock. Log prices normalize this perfectly.

**The magic of logarithms:** If you buy at price $P_0$ and sell at $P_1$, your log return is:

$$\ln(P_1) - \ln(P_0) = \ln\left(\frac{P_1}{P_0}\right)$$

This is exactly your percentage return! A 10% gain gives $\ln(1.10) \approx 0.0953$, and a 10% loss gives $\ln(0.90) \approx -0.1054$. Notice these appear symmetric in regular space (both "10%"), but they're actually asymmetric everywhere—including log space! The real benefit of log space is that it captures the true asymmetry of compounding.

## Mean Reversion in Discrete Time

Think of mean reversion like a rubber band. When a stock's log price $x_t$ drifts away from its long-run average $\mu$, there's a pull bringing it back.

> **Mean reversion**: The tendency for prices to return to their historical average over time. Like gravity for stock prices.

In discrete time steps (say, every minute or every hour), the log price updates like this:

$$x_{t+1} = x_t + \theta(\mu - x_t)\Delta t + \sigma\sqrt{\Delta t} \cdot \varepsilon_t$$

Where:
- $x_t = \ln(P_t)$ is the log price at time $t$ (unitless, it's a logarithm)
- $\theta$ = reversion speed (units: $\text{time}^{-1}$, e.g., "per hour")
- $\mu$ = long-run log price average (unitless)
- $\sigma$ = volatility (units: $\text{time}^{-1/2}$, e.g., "per $\sqrt{\text{hour}}$")
- $\Delta t$ = time step size (e.g., 0.1 hours = 6 minutes)
- $\varepsilon_t \sim N(0,1)$ = random shock (unitless)

> **Units and interpretation**: All time must be in the same units! If $\theta = 2.0$ per hour and $\sigma = 0.15$ per $\sqrt{\text{hour}}$, then $\Delta t$ must be in hours (not minutes). 
>
> **What does $\theta = 2.0$ mean?** The "half-life" of deviations is $\ln(2)/\theta \approx 0.35$ hours (~20 minutes). After 20 minutes, half of any price deviation from $\mu$ gets corrected. Larger $\theta$ means faster snap-back.
>
> **Why the weird units?** $\theta \cdot \Delta t$ needs to be unitless (it's multiplied by the unitless quantity $\mu - x_t$). Similarly, $\sigma\sqrt{\Delta t}$ must be unitless to match log price changes.

> **Ornstein-Uhlenbeck (OU) process**: A fancy name for mean-reverting random walk. The continuous version of what we're showing here.

**Key insight:** The drift term $\theta(\mu - x_t)\Delta t$ is positive when $x_t < \mu$ (below average → pushes up) and negative when $x_t > \mu$ (above average → pushes down).

## The Decision Rule

You entered a trade at log price $x_{\text{entry}}$. Now at time $t$, you're at $x_t$. Should you exit?

**Current profit:**
$$\text{Profit}_{\text{now}} = x_t - x_{\text{entry}}$$

**Expected profit if you wait one more time step:**

First, compute the expected log price:
$$\mathbb{E}[x_{t+1} | x_t] = x_t + \theta(\mu - x_t)\Delta t$$

> **Why is this the expectation?** Let's go slow. Starting from our update rule:
> $$x_{t+1} = x_t + \theta(\mu - x_t)\Delta t + \sigma\sqrt{\Delta t} \cdot \varepsilon_t$$
> 
> We want to find: "What do I expect $x_{t+1}$ to be, given that I know $x_t$ right now?"
> 
> **Step 1:** Take the conditional expectation of both sides (conditioning on knowing $x_t$):
> $$\mathbb{E}[x_{t+1} | x_t] = \mathbb{E}\left[x_t + \theta(\mu - x_t)\Delta t + \sigma\sqrt{\Delta t} \cdot \varepsilon_t \,\big|\, x_t\right]$$
> 
> **Step 2:** Split up the expectation (linearity):
> $$\mathbb{E}[x_{t+1} | x_t] = \mathbb{E}[x_t | x_t] + \mathbb{E}[\theta(\mu - x_t)\Delta t | x_t] + \mathbb{E}[\sigma\sqrt{\Delta t} \cdot \varepsilon_t | x_t]$$
> 
> **Step 3:** Simplify each term:
> - $\mathbb{E}[x_t | x_t] = x_t$ (if I know $x_t$, its expected value is just itself)
> - $\mathbb{E}[\theta(\mu - x_t)\Delta t | x_t] = \theta(\mu - x_t)\Delta t$ (everything here is known/deterministic given $x_t$)
> - $\mathbb{E}[\sigma\sqrt{\Delta t} \cdot \varepsilon_t | x_t] = \sigma\sqrt{\Delta t} \cdot \mathbb{E}[\varepsilon_t | x_t] = \sigma\sqrt{\Delta t} \cdot 0 = 0$
>
> (The last one is zero because $\varepsilon_t$ is independent of $x_t$ and has mean zero)
> 
> **Step 4:** Put it together:
> $$\mathbb{E}[x_{t+1} | x_t] = x_t + \theta(\mu - x_t)\Delta t$$
> 
> **Intuition:** On average, the random shocks cancel out. Only the deterministic drift (mean reversion pull) remains.

Then the expected profit is:
$$\text{Profit}_{\text{expected}} = \mathbb{E}[x_{t+1} | x_t] - x_{\text{entry}}$$

**Exit rule:**
$$\text{Exit if: } x_t - x_{\text{entry}} \geq \mathbb{E}[x_{t+1} | x_t] - x_{\text{entry}} - c$$

Where $c$ is your holding cost (trading fees, slippage, opportunity cost).

Simplifying:
$$\text{Exit if: } x_t \geq x_t + \theta(\mu - x_t)\Delta t - c$$
$$\text{Exit if: } 0 \geq \theta(\mu - x_t)\Delta t - c$$
$$\text{Exit if: } \theta(\mu - x_t)\Delta t \leq c$$

**Translation:** Exit when the expected mean reversion pull is smaller than your holding costs.

## Estimating Parameters from Historical Data

In practice, you don't know $\mu$ and $\theta$ in advance—you need to estimate them from past prices.

**The approach:** Use regression on historical log price changes. If you have log prices $x_0, x_1, x_2, \ldots, x_n$ at equal time intervals $\Delta t$, then:

$$x_{t+1} - x_t = \theta(\mu - x_t)\Delta t + \text{noise}$$

Rearranging:
$$x_{t+1} - x_t = \theta\mu\Delta t - \theta\Delta t \cdot x_t + \text{noise}$$

This is just linear regression! Let $y_t = x_{t+1} - x_t$ (the log price change) and run:

$$y_t = \beta_0 + \beta_1 x_t + \text{error}$$

From the regression coefficients:
- $\theta = -\beta_1 / \Delta t$
- $\mu = -\beta_0 / \beta_1$
- $\sigma = \text{std(residuals)} / \sqrt{\Delta t}$

> **How much history?** More is better, but too much includes irrelevant regimes. A common choice: 20-60 days of minute-by-minute or hourly data for intraday trading. The tradeoff is between statistical precision (needs more data) and stationarity (parameters change over time).

> **The workflow with minute-by-minute data:** 
> 
> **Step 1:** Collect your minute-by-minute log prices: $x_0, x_1, x_2, \ldots, x_n$
> 
> **Step 2:** Run the regression:
> - Compute changes: $y_t = x_{t+1} - x_t$ (log price change from minute $t$ to $t+1$)
> - Regress: $y_t = \beta_0 + \beta_1 x_t + \text{error}$
> - Get coefficients: $\beta_0$ and $\beta_1$
> 
> **Step 3:** Convert to parameters. Now you **choose** your preferred time units:
> 
> **Option A - Work in hours** (most common):
> - Set $\Delta t = 1/60$ hours (your data points are 1 minute = 1/60 hour apart)
> - Calculate: $\theta = -\beta_1 / (1/60) = -60\beta_1$ per hour
> - Calculate: $\mu = -\beta_0 / \beta_1$ (unitless, same either way)
> - Calculate: $\sigma = \text{std(residuals)} / \sqrt{1/60}$ per $\sqrt{\text{hour}}$
> 
> **Option B - Work in minutes:**
> - Set $\Delta t = 1$ minute (your data points are 1 minute apart)
> - Calculate: $\theta = -\beta_1 / 1 = -\beta_1$ per minute
> - Calculate: $\mu = -\beta_0 / \beta_1$ (same)
> - Calculate: $\sigma = \text{std(residuals)} / 1$ per $\sqrt{\text{minute}}$
> 
> Both give identical predictions! Example: if regression gives $\beta_1 = -0.0333$, then $\theta = 2.0$ per hour is the same as $\theta = 0.0333$ per minute. Most people prefer hours because $\theta = 2.0$ per hour is easier to interpret than $\theta = 0.0333$ per minute.

> **The big assumption:** You're assuming the mean-reverting dynamics you observed historically will continue today. If the market regime has changed (news, volatility spike, trend), your parameters could be wrong. This is the fundamental challenge of all statistical trading!

**Quick sanity checks:**
- $\theta > 0$? (Must be positive for mean reversion)
- $\mu$ near recent average log price? (If wildly different, model may not fit)
- $\sigma$ reasonable? (Compare to historical volatility measures)

## A Concrete Example

You're trading a stock that normally sits at $\mu = 4.605$ (about $\$100$). It's currently oversold at $x_t = 4.50$ (about $\$90$).

**Parameters:**
- Mean reversion speed: $\theta = 2.0$ per hour
- Volatility: $\sigma = 0.15$ per hour
- Time step: $\Delta t = 0.1$ hours (6 minutes)
- Holding cost: $c = 0.001$ (0.1%)

**Expected log price in 6 minutes:**
$$\mathbb{E}[x_{t+1}] = 4.50 + 2.0 \times (4.605 - 4.50) \times 0.1 = 4.521$$

In dollar terms: $e^{4.521} \approx \$91.90$

**Your decision:** 
- Current profit: $4.50 - 4.50 = 0$ log points
- Expected profit: $4.521 - 4.50 = 0.021$ log points ≈ 2.1%
- Since $0.021 > 0.001$, **keep holding!** The expected gain exceeds holding costs.

## Why Log Space Matters for Stops and Targets

Many traders set symmetric percentage stops in price space. This is a mistake!

**Example:** Stock at \$100, trader sets:
- Target: \$110 (+10%)
- Stop: \$90 (−10%)

In log space:
- Target: $\ln(110) - \ln(100) = 0.0953$
- Stop: $\ln(90) - \ln(100) = -0.1054$

**Asymmetric!** You're risking 10.54% to gain 9.53%.

**Corrected symmetric setup in log space:**
- Target: $\ln(100) + 0.10 = 4.705$ → $\$110.52$
- Stop: $\ln(100) - 0.10 = 4.505$ → $\$90.48$

Now risk/reward is truly balanced.

## The Big Picture

Optimal stopping with log prices gives you:

1. **Normalization**: A 1% move is a 1% move, regardless of whether the stock is \$10 or \$1000
2. **Linear dynamics**: Mean reversion becomes a simple linear pull in log space
3. **Stable probabilities**: The chance of moving up 0.1 log points is the same everywhere
4. **Correct risk assessment**: Stops and targets are properly symmetric

The decision rule is beautifully simple: exit when the mean reversion pull becomes weaker than your costs.

---

## Further Notes

> **Kelly Criterion**: A formula for optimal bet sizing that maximizes log wealth. It naturally lives in log space too, which is why all these pieces fit together so nicely.

> **Scaled exits**: Even with optimal stopping, many traders benefit from scaling out of positions (exiting in chunks). This reduces variance in your returns, which compounds to better long-term growth.