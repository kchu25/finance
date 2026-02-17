@def title = "Mathematical Description of Jump Detection Algorithm"
@def published = "15 November 2025"
@def tags = ["quant", "trading"]

# Mathematical Description of Jump Detection Algorithm

## Overview
This algorithm detects significant price jumps in time series data using magnitude-based thresholds and optional volume confirmation.

## Inputs
- $P = \{P_1, P_2, \ldots, P_n\}$: Price series
- $V = \{V_1, V_2, \ldots, V_n\}$: Volume series (optional)
- $\tau$: Threshold percentage (default: 2.0%)
- $\nu$: Volume threshold multiplier (default: 1.5)
- $w$: Window size for moving average (default: 20)

```julia
function detect_jumps_magnitude(prices, volumes=nothing; 
                                threshold_pct=2.0, 
                                volume_threshold=1.5, 
                                window_size=20)
```

## Hyperparameters

The algorithm has **three key hyperparameters** that control jump detection sensitivity:

| Hyperparameter | Symbol | Default | Description | Effect of Increasing |
|----------------|--------|---------|-------------|---------------------|
| **Threshold percentage** | $\tau$ | 2.0% | Minimum absolute return to qualify as a jump candidate | Fewer, larger jumps detected (less sensitive) |
| **Volume threshold** | $\nu$ | 1.5 | Minimum ratio of current volume to moving average | Fewer jumps confirmed (stricter volume requirement) |
| **Window size** | $w$ | 20 | Lookback period for volume moving average | Smoother volume baseline (less sensitive to recent spikes) |

### Tuning Guidelines

**Threshold percentage ($\tau$):**
- **Lower values (0.5-1%)**: Detects many small movements; useful for high-frequency trading or volatile assets
- **Medium values (2-3%)**: Balanced; catches significant moves while avoiding noise
- **Higher values (5%+)**: Only extreme events; useful for daily/weekly data or detecting major shocks

**Volume threshold ($\nu$):**
- **Lower values (1.2-1.3)**: More lenient; confirms jumps with modest volume increases
- **Medium values (1.5-2.0)**: Standard; requires noticeable volume spike
- **Higher values (2.5+)**: Strict; only confirms jumps with exceptional volume

**Window size ($w$):**
- See the note below on choosing appropriate window sizes for your data frequency
- Longer windows → more stable baseline but slower adaptation to regime changes
- Shorter windows → more responsive but may generate false positives during volatile periods

### Hyperparameter Interactions

These parameters work together:
- **Loose price threshold + strict volume threshold**: Catches many price moves but only confirms those with strong volume (conservative)
- **Strict price threshold + loose volume threshold**: Only looks at large moves, confirms most of them (aggressive on big moves)
- **Both strict**: Very high precision, low recall (few but high-quality jump signals)
- **Both loose**: High recall, lower precision (many jump signals, some false positives)

## Step 1: Calculate Percentage Returns

For each time $t = 2, 3, \ldots, n$:

$$r_t = \frac{P_t - P_{t-1}}{P_{t-1}} \times 100$$

This produces the returns series $R = \{r_2, r_3, \ldots, r_n\}$.

**Code:**
```julia
returns = @views diff(prices) ./ prices[1:end-1] * 100
```

**Explanation:**
- `diff(prices)` computes $P_t - P_{t-1}$ for all $t$
- `prices[1:end-1]` gives $P_{t-1}$
- Division and multiplication by 100 gives percentage returns

---

## Step 2: Identify Jump Candidates

Jump candidates are identified as times where the absolute return exceeds the threshold:

$$\mathcal{J}_{\text{candidates}} = \{t : |r_t| > \tau\}$$

**Code:**
```julia
jump_candidates = findall(x -> abs(x) > threshold_pct, returns) .+ 1
```

**Explanation:**
- `findall(x -> abs(x) > threshold_pct, returns)` finds indices where $|r_t| > \tau$
- `.+ 1` adjusts indices because `returns` is one element shorter than `prices`
- Maps return indices back to price indices

---

