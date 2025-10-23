@def title = "Options Greeks: The Complete Guide"
@def published = "22 October 2025"
@def tags = ["options"]

# Options Greeks: The Complete Guide

## Quick Reference Table

| Greek | Catchphrase | Measures | Typical Range |
|-------|-------------|----------|---------------|
| **Delta (Δ)** | "Speed of profit" | Price sensitivity | -1 to +1 |
| **Gamma (Γ)** | "Acceleration of delta" | Delta's rate of change | 0 to ~0.1 |
| **Theta (Θ)** | "Time is money (bleeding)" | Time decay per day | Negative for long |
| **Vega (ν)** | "Volatility appetite" | IV sensitivity | 0 to ~1+ |
| **Rho (ρ)** | "Interest rate whisper" | Rate sensitivity | Small values |

---

## Delta (Δ): The Directional Compass

### Mathematical Definition
```
Δ = ∂V/∂S
(Change in option value per $1 change in underlying)
```

### Catchphrase: **"Speed of Profit"**

### Key Concepts
- **Calls**: 0 to +1.00 (usually 0.01 to 0.99)
- **Puts**: -1.00 to 0 (usually -0.99 to -0.01)
- **At-the-money (ATM)**: ~0.50 for calls, ~-0.50 for puts
- **Deep in-the-money (ITM)**: approaches ±1.00
- **Out-of-the-money (OTM)**: approaches 0

### Intuitive Understanding
- Delta of 0.30 = "30% probability of expiring ITM" (rough approximation)
- Delta of 0.50 call = "Move $50 when stock moves $100"
- Delta of -0.25 put = "Gain $25 when stock drops $100"

### Algo-Trading Applications
```python
# Delta-neutral strategies
portfolio_delta = sum(position.quantity * position.delta)

# Dynamic hedging
if abs(portfolio_delta) > threshold:
    hedge_quantity = -portfolio_delta / underlying_delta
    execute_hedge(hedge_quantity)

# Delta-based position sizing
position_size = target_delta_exposure / option_delta
```

**Common Strategies:**
- **Delta hedging**: Keep portfolio delta near zero
- **Directional trading**: Accumulate positive/negative delta
- **Delta-weighted portfolios**: Balance exposure across positions

---

## Gamma (Γ): The Curvature Monster

### Mathematical Definition
```
Γ = ∂²V/∂S² = ∂Δ/∂S
(Change in delta per $1 change in underlying)
```

### Catchphrase: **"Acceleration of Delta"**

### Key Concepts
- **Always positive** for long options (both calls and puts)
- **Highest at-the-money** and near expiration
- **Decreases** as you move ITM or OTM
- **Explodes** in the final days before expiry

### Intuitive Understanding
- High gamma = "Delta changes rapidly" = More dynamic hedging needed
- Low gamma = "Delta is stable" = Less rebalancing required
- Gamma scalping = Profiting from realized volatility exceeding implied volatility

### The Gamma Trap
**Long gamma** (long options):
- ✅ Benefits from big moves (convexity)
- ❌ Pays theta for the privilege

**Short gamma** (short options):
- ✅ Collects theta
- ❌ Gets hurt by big moves (negative convexity)

### Algo-Trading Applications
```python
# Gamma scalping
if position.gamma > 0:  # Long gamma
    # When stock moves up, delta increases
    # Sell stock to rebalance (sell high)
    if underlying.price_change > threshold:
        rebalance_quantity = gamma * price_change
        sell(underlying, rebalance_quantity)
    
    # When stock moves down, delta decreases
    # Buy stock to rebalance (buy low)
    elif underlying.price_change < -threshold:
        rebalance_quantity = abs(gamma * price_change)
        buy(underlying, rebalance_quantity)

# Gamma risk management
max_gamma_exposure = account_size * risk_factor
if abs(portfolio_gamma) > max_gamma_exposure:
    reduce_positions()
```

**Common Strategies:**
- **Gamma scalping**: Profit from rebalancing a delta-hedged position
- **Pin risk management**: Monitor gamma near strike prices at expiration
- **Zero-gamma portfolios**: Combine different strikes to neutralize gamma

---

## Theta (Θ): The Silent Killer

### Mathematical Definition
```
Θ = ∂V/∂t
(Change in option value per day passing)
```

### Catchphrase: **"Time is Money Bleeding"**

### Key Concepts
- **Always negative** for long options (you lose money daily)
- **Always positive** for short options (you gain money daily)
- **Accelerates** as expiration approaches
- **Highest** for at-the-money options
- Measured in dollars per day (e.g., Θ = -0.05 = lose $5/day on 100 shares)

