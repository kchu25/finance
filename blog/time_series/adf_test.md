@def title = "Understanding Stationarity: ADF Test and Autocorrelation"
@def published = "20 October 2025"
@def tags = ["time-series"]

# Understanding Stationarity: ADF Test and Autocorrelation

Hey! Let's break down these concepts in a way that actually makes sense.

## What's the Big Picture?

When you're working with time series data, you need to know if your data is **stationary** - basically, does it have stable statistical properties over time, or is it wandering around? This matters because many statistical models assume stationarity.

## The Augmented Dickey-Fuller (ADF) Test

The ADF test is like a detective that checks if your time series has a "unit root" - which is a fancy way of saying "does this data have a tendency to wander off and not come back?"

### How It Works

The ADF test runs a regression that looks something like this:

$\Delta x_t = \alpha + \beta t + \gamma x_{t-1} + \sum_{i=1}^{p} \delta_i \Delta x_{t-i} + \epsilon_t$

Where:
- $\Delta x_t = x_t - x_{t-1}$ (the change from one period to the next)
- $\gamma$ is the key parameter we care about
- The sum term handles autocorrelation at different lags

**Yes, ALL of these are estimated!** It's just a regular OLS regression. Let me break down what each parameter does:

### The Parameters Explained

**$\alpha$ (intercept/drift)**: 
- This is just a constant term
- Captures whether there's a general upward/downward drift in the series
- Estimated like any regression intercept

**$\beta$ (trend coefficient)**:
- Multiplied by time $t$ (1, 2, 3, 4, ...)
- Captures whether there's a deterministic time trend
- You can actually choose to include this or not! More on this below.

**$\gamma$ (the star of the show)**:
- Coefficient on the lagged level $x_{t-1}$
- **This is what we're testing!**
- If $\gamma$ is significantly negative → mean reversion → stationary
- If $\gamma \approx 0$ → unit root → non-stationary

**$\delta_i$ (lagged difference terms)**:
- Coefficients on past changes $\Delta x_{t-1}, \Delta x_{t-2}$, etc.
- These "soak up" any serial correlation in the residuals
- Make sure your test results are valid
- There are $p$ of these (you choose $p$)

### How Do You Choose What to Include?

The ADF test actually has **three versions** depending on what you include:

1. **No constant, no trend**: $\Delta x_t = \gamma x_{t-1} + \sum \delta_i \Delta x_{t-i} + \epsilon_t$
2. **With constant, no trend**: $\Delta x_t = \alpha + \gamma x_{t-1} + \sum \delta_i \Delta x_{t-i} + \epsilon_t$
3. **With constant and trend**: $\Delta x_t = \alpha + \beta t + \gamma x_{t-1} + \sum \delta_i \Delta x_{t-i} + \epsilon_t$

You pick based on your data:
- Random walk with no drift? → Version 1
- Data oscillates around a constant? → Version 2
- Data has a clear time trend? → Version 3

### How Many Lags ($p$)?

You need to choose how many lagged differences to include. Common approaches:

**1. Information Criteria (most common)**:
- Try different values of $p$
- Pick the one that minimizes AIC or BIC
- Most software does this automatically

**2. Rule of thumb**:
- $p \approx 12 \times (T/100)^{1/4}$ where $T$ is your sample size
- For monthly data: $p \approx 12$
- For quarterly data: $p \approx 4$

**3. Ljung-Box test**:
- Keep adding lags until residuals show no autocorrelation

**The test checks**: Is $\gamma$ significantly negative?

- **If $\gamma < 0$ and significant**: Your series "wants" to return to some level → **stationary** ✓
- **If $\gamma \approx 0$**: Your series just wanders around → **non-stationary** (unit root) ✗

### Interpreting the Results

You'll get a test statistic and a p-value:
- **p-value < 0.05**: Reject the null hypothesis → series is stationary
- **p-value > 0.05**: Can't reject null → series likely has a unit root (non-stationary)

The null hypothesis is "there's a unit root" (non-stationary), so a low p-value is good news!

## Checking Autocorrelation of $(x_t - \bar{x})$

Now let's talk about your second question. You're looking at the **demeaned series** (subtracting the mean) and checking its autocorrelation.

### What Does "Negative at Lag 1" Mean?