## Step 3: Volume Confirmation (Optional)

If volume data is provided:

**Code:**
```julia
if volumes !== nothing && length(volumes) == length(prices)
```

### 3a. Volume Moving Average

For each time $t = w+1, w+2, \ldots, n$:

$$\overline{V}_t = \frac{1}{w} \sum_{i=t-w}^{t} V_i$$

**Code:**
```julia
vol_ma = @views [mean(volumes[max(1,i-window_size):i]) 
                 for i in (window_size+1):length(volumes)]
```

**Explanation:**
- For each index `i` from `window_size+1` to `n`
- `volumes[max(1,i-window_size):i]` extracts the window $[V_{i-w}, \ldots, V_i]$
- `mean(...)` computes $\overline{V}_i$
- `max(1,...)` handles edge cases at the start of the series

---

### 3b. Volume Spike Detection

Volume spikes occur when current volume exceeds the moving average by the volume threshold:

$$\mathcal{S}_{\text{volume}} = \left\{t : \frac{V_t}{\overline{V}_t} > \nu, \quad t \geq w+1\right\}$$

**Code:**
```julia
volume_spikes = @views findall(x -> x > volume_threshold, 
                               volumes[(window_size+1):end] ./ vol_ma) .+ window_size
```

**Explanation:**
- `volumes[(window_size+1):end]` gets $V_t$ for $t \geq w+1$
- `./ vol_ma` computes the ratio $\frac{V_t}{\overline{V}_t}$
- `findall(x -> x > volume_threshold, ...)` finds where ratio $> \nu$
- `.+ window_size` adjusts indices back to the original price series

---

### 3c. Confirmed Jumps

Jumps are confirmed when both magnitude and volume criteria are satisfied:

$$\mathcal{J}_{\text{confirmed}} = \mathcal{J}_{\text{candidates}} \cap \mathcal{S}_{\text{volume}}$$

**Code:**
```julia
jump_indices = intersect(jump_candidates, volume_spikes)
return jump_indices, returns, volume_spikes
```

**Explanation:**
- `intersect(...)` finds common elements between the two sets
- Returns confirmed jumps, all returns, and volume spikes

---

**When volume is not provided:**
```julia
else
    return jump_candidates, returns, Int[]
end
```
Returns all jump candidates without volume confirmation, and an empty array for volume spikes.

---

## Output

The algorithm returns:
1. **Jump indices**: $\mathcal{J}_{\text{confirmed}}$ (if volume provided) or $\mathcal{J}_{\text{candidates}}$ (otherwise)
2. **Returns series**: $R = \{r_2, r_3, \ldots, r_n\}$
3. **Volume spike indices**: $\mathcal{S}_{\text{volume}}$ (if volume provided, empty otherwise)

## Interpretation

- A **jump** is a sudden, significant price movement detected when $|r_t| > \tau$
- **Volume confirmation** strengthens jump detection by requiring abnormally high trading activity
- The moving average window $w$ provides context for what constitutes "abnormal" volume
- The algorithm is symmetric: it detects both upward jumps (positive $r_t$) and downward jumps (negative $r_t$)

> **Note on Window Size for Minute-by-Minute Data:**
> 
> If your data is **minute-by-minute**, the default `window_size=20` means looking back only **20 minutes**, which may be too short to establish a reliable baseline for "normal" volume.
> 
> **Recommended window sizes for intraday minute data:**
> - `window_size = 60` (1 hour): Good for detecting unusual activity relative to recent intraday patterns
> - `window_size = 120` (2 hours): More stable baseline, less sensitive to very recent fluctuations  
> - `window_size = 390` (full trading day): Compares against today's typical volume
> - `window_size = 1950` (~5 days): Multi-day context for more stable comparison
> 
> **Why this matters:** Intraday volume has natural patterns (high at open/close, low at midday). A 20-minute window might flag normal afternoon volume as "spikes" if calculated during a quiet midday period. Longer windows smooth out these intraday variations.

