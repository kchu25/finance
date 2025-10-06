@def title = "Mathematical Framework for Mean Reversion Exit Strategies"
@def published = "5 October 2025"
@def tags = ["exit-strategy"]

# Mathematical Framework for Mean Reversion Exit Strategies

## 1. Expected Value Framework

**The Big Idea:** Your goal is simple - maximize the average profit across all the different ways the trade could play out.

$$E[\text{Total Profit}] = \sum_{i} P(\text{scenario}_i) \times \text{Profit}_i$$

**Concrete Example:** Say you enter a mean reversion trade when a stock drops 2% below its average. Historically, you know:
- 40% of the time it bounces to +1% profit → contributes $0.40 \times 1\% = 0.40\%$
- 30% of the time it only reaches +0.5% → contributes $0.30 \times 0.5\% = 0.15\%$
- 30% of the time it drops further and you lose 1% → contributes $0.30 \times (-1\%) = -0.30\%$

**Expected profit:** $0.40\% + 0.15\% - 0.30\% = 0.25\%$ per trade

## 2. Exit Strategy Comparison

Let $P_0$ be where you bought and $P_t$ be the current price.

### Single Exit Strategy

**The Idea:** Pick one target, one stop loss. All or nothing.

$$E[\pi] = P(\text{hit target}) \times r_{\text{target}} - P(\text{hit stop}) \times r_{\text{stop}}$$

**Example:** You always exit at +1.5% or -1% stop loss.
- 60% chance of hitting +1.5%
- 40% chance of hitting -1%

$$E[\pi] = 0.60 \times 1.5\% - 0.40 \times 1\% = 0.90\% - 0.40\% = 0.50\%$$

### Scaled Exit Strategy

**The Idea:** Take money off the table gradually. Lock in some profit early, let some ride for bigger gains.

$$E[\pi] = \frac{1}{3}\sum_{i=1}^{3} T_i \cdot P(T_i \mid T_1, \ldots, T_{i-1})$$

**Example:** Sell 1/3 at each level: +0.5%, +1%, +1.5%

From historical data:
- $P(\text{reach } +0.5\%) = 0.80$ (80% of trades get here)
- $P(\text{reach } +1\% \mid \text{reached } +0.5\%) = 0.70$ (of those, 70% continue)
- $P(\text{reach } +1.5\% \mid \text{reached } +1\%) = 0.50$ (of those, 50% continue)

$$\begin{align}
E[\pi] &= \frac{1}{3}[0.5\% \times 0.80] + \frac{1}{3}[1.0\% \times (0.80 \times 0.70)] + \frac{1}{3}[1.5\% \times (0.80 \times 0.70 \times 0.50)] \\
&= \frac{1}{3}[0.40\%] + \frac{1}{3}[0.56\%] + \frac{1}{3}[0.42\%] \\
&= 0.133\% + 0.187\% + 0.140\% = 0.46\%
\end{align}$$

Notice this gives similar expected return to single exit, but with much less volatility!

## 3. Optimal Stopping Problem

**The Big Idea:** At every moment, you're asking: "Should I take profits now or wait for more?" This is a classic problem in math.

$$V(P_t) = \max\left\{P_t - P_0, \quad E[V(P_{t+1}) \mid P_t] - c\right\}$$

Keep holding when:

$$E[\text{Profit} \mid \text{hold}] > E[\text{Profit} \mid \text{exit now}]$$

**Example:** You're up 0.8% right now. Should you sell?

Current profit if you exit: **0.8%**

Expected profit if you hold one more minute:
- 60% chance price goes to 1.0% → profit = 1.0%
- 40% chance price drops to 0.5% → profit = 0.5%
- Expected value = $0.60 \times 1.0\% + 0.40 \times 0.5\% = 0.80\%$

They're equal! But if there's any holding cost $c$ (commissions, slippage risk), you should exit now.

## 4. Risk-Adjusted Performance

### Sharpe Ratio

**The Idea:** Making money is great, but how bumpy is the ride? Sharpe ratio measures profit per unit of risk.

$$\text{Sharpe} = \frac{E[R] - R_f}{\sigma(R)}$$

**Example:** Compare two strategies over 100 trades:

**Strategy A (single exit):**
- Average profit: 0.50%
- Standard deviation: 1.2%
- Sharpe = $0.50\% / 1.2\% = 0.42$

**Strategy B (scaled exit):**
- Average profit: 0.46%
- Standard deviation: 0.8%
- Sharpe = $0.46\% / 0.8\% = 0.58$ ✓ **Better!**

Strategy B makes slightly less on average, but it's much smoother, so it wins on risk-adjusted basis.

### Utility Function

**The Idea:** How much do you hate losing? The parameter $\lambda$ measures your fear.

