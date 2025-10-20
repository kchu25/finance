@def title = "Optimal Stopping with Log Prices for Mean Reversion"
@def published = "12 October 2025"
@def tags = ["exit-strategy"]

# Optimal Stopping with Log Prices for Mean Reversion

## Why Log Prices?

**The Problem:** Raw prices don't normalize for price level. A \$1 move means different things for a \$10 stock vs a \$1000 stock.

**The Solution:** Work in log space where returns are additive and symmetric.

$$r_{\log} = \ln\left(\frac{P_t}{P_0}\right)$$

**Key Properties:**
- **Additive:** $\ln(P_t/P_0) = \ln P_t - \ln P_0$
- **Symmetric:** A 10\% gain and 10\% loss have equal magnitude in log space
- **Stationary:** Statistical properties don't depend on price level

## Mean Reversion in Log Space

Mean reversion is naturally modeled as an **Ornstein-Uhlenbeck (OU) process** in log prices:

$$d(\ln P_t) = \theta(\mu - \ln P_t)dt + \sigma dW_t$$

**Parameters:**
- $\theta$ = mean reversion speed (how fast it reverts)
- $\mu$ = long-run equilibrium level (log price)
- $\sigma$ = volatility
- $W_t$ = Brownian motion

**Intuition:** When $\ln P_t < \mu$ (price below average), the drift is positive and pulls it back up. When $\ln P_t > \mu$, drift is negative.

**Discrete-time approximation:**

$$\ln P_{t+\Delta t} = \ln P_t + \theta(\mu - \ln P_t)\Delta t + \sigma\sqrt{\Delta t} \cdot \epsilon$$

where $\epsilon \sim N(0,1)$.

## Optimal Stopping in Log Space

The value function becomes:

$$V(\ln P_t) = \max\left\{\ln P_t - \ln P_0, \quad E[V(\ln P_{t+1}) \mid \ln P_t] - c\right\}$$

**Decision rule:** Exit when current profit exceeds expected future profit (accounting for holding costs).

$$\text{Exit if: } \quad \ln P_t - \ln P_0 \geq E[V(\ln P_{t+1}) \mid \ln P_t] - c$$