### Intuitive Understanding
- "Every day you hold, you pay rent"
- ATM options decay fastest in the final 30 days
- Weekend theta: Some brokers charge 3 days on Friday

### The Theta Curve
```
High θ decay  →  📉📉📉  ← Final 30 days
Medium θ      →  📉📉    ← 30-60 days
Low θ         →  📉     ← 60+ days
```

### Algo-Trading Applications
```python
# Theta decay strategies
daily_theta_income = sum(pos.theta * pos.quantity for pos in portfolio)

# Roll timing optimization
days_to_expiry = (option.expiry - today).days
if days_to_expiry < theta_roll_threshold and theta_decay_accelerating:
    roll_to_next_expiry()

# Time-based position management
theta_to_premium_ratio = abs(theta) / option_price
if theta_to_premium_ratio > 0.05:  # Losing 5%+ per day
    consider_closing_position()
```

**Common Strategies:**
- **Theta harvesting**: Sell options to collect decay (iron condors, credit spreads)
- **Theta avoidance**: Close long options before heavy decay period
- **Calendar spreads**: Exploit differences in theta between expirations

---

## Vega (ν): The Volatility Surfer

### Mathematical Definition
```
ν = ∂V/∂σ
(Change in option value per 1% change in implied volatility)
```

### Catchphrase: **"Volatility Appetite"**

### Key Concepts
- **Always positive** for long options (benefit from IV increase)
- **Always negative** for short options (hurt by IV increase)
- **Highest** for at-the-money options
- **Increases** with time to expiration (more time = more uncertainty)
- Measured in dollars per 1% IV change (e.g., ν = 0.12 = gain $12 if IV rises 1%)

### Intuitive Understanding
- Long vega = "Betting on uncertainty increasing" = Long options
- Short vega = "Betting on calm markets" = Short options
- Vega and theta trade-off: High vega usually means high theta cost

### The IV Crush
**Earnings events:**
- Before: IV inflated (high vega)
- After: IV collapses (vega value evaporates)
- Long options lose even if directionally correct!

### Algo-Trading Applications
```python
# Volatility regime detection
current_iv = option.implied_volatility
historical_iv_percentile = get_percentile(current_iv, lookback=252)

if historical_iv_percentile > 80:  # High IV environment
    # Sell premium (short vega)
    execute_strategy('iron_condor')
elif historical_iv_percentile < 20:  # Low IV environment
    # Buy premium (long vega)
    execute_strategy('long_straddle')

# Vega-neutral strategies
portfolio_vega = sum(pos.vega * pos.quantity for pos in portfolio)
if abs(portfolio_vega) > threshold:
    # Add opposite vega exposure
    hedge_with_vega_offset()

# Event-based vega trading
if earnings_date_approaching and iv_rank < 50:
    # Buy volatility before it spikes
    buy_options_before_event()
```

**Common Strategies:**
- **Vega arbitrage**: Exploit IV differences across strikes/expirations
- **Vol selling**: Short vega in high IV percentile environments
- **Vol buying**: Long vega before expected volatility expansion
- **Dispersion trading**: Trade realized vs implied vol differences

---

## Rho (ρ): The Forgotten Greek

### Mathematical Definition
```
ρ = ∂V/∂r
(Change in option value per 1% change in risk-free rate)
```

### Catchphrase: **"Interest Rate Whisper"**

### Key Concepts
- **Usually the smallest Greek** in terms of impact
- **Positive for calls**, **negative for puts**
- **Matters more** for long-dated options (LEAPS)
- **Mostly ignored** for short-term trading

### Intuitive Understanding
- Higher rates → Calls worth more (opportunity cost of capital)
- Higher rates → Puts worth less
- Only really matters when Fed is actively changing rates

### Algo-Trading Applications
```python
# Mostly ignored in short-term trading, but for LEAPS:
if option.days_to_expiry > 365:
    # Monitor Fed policy changes
    if fed_rate_change_expected:
        adjust_for_rho_exposure()

# Interest rate environment positioning
if rising_rate_environment and holding_long_dated_calls:
    rho_benefit = position.rho * expected_rate_change
    # Factor into position valuation
```

---

## Second-Order Greeks (Advanced)

### Vanna: ∂Δ/∂σ
**"Delta's volatility sensitivity"**
- How much delta changes when IV changes
- Important for volatility skew trading

### Charm: ∂Δ/∂t
**"Delta decay"**
- How much delta changes as time passes
- Critical for pin risk near expiration

### Vomma (Volga): ∂ν/∂σ
**"Vega's volatility sensitivity"**
- How vega changes with IV changes
- Important for volatility of volatility trading