$$U = E[\pi] - \frac{\lambda}{2}\text{Var}[\pi]$$

**Example:** You're choosing between two strategies:

**Strategy A:**
- $E[\pi] = 1.0\%$
- $\text{Var}[\pi] = 4\%^2 = 0.0016$

**Strategy B:**
- $E[\pi] = 0.8\%$
- $\text{Var}[\pi] = 1\%^2 = 0.0001$

If you're moderately risk-averse with $\lambda = 2$:

$$\begin{align}
U_A &= 1.0\% - \frac{2}{2} \times 0.0016 = 1.0\% - 0.16\% = 0.84\% \\
U_B &= 0.8\% - \frac{2}{2} \times 0.0001 = 0.8\% - 0.01\% = 0.79\%
\end{align}$$

Strategy A still wins, but it's close. If $\lambda = 4$ (very risk-averse), then B wins.

## 5. Kelly Criterion for Position Sizing

**The Idea:** How much of your bankroll should you risk? Kelly tells you the mathematically optimal amount.

$$f^* = \frac{p \cdot b - q}{b}$$

where $p$ = win probability, $q$ = loss probability, $b$ = win/loss ratio

**Example:** Your mean reversion strategy:
- Wins 65% of the time ($p = 0.65$, $q = 0.35$)
- Average win is 1.5%, average loss is 1% → $b = 1.5$

$$f^* = \frac{0.65 \times 1.5 - 0.35}{1.5} = \frac{0.975 - 0.35}{1.5} = \frac{0.625}{1.5} = 0.417$$

**Bet 41.7% of your capital on each trade.**

**Connection to Exits:** As the stock reverts to the mean, your edge shrinks (less room to run). Kelly says reduce exposure proportionally → this mathematically justifies scaling out!

## 6. Conditional Probability Framework

**The Idea:** Use your historical data to estimate: "If I've gotten this far, what are the odds I get further?"

$$\begin{align}
P(\text{reach } +0.5\% \mid \text{entry}) &= p_1 \\
P(\text{reach } +1.0\% \mid \text{reached } +0.5\%) &= p_2 \\
P(\text{reach } +1.5\% \mid \text{reached } +1.0\%) &= p_3
\end{align}$$

**Real Example from Backtest:** You analyze 200 mean reversion trades:
- 160 reached +0.5% → $p_1 = 160/200 = 0.80$
- Of those 160, 100 reached +1.0% → $p_2 = 100/160 = 0.625$
- Of those 100, 40 reached +1.5% → $p_3 = 40/100 = 0.40$

Expected profit for 1/3 position at each level:

$$E[\pi] = \frac{1}{3}(0.5\% \times 0.80) + \frac{1}{3}(1.0\% \times 0.80 \times 0.625) + \frac{1}{3}(1.5\% \times 0.80 \times 0.625 \times 0.40)$$

$$= \frac{1}{3}(0.40\%) + \frac{1}{3}(0.50\%) + \frac{1}{3}(0.30\%) = 0.40\%$$

## 7. Monte Carlo Optimization

**The Idea:** Can't solve it analytically? Simulate it 10,000 times and see which strategy wins!

$$\begin{align}
\mu &= \frac{1}{N}\sum_{i=1}^{N} \pi_i \quad \text{(mean profit)} \\
\sigma^2 &= \frac{1}{N}\sum_{i=1}^{N} (\pi_i - \mu)^2 \quad \text{(variance)} \\
\text{Sharpe} &= \frac{\mu}{\sigma}
\end{align}$$

**Example Simulation Results (10,000 trades each):**

| Strategy | Mean Profit | Std Dev | Sharpe | Median Profit |
|----------|-------------|---------|--------|---------------|
| Single Exit (1.5%) | 0.52% | 1.8% | 0.29 | 0.30% |
| Scaled (0.5/1.0/1.5%) | 0.48% | 1.1% | **0.44** | **0.45%** |
| Trailing Stop | 0.55% | 2.2% | 0.25 | 0.20% |

**Winner:** Scaled exit has the best Sharpe and best median (it's more consistent).

Choose strategy that maximizes:

$$\arg\max_{\text{strategy}} \left\{\text{Sharpe ratio}, \quad \text{Median}[\pi]\right\}$$

## Key Mathematical Insight

Scaled exits dominate because of the **variance reduction effect**:

$$\text{Var}\left[\frac{1}{3}X_1 + \frac{1}{3}X_2 + \frac{1}{3}X_3\right] < \text{Var}[X_3]$$

Even though $E[X_3]$ might be highest (waiting for the biggest target), the variance kills your Sharpe ratio. By taking partial profits, you:

1. **Reduce $\text{Var}[\pi]$** → smoother equity curve
2. **Maintain exposure** to tail events → don't miss the big moves
3. **Achieve higher Sharpe** → better compounding long-term