**Why this works better:**
1. Mean reversion dynamics are **linear** in log space
2. Conditional expectations are easy to compute from OU process
3. Probabilities are **stationary** (don't depend on price level)

## Concrete Example

**Setup:**
- Stock normally trades at $\ln P = 4.605$ ($e^{4.605} ≈ \$100$)
- Currently at $\ln P = 4.500$ ($e^{4.500} ≈ \$90$) — oversold!
- Mean reversion speed: $\theta = 2.0$ per hour
- Volatility: $\sigma = 0.15$ per hour
- Time step: $\Delta t = 0.1$ hours (6 minutes)

**Expected log price in 6 minutes:**

$$E[\ln P_{t+0.1}] = 4.500 + 2.0 \times (4.605 - 4.500) \times 0.1 = 4.500 + 0.021 = 4.521$$

In price terms: $e^{4.521} ≈ \$91.91$

**At current position $\ln P = 4.55$ ($\approx \$94.63$):**

Current profit: $4.55 - 4.50 = 0.05$ log points $\approx 5.13\%$

Expected profit if holding another 6 minutes:
$$E[\ln P_{t+0.1}] = 4.55 + 2.0 \times (4.605 - 4.55) \times 0.1 = 4.561$$

Expected profit: $4.561 - 4.50 = 0.061$ log points $\approx 6.29\%$

**Decision:** If holding cost $c < 0.011$ (≈1.1\%), keep holding!

## Symmetry Correction Example

**Common mistake:** Setting symmetric percentage stops/targets in price space.

Stock at \$100, trader sets:
- Target: \$110 (+10\%)
- Stop: \$90 (−10\%)

**In log space:**
- Target: $\ln(110/100) = 0.0953$
- Stop: $\ln(90/100) = -0.1054$

**Asymmetric!** You're risking 10.54\% to gain 9.53\%.

**Corrected symmetric setup:**
- Target: $\ln(100) + 0.10 = 4.705 \Rightarrow P = \$110.52$
- Stop: $\ln(100) - 0.10 = 4.505 \Rightarrow P = \$90.48$

Now risk/reward is truly balanced in log space.

## Julia Implementation

### Estimating OU Process Parameters

```julia
using Statistics, LinearAlgebra

function estimate_ou_parameters(log_prices::Vector{Float64}, Δt::Float64)
    """
    Estimate θ, μ, σ from historical log price data
    Using discrete-time regression: Δ(log P) = θ(μ - log P_t)Δt + ε
    """
    n = length(log_prices) - 1
    
    # Create regression variables
    X = hcat(ones(n), log_prices[1:end-1])  # [1, log P_t]
    y = diff(log_prices)  # Δ(log P)
    
    # OLS regression: y = β₀ + β₁*log_P_t + ε
    β = (X' * X) \ (X' * y)
    
    # Extract parameters
    # y = θμΔt - θΔt*log_P_t + ε
    θ = -β[2] / Δt
    μ = -β[1] / β[2]
    
    # Estimate volatility from residuals
    residuals = y - X * β
    σ = std(residuals) / sqrt(Δt)
    
    return θ, μ, σ
end

# Example usage
log_prices = [4.60, 4.58, 4.56, 4.55, 4.54, 4.53, 4.52, 4.50]
Δt = 1/60  # 1 minute intervals

θ, μ, σ = estimate_ou_parameters(log_prices, Δt)
println("θ (reversion speed): $(round(θ, digits=3))")
println("μ (long-run mean): $(round(μ, digits=3))")
println("σ (volatility): $(round(σ, digits=3))")
```

### Optimal Stopping Decision

```julia
function expected_log_price(log_P_current::Float64, θ::Float64, 
                           μ::Float64, Δt::Float64)
    """
    Expected log price after Δt under OU process
    E[ln P_{t+Δt} | ln P_t] = ln P_t + θ(μ - ln P_t)Δt
    """
    return log_P_current + θ * (μ - log_P_current) * Δt
end

function should_exit(log_entry::Float64, log_current::Float64, 
                    θ::Float64, μ::Float64, Δt::Float64, 
                    holding_cost::Float64)
    """
    Optimal stopping decision in log space
    Exit if current profit ≥ expected future profit - costs
    """
    # Current profit in log space
    current_profit = log_current - log_entry
    
    # Expected log price after Δt
    log_expected = expected_log_price(log_current, θ, μ, Δt)
    expected_profit = log_expected - log_entry
    
    # Exit if holding is not worth the cost
    return current_profit >= expected_profit - holding_cost
end

# Example: Decision at different price levels
log_entry = 4.50  # Entered at $90
θ, μ = 2.0, 4.605
Δt = 0.1  # 6 minutes
holding_cost = 0.001  # 0.1% cost

for log_P in 4.52:0.01:4.62
    P = exp(log_P)
    exit_decision = should_exit(log_entry, log_P, θ, μ, Δt, holding_cost)
    profit_pct = 100 * (log_P - log_entry)
    
    println("Price: \$$(round(P, digits=2)), " *
            "Profit: $(round(profit_pct, digits=2))%, " *
            "Exit: $exit_decision")
end
```

### Monte Carlo Simulation

```julia
using Random, Distributions

function simulate_ou_path(log_P0::Float64, θ::Float64, μ::Float64, 
                         σ::Float64, Δt::Float64, n_steps::Int)
    """
    Simulate one path of OU process in log space
    """
    log_prices = zeros(n_steps + 1)
    log_prices[1] = log_P0
    
    for t in 1:n_steps
        drift = θ * (μ - log_prices[t]) * Δt
        diffusion = σ * sqrt(Δt) * randn()
        log_prices[t+1] = log_prices[t] + drift + diffusion
    end
    
    return log_prices
end

function test_exit_strategies(log_entry::Float64, θ::Float64, μ::Float64,
                             σ::Float64, Δt::Float64, n_sims::Int)
    """
    Compare different exit strategies via Monte Carlo
    """
    n_steps = 100  # Simulate 100 time steps
    
    # Strategy results
    single_exit_profits = Float64[]
    scaled_exit_profits = Float64[]
    optimal_stop_profits = Float64[]
    
    for sim in 1:n_sims
        log_path = simulate_ou_path(log_entry, θ, μ, σ, Δt, n_steps)
        
        # Strategy 1: Single exit at +2% or -1% stop
        target = log_entry + 0.02
        stop = log_entry - 0.01
        single_profit = 0.0
        
        for log_P in log_path
            if log_P >= target
                single_profit = 0.02
                break
            elseif log_P <= stop
                single_profit = -0.01
                break
            end
        end
        push!(single_exit_profits, single_profit)
        
        # Strategy 2: Scaled exit (1/3 at 0.5%, 1%, 1.5%)
        targets = [log_entry + 0.005, log_entry + 0.01, log_entry + 0.015]
        filled = [false, false, false]
        scaled_profit = 0.0
        
        for log_P in log_path
            for i in 1:3
                if !filled[i] && log_P >= targets[i]
                    filled[i] = true
                    scaled_profit += (targets[i] - log_entry) / 3
                end
            end
            if all(filled)
                break
            end
        end
        push!(scaled_exit_profits, scaled_profit)
        
        # Strategy 3: Optimal stopping
        optimal_profit = 0.0
        for (i, log_P) in enumerate(log_path)
            if should_exit(log_entry, log_P, θ, μ, Δt, 0.0001)
                optimal_profit = log_P - log_entry
                break
            end
        end
        push!(optimal_stop_profits, optimal_profit)
    end
    
    # Calculate statistics
    strategies = ["Single Exit", "Scaled Exit", "Optimal Stop"]
    results = [single_exit_profits, scaled_exit_profits, optimal_stop_profits]
    
    println("\nMonte Carlo Results ($n_sims simulations):\n")
    println("Strategy          | Mean    | Std Dev | Sharpe")
    println("-" ^ 50)
    
    for (name, profits) in zip(strategies, results)
        μ_profit = mean(profits)
        σ_profit = std(profits)
        sharpe = μ_profit / σ_profit
        
        println("$(rpad(name, 17)) | " *
                "$(rpad(round(100*μ_profit, digits=3), 7)) | " *
                "$(rpad(round(100*σ_profit, digits=3), 7)) | " *
                "$(round(sharpe, digits=3))")
    end
end

# Run simulation
Random.seed!(42)
test_exit_strategies(4.50, 2.0, 4.605, 0.15, 0.1, 10000)
```

## Key Insights from Log Space Analysis

### 1. Probabilities are More Stable

In price space, the probability of reaching \$110 from \$100 is different from reaching \$55 from \$50.

In log space, $P(\text{reach } +0.0953 \mid \text{entry})$ is the same regardless of price level!

### 2. Variance Reduction Still Dominates

$$\text{Var}\left[\sum_{i=1}^{3} \frac{1}{3}(\ln P_{T_i} - \ln P_0)\right] < \text{Var}[\ln P_{T_3} - \ln P_0]$$

Scaled exits reduce variance in log space, which compounds to better long-term growth.

### 3. Kelly Criterion Connection

Since log returns compound multiplicatively, Kelly criterion naturally works in log space:

$$\max_f E[\ln(\text{Wealth})]$$

This reinforces: work in log space for all decision-making!

## Bottom Line

**Optimal stopping MUST use log prices** because:

1. ✓ Normalizes for price level
2. ✓ Makes mean reversion linear and tractable
3. ✓ Creates stable, stationary probabilities
4. ✓ Aligns with Kelly criterion (log wealth maximization)
5. ✓ Enables proper risk-symmetric stop/target placement

**And scaled exits still win** because variance reduction in log space leads to superior compounding over time!