### Zomma: ∂Γ/∂σ
**"Gamma's volatility sensitivity"**
- How gamma changes when IV changes

---

## Greeks in API Responses

Yes, most options data providers include Greeks in their API responses:

### Typical JSON Response Structure
```json
{
  "symbol": "AAPL250117C00150000",
  "underlying": "AAPL",
  "strike": 150,
  "expiry": "2025-01-17",
  "type": "call",
  "last_price": 12.50,
  "bid": 12.45,
  "ask": 12.55,
  "volume": 1250,
  "open_interest": 5430,
  "implied_volatility": 0.28,
  "greeks": {
    "delta": 0.5234,
    "gamma": 0.0156,
    "theta": -0.0423,
    "vega": 0.1892,
    "rho": 0.0234
  },
  "underlying_price": 148.75
}
```

### Popular Data Providers
- **Interactive Brokers API**: Yes, includes Greeks
- **TD Ameritrade API**: Yes, includes Greeks
- **Tradier**: Yes, includes Greeks
- **Polygon.io**: Yes, includes Greeks
- **CBOE Data**: Yes, includes Greeks
- **Bloomberg Terminal**: Yes, extensive Greeks

### Calculating Greeks Yourself
If your data source doesn't provide Greeks, you can calculate them using Black-Scholes:

```python
from scipy.stats import norm
import numpy as np

def black_scholes_greeks(S, K, T, r, sigma, option_type='call'):
    """
    S: underlying price
    K: strike price
    T: time to expiration (years)
    r: risk-free rate
    sigma: volatility
    """
    d1 = (np.log(S/K) + (r + sigma**2/2)*T) / (sigma*np.sqrt(T))
    d2 = d1 - sigma*np.sqrt(T)
    
    if option_type == 'call':
        delta = norm.cdf(d1)
        theta = (-S*norm.pdf(d1)*sigma/(2*np.sqrt(T)) 
                 - r*K*np.exp(-r*T)*norm.cdf(d2)) / 365
        rho = K*T*np.exp(-r*T)*norm.cdf(d2) / 100
    else:  # put
        delta = -norm.cdf(-d1)
        theta = (-S*norm.pdf(d1)*sigma/(2*np.sqrt(T)) 
                 + r*K*np.exp(-r*T)*norm.cdf(-d2)) / 365
        rho = -K*T*np.exp(-r*T)*norm.cdf(-d2) / 100
    
    gamma = norm.pdf(d1) / (S*sigma*np.sqrt(T))
    vega = S*norm.pdf(d1)*np.sqrt(T) / 100
    
    return {
        'delta': delta,
        'gamma': gamma,
        'theta': theta,
        'vega': vega,
        'rho': rho
    }
```

---

## Practical Algo-Trading Framework

### 1. Risk Management Using Greeks
```python
class GreeksRiskManager:
    def __init__(self, portfolio):
        self.portfolio = portfolio
    
    def get_portfolio_greeks(self):
        return {
            'delta': sum(p.delta * p.quantity for p in self.portfolio),
            'gamma': sum(p.gamma * p.quantity for p in self.portfolio),
            'theta': sum(p.theta * p.quantity for p in self.portfolio),
            'vega': sum(p.vega * p.quantity for p in self.portfolio),
        }
    
    def check_limits(self, limits):
        greeks = self.get_portfolio_greeks()
        violations = []
        
        for greek, value in greeks.items():
            if abs(value) > limits.get(greek, float('inf')):
                violations.append(f"{greek}: {value:.2f} exceeds {limits[greek]}")
        
        return violations
```

### 2. Greeks-Based Position Sizing
```python
def size_position_by_greeks(target_exposure, option_greeks, risk_limits):
    """
    Determine position size based on Greek exposures
    """
    # Primary constraint: Delta exposure
    max_by_delta = abs(target_exposure['delta'] / option_greeks['delta'])
    
    # Secondary constraint: Gamma exposure
    max_by_gamma = abs(risk_limits['gamma'] / option_greeks['gamma'])
    
    # Tertiary constraint: Vega exposure
    max_by_vega = abs(risk_limits['vega'] / option_greeks['vega'])
    
    # Take minimum to respect all constraints
    position_size = min(max_by_delta, max_by_gamma, max_by_vega)
    
    return int(position_size)
```