> **Connection to Exit Strategies: "Taking profit now is at least as good as waiting"**
>
> This intuition comes from optimal stopping theory in mean-reverting systems. Imagine you're holding a profitable position:
> 
> **The comparison:**
> - **Left side** (exit now): Lock in your current profit with certainty
> - **Right side** (wait): Expected profit from waiting minus the costs of holding (fees, slippage, opportunity cost)
>
> **Three scenarios:**
> 1. **Far from equilibrium** (stock oversold/overbought): Mean reversion will likely push prices further in your favor → expected future profit > current profit → **keep holding**
> 2. **Near equilibrium** (stock at fair value): Mean reversion pull is weak → expected future profit ≈ current profit → **exit now** (why pay holding costs for minimal expected gain?)
> 3. **Adverse conditions**: Mean reversion suggests things will get worse → expected future profit < current profit → **exit immediately**
>
> **Why this is powerful:** The decision is **automatic and data-driven**. The parameter $\theta$ (reversion speed) captures how strongly prices pull back to equilibrium:
> - Large $\theta$ → Strong reversion → Stay in positions longer (prices snap back fast)
> - Small $\theta$ → Weak reversion → Exit earlier (prices drift slowly)
> 
> You don't need to manually judge "is this far enough from fair value?" — $\theta$ quantifies exactly how much edge you have at each price level. The exit rule becomes mechanical: calculate expected profit, compare to current profit minus costs, done.
>
> **CRITICAL: What if θ is negative?**
> 
> If your regression estimates $\theta < 0$ (so $\kappa < 0$ in the OU process), **the stock is NOT mean-reverting — it's trending/explosive!**
> 
> Consider the drift term $\theta(\mu - X_t)$:
> - When $X_t < \mu$ (below average): If $\theta > 0$, drift pushes UP toward $\mu$ ✓ (mean reversion)
> - When $X_t < \mu$ (below average): If $\theta < 0$, drift pushes DOWN away from $\mu$ ✗ (explosive)
> 
> **What negative θ means:** Deviations from the mean get amplified, not corrected. The price trends away from equilibrium rather than reverting to it.
> 
> **What to do:** The optimal stopping framework doesn't apply! You need a **trend-following strategy** instead of mean reversion. This is actually valuable information — it tells you the market regime has changed and you should trade accordingly (or stay out).
>
> **Jump detection tie-in:** Detecting jumps helps you identify when prices have moved far from equilibrium (scenario 1), potentially signaling entry points for mean-reversion strategies, or exit points when jumps break the mean-reverting regime entirely (regime shift to trending behavior).

## Alternative Approaches

While the magnitude-based approach above is practical and interpretable, more sophisticated methods exist:

### Statistical Jump Detection

**Lee-Mykland (2008) Test**: Uses local volatility estimation
$$L_t = \frac{r_t}{\hat{\sigma}_t}$$
where $\hat{\sigma}_t$ is a robust volatility estimate (e.g., bipower variation). Jumps detected when $|L_t|$ exceeds a critical value from extreme value theory.

**Advantages**: Adapts to changing volatility, statistical foundation  
**Disadvantages**: More complex, requires careful parameter selection

### Barndorff-Nielsen-Shephard (2006)

Separates continuous and jump components using realized variance and bipower variation:
$$\text{Jump Component}_t = \text{RV}_t - \text{BV}_t$$
where BV is less sensitive to jumps than RV.

### GARCH-Jump Models

Models volatility dynamics explicitly:
$$r_t = \mu + \sigma_t \epsilon_t + J_t$$
where $\sigma_t^2$ follows GARCH dynamics and $J_t$ is a jump process.

**Advantages**: Captures volatility clustering, probabilistic jump identification  
**Disadvantages**: Computationally intensive, requires estimation

### When Simple is Better

The magnitude + volume approach is preferred when:
- Interpretability matters (explaining to stakeholders)
- Real-time detection is needed (low computational cost)
- Data is noisy or limited
- You want actionable, clear signals

More sophisticated methods are better when:
- You need statistical inference about jump properties
- Working with high-frequency data
- Volatility varies significantly over time
- Academic rigor is required