The autocorrelation at lag 1 measures the correlation between:
- $(x_t - \bar{x})$ (today's deviation from mean) and 
- $(x_{t-1} - \bar{x})$ (yesterday's deviation from mean)

Let me break this down with a concrete example:

**Imagine a stock price that oscillates around \$100**:

| Time | Price $x_t$ | Deviation $(x_t - \bar{x})$ |
|------|-------------|------------------------------|
| 1    | \$95         | -\$5 (below average)          |
| 2    | \$105        | +\$5 (above average)          |
| 3    | \$98         | -\$2 (below average)          |
| 4    | \$102        | +\$2 (above average)          |
| 5    | \$99         | -\$1 (below average)          |

See the pattern? When it's above average at time $t$, it tends to be below average at time $t-1$ (and vice versa). The signs **alternate** - that's negative autocorrelation!

### What Negative Lag-1 Autocorrelation Tells You

**If autocorrelation at lag 1 is negative** (like -0.3):
- When today is above the mean → yesterday was likely below the mean
- When today is below the mean → yesterday was likely above the mean
- The series **overshoots and corrects** - it bounces around the mean
- This is **mean reversion** = hallmark of stationarity!

**If autocorrelation at lag 1 is positive** (like +0.7):
- When today is above the mean → yesterday was probably also above the mean
- When today is below the mean → yesterday was probably also below the mean
- The series has **persistence** - it stays on one side
- This suggests **non-stationarity** (like a random walk)

### Visual Intuition

Think of it like a ball:

**Negative autocorrelation (stationary)**:
- Ball on a spring attached to a wall
- Pull it right → it bounces back left
- Pull it left → it bounces back right
- Always returns to center (the mean)

**Positive autocorrelation (non-stationary)**:
- Ball rolling on a flat surface
- Push it right → it keeps going right
- No force pulling it back
- Can drift away indefinitely

### Why This Matters for Stationarity

A stationary series has a **stable mean** it orbits around. If you see negative lag-1 autocorrelation, it means:
- The series doesn't wander off
- It has a "home base" (the mean)
- Deviations are temporary and self-correcting

This is exactly what stationarity requires!

### Why Negative Lag-1 Suggests Stationarity

Think about it intuitively:

**Stationary process**: If you're above the mean today, you tend to drift back down tomorrow (negative autocorrelation). The series has a "home base" it returns to.

**Non-stationary process**: If you're high today, you tend to stay high tomorrow (positive autocorrelation). The series can wander off indefinitely.

### The Connection to ADF

The negative autocorrelation at lag 1 is actually related to what the ADF test checks! When the ADF finds $\gamma < 0$, it's detecting that same mean-reverting behavior.

## What Should You Actually Test?

### Here's the Deal with Stock Prices

You're absolutely right! Stock prices are almost **never stationary** - they wander around, trend up/down, and don't have a stable mean. This is called being **integrated of order 1**, or **I(1)**.

But here's the key insight: **their returns (differences) usually ARE stationary!**

### What to Test in Practice

**Test the raw series first**:
```julia
# Test the price level
adf_test = ADFTest(stock_prices, :constant, 1)
```

If it's non-stationary (high p-value), then test the differences:

```julia
# Test the returns (first difference)
returns = diff(stock_prices)  # This is Δx_t
adf_test = ADFTest(returns, :constant, 1)
```

### The Logic

The ADF test **already works on the original series** $x_t$. Remember the regression:

$\Delta x_t = \alpha + \gamma x_{t-1} + \sum_{i=1}^{p} \delta_i \Delta x_{t-i} + \epsilon_t$

The test creates the differences internally! You give it $x_t$ (the levels), and it:
1. Computes $\Delta x_t$ on the left side
2. Tests if $x_{t-1}$ has a significant negative coefficient

### So What Should You Do?

**Option 1 (Standard approach)**:
- Run ADF on the price levels $x_t$
- If non-stationary → differencing is needed
- Run ADF on returns $\Delta x_t$ to confirm they're stationary
- Use returns for modeling

**Option 2 (If you know it's I(1))**:
- Skip straight to testing returns
- Most financial time series are I(1), so this saves time

### Example: Stock Prices

```julia
using HypothesisTests, StatsBase

# Test price levels
prices = [100, 102, 101, 105, 108, ...]
adf_prices = ADFTest(prices, :constant, 1)
println("Prices p-value: ", pvalue(adf_prices))  # Usually > 0.05 (non-stationary)

# Test returns
returns = diff(log.(prices))  # Log returns
adf_returns = ADFTest(returns, :constant, 1)
println("Returns p-value: ", pvalue(adf_returns))  # Usually < 0.05 (stationary!)
```

> **Note on differencing**: When you compute returns with `diff()`, you lose one observation! If `prices` has $T$ observations, `returns` will have $T-1$ observations starting from the second time point. This is because $\Delta x_2 = x_2 - x_1$ is your first return (you can't compute a return for $x_1$ since there's no $x_0$). This is normal - just remember to align your dates/indices accordingly!

### Integration Order

- **I(0)**: Stationary as-is (rare for prices)
- **I(1)**: Stationary after 1st difference (most financial data)
- **I(2)**: Needs 2 differences (rare, usually a data problem)

**Bottom line**: Test the levels first to see if you need to difference. If ADF says non-stationary, difference once and test again!

**What to look for**:
- ADF p-value < 0.05 ✓
- Lag-1 autocorrelation is negative ✓
- Both suggest your series is stationary!

## Key Takeaway

Both tests are looking at the same fundamental question from different angles: **Does this series have a stable mean it returns to?**

- **ADF**: Formal statistical test
- **Negative lag-1 autocorrelation**: Quick visual/numeric check

If you see both, you're in good shape for modeling!