### 3. Dynamic Hedging Algorithm
```python
class DynamicHedger:
    def __init__(self, rehedge_threshold=100):
        self.rehedge_threshold = rehedge_threshold  # Delta threshold
    
    def should_rehedge(self, portfolio_delta):
        return abs(portfolio_delta) > self.rehedge_threshold
    
    def calculate_hedge(self, portfolio_delta, underlying_price):
        # Hedge with underlying shares
        shares_to_hedge = -portfolio_delta
        
        return {
            'action': 'buy' if shares_to_hedge > 0 else 'sell',
            'quantity': abs(shares_to_hedge),
            'instrument': 'underlying'
        }
    
    def execute_hedge(self, hedge_order):
        # Execute the hedge trade
        print(f"Hedging: {hedge_order['action']} {hedge_order['quantity']} shares")
```

### 4. Greeks-Based Signal Generation
```python
def generate_signals(option_chain, market_conditions):
    signals = []
    
    for option in option_chain:
        # High IV + High Theta = Good short opportunity
        if (option.implied_volatility > market_conditions['iv_75th_percentile'] and
            abs(option.theta) / option.price > 0.03):
            signals.append({
                'type': 'SELL_PREMIUM',
                'option': option,
                'reason': 'High IV, High Theta decay'
            })
        
        # Low IV + ATM + Long DTE = Good long vega opportunity
        if (option.implied_volatility < market_conditions['iv_25th_percentile'] and
            0.4 < abs(option.delta) < 0.6 and
            option.days_to_expiry > 30):
            signals.append({
                'type': 'BUY_VOLATILITY',
                'option': option,
                'reason': 'Low IV, ATM, good vega exposure'
            })
        
        # High Gamma near expiry = Avoid or gamma scalp
        if (option.gamma > 0.05 and option.days_to_expiry < 7):
            signals.append({
                'type': 'GAMMA_SCALP' if market_conditions['volatile'] else 'AVOID',
                'option': option,
                'reason': 'High gamma + near expiry'
            })
    
    return signals
```

---

## Common Greek-Based Strategies

### 1. Delta-Neutral Portfolio
**Goal:** Zero delta, profit from other Greeks
```
Long 100 shares of stock (+100 delta)
Short 2 ATM calls (-100 delta)
= 0 net delta, positive theta, short gamma/vega
```

### 2. Gamma Scalping
**Goal:** Profit from realized volatility > implied volatility
```
Long straddle (long gamma, short theta)
Continuously rebalance delta by trading underlying
Profit if realized vol > implied vol
```

### 3. Iron Condor (Theta Harvesting)
**Goal:** Collect theta, stay within range
```
Short OTM call + Short OTM put (collect theta)
Long further OTM call + Long further OTM put (define risk)
= Positive theta, negative gamma/vega, near-zero delta
```

### 4. Calendar Spread (Vega & Theta Play)
**Goal:** Exploit different decay rates
```
Sell near-term option (high theta decay)
Buy longer-term option (lower theta decay)
= Positive vega, small positive theta
```

### 5. Diagonal Spread (Delta + Theta)
**Goal:** Directional + income
```
Sell near-term OTM option
Buy longer-term closer-to-ATM option
= Directional delta + theta collection
```

---

## Key Takeaways for Algo-Trading

1. **Monitor all Greeks continuously** - They change with price, time, and volatility
2. **Greeks interact** - Changing one affects others (delta-gamma, vega-theta relationships)
3. **Scale matters** - 1 contract vs 100 contracts = 100x the Greek exposure
4. **Greeks are estimates** - Models (Black-Scholes) have assumptions that don't always hold
5. **Execution matters** - Slippage can eat up theoretical Greek advantages
6. **Combine Greeks for signals** - Multi-dimensional analysis is more robust
7. **Hedge dynamically** - Greeks change constantly, static hedges degrade
8. **Watch for Greek explosions** - Near expiry, Greeks become extreme and less predictable
9. **Use Greeks for risk limits** - Set maximum portfolio Greek exposures
10. **Backtest with Greeks** - Don't just simulate P&L, track Greek evolution

---

## The Ultimate Greek Cheat Sheet

| Situation | Primary Greek | Action |
|-----------|---------------|--------|
| Expecting big move | Gamma | Buy straddle/strangle |
| Expecting low volatility | Theta | Sell iron condor |
| IV extremely high | Vega | Sell premium |
| IV extremely low | Vega | Buy premium |
| Need directional exposure | Delta | Buy calls/puts |
| Time is running out | Theta | Close long options |
| Near expiration at strike | Gamma | Close or roll position |
| Rates rising (rare concern) | Rho | Consider for LEAPS only |

**Final Wisdom:** Greeks are your navigation instruments. You wouldn't fly a plane without checking your instruments constantly—don't trade options without monitoring your Greeks.