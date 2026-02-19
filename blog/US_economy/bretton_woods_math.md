@def title = "The Math of Manufactured Dollar Demand"
@def tags = ["macro", "stablecoins"]
@def published = "19 February 2026"
@def rss_pubdate = Date(2026, 2, 19)
@def rss_description = "A mathematical companion to the Bretton Woods post — formalizing the gold standard correction mechanism, Bretton Woods dollar demand, the Triffin Dilemma, petrodollar recycling, stablecoin Treasury demand, and debt sustainability into precise (and surprisingly simple) equations."

# The Math of Manufactured Dollar Demand

\toc

---

## Why Formalize This?

The [Bretton Woods post](/blog/US_economy/bretton_woods/) tells the story of three systems of structural dollar demand: gold-peg reserve accumulation (1944), petrodollar recycling (1974), and stablecoin Treasury mandates (2025). The narrative is persuasive, but narratives can hide sloppy reasoning.

This companion post translates each mechanism into math. The goal isn't to build a publishable economic model — it's to check whether the verbal arguments are *structurally coherent*, and to answer a specific question: **do these mechanisms reduce to simple linear equations, or is there hidden nonlinearity?**

Spoiler: it's almost entirely linear. The one exception is important.

---

## 1. The Classical Gold Standard — Self-Correcting Trade

### The Mechanism (in words)

Under the gold standard, trade imbalances self-corrected. A country importing more than it exported lost gold, which contracted its money supply, which lowered prices, which made its exports cheaper, which corrected the deficit.

### The Model

Let country $i$ at time $t$ have:
- $G_i(t)$: gold reserves
- $M_i(t)$: money supply
- $P_i(t)$: domestic price level
- $X_i(t)$: exports
- $Z_i(t)$: imports
- $B_i(t) = X_i(t) - Z_i(t)$: trade balance

**Equation 1 — Gold flow.** Gold moves according to the trade balance:

$$\Delta G_i = G_i(t+1) - G_i(t) = B_i(t) = X_i(t) - Z_i(t)$$

Deficit ($B_i < 0$) means gold flows out. Surplus ($B_i > 0$) means gold flows in. This is an accounting identity — not a behavioral assumption.

**Equation 2 — Money supply tracks gold.** Under a gold standard, the money supply is proportional to gold reserves:

$$M_i(t) = k \cdot G_i(t), \quad k > 0$$

where $k$ is the money multiplier (constant under strict gold standard rules). This is **linear**.

**Equation 3 — Prices track money supply.** By the [quantity theory of money](https://en.wikipedia.org/wiki/Quantity_theory_of_money):

> **What is $MV = PY$?**
>
> This is the [Fisher equation](https://en.wikipedia.org/wiki/Equation_of_exchange), the foundational identity of monetary economics:
> - $M$ — the money supply (total currency and deposits in circulation)
> - $V$ — velocity of money (how many times the average dollar changes hands per year)
> - $P$ — the price level (average price of goods and services)
> - $Y$ — real output (total quantity of goods and services produced)
>
> The left side $MV$ is the total dollar value of all transactions in the economy. The right side $PY$ is the same thing viewed differently: price times quantity = nominal GDP. So $MV = PY$ is an accounting identity, always true by definition.
>
> The behavioral assumption comes when we treat $V$ and $Y$ as roughly *constant* in the short run — a reasonable approximation when the economy isn't in upheaval. Under that assumption, doubling $M$ must double $P$: more money chasing the same amount of goods means higher prices. This is why printing money causes inflation, and why losing gold (which contracted $M$) caused deflation under the gold standard.

In its simplest form, holding velocity $V$ and real output $Y$ roughly constant in the short run:

$$P_i(t) = \frac{M_i(t) \cdot V}{Y_i} = \frac{k \cdot V}{Y_i} \cdot G_i(t)$$

Prices are **linear** in gold reserves.

**Equation 4 — Exports respond to prices.** Lower prices make a country's goods cheaper on world markets. In the simplest specification:

$$X_i(t) = \bar{X}_i - \alpha \cdot P_i(t), \quad \alpha > 0$$

Exports are **linear** in the price level (and therefore linear in gold reserves).

**Equation 5 — Imports respond to prices.** Higher domestic prices make foreign goods relatively cheaper, increasing imports:

$$Z_i(t) = \bar{Z}_i + \beta \cdot P_i(t), \quad \beta > 0$$

Also **linear**.

### The Complete Dynamics

Substituting everything into the gold flow equation:

$$\Delta G_i = (\bar{X}_i - \alpha P_i) - (\bar{Z}_i + \beta P_i) = (\bar{X}_i - \bar{Z}_i) - (\alpha + \beta) P_i$$

Since $P_i$ is proportional to $G_i$, let $\gamma = (\alpha + \beta) \cdot \frac{kV}{Y_i}$. Then:

$$\boxed{\Delta G_i = \underbrace{(\bar{X}_i - \bar{Z}_i)}_{\text{structural balance}} - \gamma \cdot G_i(t)}$$

This is a **first-order linear difference equation** with a negative feedback coefficient ($-\gamma < 0$). It has a unique stable equilibrium:

$$G_i^* = \frac{\bar{X}_i - \bar{Z}_i}{\gamma}$$

**Interpretation:** The gold standard was a *linear negative feedback system*. Trade deficits automatically reduced gold, which reduced money supply, which reduced prices, which corrected the deficit. The correction was proportional to the imbalance.

**Why it failed:** The model assumes $k$ is constant (strict gold standard rules) and that $Y_i$ doesn't collapse. During the Great Depression, $Y_i$ collapsed, making the $\frac{kV}{Y_i}$ factor enormous — prices fell catastrophically, but the deflation destroyed real output faster than it corrected trade imbalances. The linear model was technically correct but the correction mechanism was too brutal for the real economy to absorb. Governments abandoned the gold standard not because the math was wrong, but because the social cost of the equilibrating mechanism was unbearable.

---

## 2. Bretton Woods — Structural Dollar Demand

### The Mechanism (in words)

Countries peg their currencies to the dollar. Maintaining the peg requires dollar reserves. Dollar reserves are held as Treasuries. Therefore, participating in the system generates Treasury demand proportional to participation.

### The Model

Let there be $n$ countries indexed $i = 1, \ldots, n$, each with:
- $e_i$: fixed exchange rate (units of currency $i$ per dollar), set at Bretton Woods
- $T_i(t)$: trade volume of country $i$ in period $t$
- $R_i(t)$: dollar reserves held by country $i$

**Equation 6 — Reserve requirement.** To defend a fixed peg, a central bank needs reserves proportional to its trade exposure and the width of allowed fluctuations. In the simplest form:

$$R_i(t) = \lambda \cdot T_i(t), \quad \lambda > 0$$

where $\lambda$ is the reserve-adequacy ratio (typically 3–6 months of import cover). This is **linear** — twice the trade volume requires twice the reserves.

**Equation 7 — Aggregate dollar demand.** Total structural dollar demand from the Bretton Woods system is:

$$D_{\text{BW}}(t) = \sum_{i=1}^{n} R_i(t) = \lambda \sum_{i=1}^{n} T_i(t) = \lambda \cdot T_{\text{world}}(t)$$

**Structural dollar demand is linear in world trade volume.** As global trade grows, dollar demand grows proportionally. This is the key insight: Bretton Woods didn't create a *fixed* stock of dollar demand — it created a *flow* that scaled with the world economy.

**Equation 8 — Reserves held as Treasuries.** Let $\theta$ be the fraction of dollar reserves held in Treasuries (versus cash deposits or other dollar assets). Then Treasury demand from Bretton Woods is:

$$\boxed{D_{\text{Treasury}}^{\text{BW}}(t) = \theta \cdot \lambda \cdot T_{\text{world}}(t)}$$

This is **linear** in world trade. Historically, $\theta$ was high (Treasuries were the safest, most liquid dollar-denominated asset), so practically all reserve accumulation became Treasury demand.

### The Scaling Behavior

World trade grew at roughly 6–8% per year in real terms during 1945–1971. That means Bretton Woods generated *exponentially growing* Treasury demand — not because the equation was exponential, but because the input ($T_{\text{world}}$) was growing exponentially. The equation itself was linear; the growth was in the underlying driver.

This distinction matters: the system's demand-generating power was entirely dependent on the growth rate of world trade. If trade stagnated, dollar demand would stagnate. The US was, in effect, borrowing against global trade growth.

---

## 3. The Triffin Dilemma — When Linear Meets a Constraint

### The Mechanism (in words)

The world needs more dollars (from US deficits) to fuel growing trade. But each dollar held abroad is a claim on US gold. US gold reserves are finite. Eventually, claims exceed reserves, and confidence collapses.

### The Model

Let:
- $D(t) = \lambda \cdot T_{\text{world}}(t)$: total foreign dollar holdings (from Equation 7)
- $G_{\text{US}}(t)$: US gold reserves (in dollar terms at \$35/oz)
- $\phi(t) = \frac{G_{\text{US}}(t)}{D(t)}$: gold coverage ratio

**Equation 9 — The coverage ratio.** Confidence in dollar-gold convertibility requires $\phi(t) \geq \phi_{\min}$, some minimum threshold (psychologically, around 25–40% seemed to be where markets got nervous).

Now, the critical dynamics:
- $D(t)$ grows with world trade (roughly exponential: $D(t) \approx D_0 \cdot e^{g \cdot t}$ where $g \approx 0.07$)
- $G_{\text{US}}(t)$ is roughly constant or slowly declining (gold is a finite physical stock; the US was slowly losing gold to conversions)

Therefore:

$$\phi(t) = \frac{G_{\text{US}}(t)}{D_0 \cdot e^{g \cdot t}} \to 0 \quad \text{as } t \to \infty$$

**The coverage ratio converges monotonically to zero.** This isn't a matter of *if* — it's a matter of *when*.

$$\boxed{\text{Triffin Dilemma: } \phi(t) = \frac{G_{\text{US}}}{D_0 \cdot e^{gt}} \xrightarrow{t \to \infty} 0}$$

**The failure was mathematically inevitable.** Not because of policy mistakes, Vietnam spending, or de Gaulle's demands (though all of these accelerated the timeline). The system's linear demand equation was feeding off an exponentially growing input (world trade), while the system's constraint (gold reserves) was bounded above. An exponentially growing numerator divided by a fixed numerator — I mean a fixed denominator divided by an exponentially growing denominator — converges to zero.

Correction: fixed denominator $G_{\text{US}}$ over exponentially growing $D(t)$. The ratio is:

$$\phi(t) = \frac{G_{\text{US}}}{D(t)} = \frac{\text{bounded}}{\text{exponentially growing}} \to 0$$

This is the one place in the story where the interaction of linearity (the demand equation) with a *hard constraint* (finite gold) produces nonlinear dynamics — specifically, a *collapse threshold*. The demand equation itself is linear. The constraint is not. Their interaction creates a crisis.

### How fast?

If $D(t)$ grows at $g = 7\%$ per year and $G_{\text{US}}$ is constant, the coverage ratio halves every $\frac{\ln 2}{g} \approx 10$ years:

| Year | $\phi$ (approx.) |
|:---|:---|
| 1950 | 65% |
| 1960 | 33% |
| 1970 | 17% |

The actual historical numbers were 65% (1950), ~40% (1960), 22% (1970). The simple exponential decay model isn't far off.

---

## 4. Petrodollar Recycling — The Flow Loop

### The Mechanism (in words)

Oil is priced in dollars. Oil importers need dollars. Oil exporters earn dollars. Exporters recycle surplus dollars into Treasuries. A closed loop that generates Treasury demand proportional to oil trade volume.

### The Model

Let:
- $Q(t)$: global oil consumption (barrels/year)
- $p(t)$: price of oil in USD per barrel
- $s$: OPEC's share of global oil production
- $c$: OPEC's domestic consumption/spending as a fraction of revenue (what they *don't* save)
- $\eta$: fraction of OPEC surplus invested in Treasuries

**Equation 10 — OPEC revenue.**

$$\text{Rev}_{\text{OPEC}}(t) = s \cdot p(t) \cdot Q(t)$$

**Equation 11 — OPEC surplus (amount available for recycling).**

$$S_{\text{OPEC}}(t) = (1 - c) \cdot s \cdot p(t) \cdot Q(t)$$

**Equation 12 — Treasury demand from petrodollar recycling.**

$$\boxed{D_{\text{Treasury}}^{\text{petro}}(t) = \eta \cdot (1 - c) \cdot s \cdot p(t) \cdot Q(t)}$$

This is **linear** — specifically, linear in both the oil price and the quantity consumed. Treasury demand from the petrodollar system is just a constant fraction of the global oil bill.

### What drives the scaling?

Oil consumption grew at ~1.5% per year from 1974–2008. Oil prices were volatile but trended upward (from ~\$12/barrel in 1974 to ~\$100/barrel by 2008). The product $p(t) \cdot Q(t)$ — the total dollar value of global oil trade — drove the scaling of Treasury demand.

The petrodollar system's demand-generating capacity is proportional to $p \cdot Q$. This is why:
- When oil prices spike → OPEC surpluses spike → Treasury purchases spike
- When oil prices crash → OPEC surpluses evaporate → Treasury purchases slow
- When oil consumption declines (energy transition) → the entire mechanism weakens

### Comparison to Bretton Woods

Both are linear, but the driver differs:

$$D_{\text{Treasury}}^{\text{BW}} \propto T_{\text{world}} \quad \text{(scales with world trade)}$$
$$D_{\text{Treasury}}^{\text{petro}} \propto p \cdot Q \quad \text{(scales with oil market value)}$$

World trade is diversified and broadly growing. Oil market value is concentrated and vulnerable to substitution. This is why the petrodollar system is structurally more fragile than Bretton Woods was — it depends on a single commodity, not on the whole economy.

---

## 5. The Stablecoin Treasury System — The GENIUS Act Mechanism

### The Mechanism (in words)

The GENIUS Act requires 100% Treasury backing for stablecoins. Every stablecoin minted forces a Treasury purchase. Treasury demand grows 1-for-1 with stablecoin supply.

### The Model

Let:
- $S(t)$: total stablecoin supply (in USD)
- $\delta$: legally mandated reserve ratio (under GENIUS Act, $\delta = 1.0$)
- $\tau$: fraction of reserves that must be held in Treasuries (versus cash at the Fed)

**Equation 13 — Treasury demand from stablecoin mandates.**

$$\boxed{D_{\text{Treasury}}^{\text{stable}}(t) = \tau \cdot \delta \cdot S(t) = \tau \cdot S(t)}$$

Since $\delta = 1$ by law, this simplifies to:

$$D_{\text{Treasury}}^{\text{stable}}(t) = \tau \cdot S(t)$$

This is **linear** and, compared to the previous two systems, *strikingly simple*. There's no complex recycling loop, no exchange rate dynamics, no commodity price volatility. It's a direct proportionality: more stablecoins $\implies$ more Treasuries, with coefficient $\tau \leq 1$.

**The coefficient $\tau$ deserves attention.** The GENIUS Act allows reserves to be held in either short-term Treasury bills or cash deposits at insured banks. In practice, Tether and Circle hold \$120B+ and \$30B+ in T-bills respectively, suggesting $\tau \approx 0.8$ or higher. If we assume $\tau = 0.8$:

$$D_{\text{Treasury}}^{\text{stable}} = 0.8 \cdot S(t)$$

For \$2 trillion in stablecoins: $D_{\text{Treasury}}^{\text{stable}} = \$1.6\text{T}$.

### Why This Is the Simplest Version

Compare the three demand equations side by side:

$$D_{\text{Treasury}}^{\text{BW}} = \theta \cdot \lambda \cdot T_{\text{world}}(t) \quad \text{(depends on } \theta, \lambda, T_{\text{world}}\text{)}$$

$$D_{\text{Treasury}}^{\text{petro}} = \eta \cdot (1-c) \cdot s \cdot p(t) \cdot Q(t) \quad \text{(depends on } \eta, c, s, p, Q\text{)}$$

$$D_{\text{Treasury}}^{\text{stable}} = \tau \cdot S(t) \quad \text{(depends on } \tau, S\text{)}$$

The stablecoin equation has the fewest parameters and the most direct causal link. There are no behavioral parameters ($\lambda$, "how much reserves do central banks want?"), no commodity market variables ($p$, $Q$), no savings rates ($c$). Just a legal mandate ($\delta = 1$), an allocation fraction ($\tau$), and the total stablecoin supply ($S$).

The reduction in parametric complexity is itself the insight: **the GENIUS Act eliminated the behavioral and market-driven uncertainty that made previous demand mechanisms variable.** It replaced "countries choose to hold reserves" and "OPEC chooses to recycle into Treasuries" with "the law requires it."

---

## 6. The Triffin Analogue for Stablecoins

### The Model

Under Bretton Woods, the Triffin Dilemma was: dollar demand grows exponentially, gold reserves are bounded, coverage ratio $\to 0$.

What's the analogous dynamic for stablecoins?

Let:
- $S(t)$: stablecoin supply (growing with on-chain economy)
- $D_{\text{total}}(t)$: total US debt outstanding
- $Y(t)$: US GDP
- $r$: average interest rate on debt
- $\rho(t) = \frac{D_{\text{total}}(t)}{Y(t)}$: debt-to-GDP ratio

Stablecoins contribute to debt *demand* (they buy Treasuries), but the Treasuries they buy are part of total US debt. So:

**Equation 14 — Stablecoin contribution to debt demand.**

$$D_{\text{Treasury}}^{\text{stable}}(t) = \tau \cdot S(t)$$

This is a fraction of total debt:

$$\text{Stablecoin share} = \frac{\tau \cdot S(t)}{D_{\text{total}}(t)}$$

**Equation 15 — Debt dynamics.** The US government's debt evolves as:

$$D_{\text{total}}(t+1) = D_{\text{total}}(t) + r \cdot D_{\text{total}}(t) + G(t) - \text{Tax}(t)$$

where $G(t) - \text{Tax}(t)$ is the primary deficit (spending minus revenue, before interest). This gives:

$$D_{\text{total}}(t+1) = (1+r) \cdot D_{\text{total}}(t) + \underbrace{G(t) - \text{Tax}(t)}_{\text{primary deficit } d(t)}$$

This is a **linear recurrence** in $D_{\text{total}}$, and with a positive primary deficit ($d > 0$) and $r > 0$, debt grows exponentially.

**The stablecoin Triffin question:** Does stablecoin-funded Treasury demand grow faster or slower than debt?

- If $S(t)$ grows faster than $D_{\text{total}}(t)$: stablecoins absorb an increasing share of new debt issuance — the system is *stabilizing*
- If $S(t)$ grows slower than $D_{\text{total}}(t)$: stablecoins absorb a shrinking share — the system is *destabilizing*

$$\boxed{\text{Stability condition: } \frac{\dot{S}}{S} > \frac{\dot{D}_{\text{total}}}{D_{\text{total}}}}$$

or equivalently: the growth rate of stablecoin supply must exceed the growth rate of total debt. If stablecoins grow at 30–50% per year (plausible for 2025–2030 from a \$250B base) and debt grows at 5–8% per year, the condition is *easily* satisfied in the near term. But stablecoin growth will eventually slow (all adoption curves saturate), while debt growth may not.

**The key difference from Bretton Woods:** Under Bretton Woods, the constraint was physical (gold reserves = fixed). Under stablecoins, the constraint is *confidence-based* (will people keep using stablecoins if they worry about the Treasuries backing them?). Confidence constraints are softer than physical constraints — they can be managed by central bank intervention, regulatory reassurance, and financial engineering. But they can also evaporate suddenly.

---

## 7. The Unified Framework — A Single Equation

All three systems, despite different historical contexts and mechanisms, can be written in a common form:

$$\boxed{D_{\text{Treasury}}(t) = \mu \cdot A(t)}$$

where:
- $D_{\text{Treasury}}(t)$ is structural Treasury demand at time $t$
- $A(t)$ is the **adoption variable** — the scale of the system whose participation requires dollar holdings
- $\mu$ is the **demand coefficient** — how many dollars of Treasury demand each unit of adoption generates

| System | $A(t)$ | $\mu$ |
|:---|:---|:---|
| Bretton Woods | $T_{\text{world}}$ (world trade volume) | $\theta \cdot \lambda$ |
| Petrodollar | $p \cdot Q$ (global oil bill) | $\eta \cdot (1-c) \cdot s$ |
| Stablecoin | $S$ (stablecoin supply) | $\tau$ |

The unified equation says: **structural Treasury demand is a linear function of how much of the world uses the system that requires dollar holdings.**

### The Growth Rate Decomposition

Taking logs and differentiating:

$$\frac{\dot{D}_{\text{Treasury}}}{D_{\text{Treasury}}} = \frac{\dot{\mu}}{\mu} + \frac{\dot{A}}{A}$$

The growth rate of Treasury demand equals the growth rate of the demand coefficient plus the growth rate of adoption.

For Bretton Woods: $\mu = \theta \lambda$ was roughly constant, so Treasury demand grew at the rate of world trade (~7%/year).

For Petrodollar: $\mu = \eta(1-c)s$ was roughly constant, but $A = p \cdot Q$ was volatile because oil prices are volatile. Treasury demand was spiky and unpredictable.

For Stablecoins: $\mu = \tau$ is legally fixed ($\delta = 1$, $\tau \approx 0.8$), and $A = S(t)$ is growing rapidly but smoothly. This system has the *most stable and predictable* demand generation.

### Why the Demand Coefficient Matters

The real evolution across the three systems isn't just in the adoption variable — it's in the *nature* of $\mu$:

- **Bretton Woods**: $\mu = \theta \cdot \lambda$. Both components are *behavioral*. $\lambda$ (how much reserve cover central banks want) is a choice. $\theta$ (how much of reserves go into Treasuries) is a choice. Countries could, and did, vary these.
- **Petrodollar**: $\mu = \eta \cdot (1-c) \cdot s$. Partially behavioral ($\eta$, choice to invest in Treasuries), partially structural ($s$, OPEC market share), partially behavioral ($c$, domestic spending rate). Multiple degrees of freedom.
- **Stablecoins**: $\mu = \tau \cdot \delta = \tau \cdot 1.0$. Here, $\delta$ is *legally mandated* (not a choice) and $\tau$ is constrained by the structure of Treasury markets (stablecoin issuers *want* T-bills for the yield and liquidity). The demand coefficient is essentially *fixed by law*.

$$\mu_{\text{BW}} = f(\text{behavioral choices}) \quad \to \quad \mu_{\text{petro}} = f(\text{market + behavioral}) \quad \to \quad \mu_{\text{stable}} = f(\text{law})$$

**Each successive system has reduced the degrees of freedom in the demand coefficient.** The demand becomes less voluntary, more mechanical, more predictable.

---

## 8. The Debt Sustainability Equation

### The Core Model

The question underlying all three systems is: **does the structural Treasury demand suppress borrowing costs enough to keep debt sustainable?**

Let:
- $\rho(t) = \frac{D_{\text{total}}(t)}{Y(t)}$: debt-to-GDP ratio
- $r$: real interest rate on government debt
- $g$: real GDP growth rate
- $d(t) = \frac{G(t) - \text{Tax}(t)}{Y(t)}$: primary deficit as a fraction of GDP

The standard debt sustainability equation (from any macro textbook) is:

$$\boxed{\Delta \rho \approx (r - g) \cdot \rho + d}$$

This says: the debt-to-GDP ratio increases when $(r - g) > 0$ (interest rate exceeds growth) and when the government runs a primary deficit ($d > 0$).

**Debt is sustainable if** $\Delta \rho \leq 0$, which requires:

$$d \leq (g - r) \cdot \rho$$

If $g > r$: the government can run a primary deficit and still see debt/GDP fall. This is the "grow out of debt" strategy.

If $r > g$: the government must run a primary *surplus* just to keep debt/GDP stable. This is austerity.

### How Structural Dollar Demand Affects $r$

Here's where the three systems connect to debt sustainability. Structural Treasury demand *suppresses $r$*. When there's a guaranteed buyer for Treasuries (central banks under Bretton Woods, OPEC under petrodollars, stablecoin issuers under GENIUS Act), the government doesn't need to offer high yields to attract buyers.

Let $r = r_0 - \sigma \cdot D_{\text{Treasury}}^{\text{structural}}$, where $r_0$ is the "natural" rate without structural demand and $\sigma > 0$ captures how much structural demand suppresses yields.

Then the debt sustainability equation becomes:

$$\Delta \rho \approx \Big(r_0 - \sigma \cdot \mu \cdot A(t) - g\Big) \cdot \rho + d$$

**Debt is stabilizing when:**

$$\boxed{\sigma \cdot \mu \cdot A(t) > r_0 - g + \frac{d}{\rho}}$$

In words: **structural Treasury demand (left side) must be large enough to push the effective interest rate below the growth rate by enough to offset the primary deficit.**

This is the *real* equation behind all three systems. The entire 80-year strategy reduces to: *engineer enough structural demand ($\mu \cdot A$) to keep the effective interest rate below the growth rate.*

### The Linearity Check

Is this equation linear? Let's see:
- $D_{\text{Treasury}} = \mu \cdot A(t)$ — **linear** in $A$
- $r = r_0 - \sigma \cdot \mu \cdot A(t)$ — **linear** in $A$
- $\Delta \rho = (r - g) \cdot \rho + d$ — **linear** in $r$ and $\rho$ *separately*, but the product $r \cdot \rho$ makes it **bilinear** (linear in each variable holding the other fixed, but not jointly linear)

So: the Treasury demand mechanism is linear. The interest rate suppression is linear. But the debt dynamics are **bilinear** — the interaction between interest rates and the debt stock creates a multiplicative term. This is the one nonlinearity in the system, and it's the reason debt dynamics can be self-reinforcing: higher debt means higher interest payments, which means more debt, which means higher interest payments...

However, over short time horizons (where $\rho$ changes slowly), the bilinear term is approximately linear. This is why the linear intuition is "almost right" — it captures the first-order effects correctly and only misses the second-order feedback that matters over decades.

---

## 9. Summary — Is It All Linear?

The user's intuition was: "all the important mechanisms in these boil down to perhaps a few very simple linear equations."

**Verdict: largely confirmed, with one important caveat.**

### What IS linear

| Mechanism | Equation | Linear? |
|:---|:---|:---|
| Gold standard self-correction | $\Delta G = (\bar{X} - \bar{Z}) - \gamma G$ | ✅ Linear (1st-order) |
| Bretton Woods reserve demand | $D^{\text{BW}} = \theta \lambda T_{\text{world}}$ | ✅ Linear |
| Petrodollar recycling | $D^{\text{petro}} = \eta(1-c) \cdot s \cdot pQ$ | ✅ Linear |
| Stablecoin mandate | $D^{\text{stable}} = \tau \cdot S$ | ✅ Linear |
| Interest rate suppression | $r = r_0 - \sigma \mu A$ | ✅ Linear |
| Unified demand equation | $D = \mu \cdot A$ | ✅ Linear |

### What is NOT linear

| Mechanism | Equation | Linear? |
|:---|:---|:---|
| Triffin Dilemma | $\phi = G_{\text{US}} / D_0 e^{gt}$ | ❌ Exponential decay |
| Debt dynamics | $\Delta \rho = (r-g)\rho + d$ | ❌ Bilinear ($r \times \rho$) |

The nonlinearities are *not* in the demand mechanisms — they're in the *constraints* (gold supply) and *feedback loops* (interest on debt). The demand side of every system is a simple proportionality. The complications arise when that demand interacts with something that doesn't scale the same way.

### The Punchline

$$\boxed{D_{\text{Treasury}} = \mu \cdot A(t)}$$

Eighty years. Three systems. One equation. The substrate changes ($T_{\text{world}} \to pQ \to S$). The demand coefficient evolves from behavioral to legal ($\theta\lambda \to \eta(1-c)s \to \tau$). But the structure is the same: **Treasury demand is a constant multiple of the scale of whatever system the US has engineered the world into using.**

The linearity is both the strength and the fragility of the strategy. Strength, because linear systems are predictable, scalable, and easy to engineer. Fragility, because the *nonlinear* failure modes (Triffin collapse, debt spiral) exist *outside* the linear model, and they strike when the linear approximation breaks down.

The math says: the strategy works until it doesn't. And when it stops working, it stops *fast* — because the failure is exponential, not linear.

---

*Companion to: [From Bretton Woods to the GENIUS Act](/blog/US_economy/bretton_woods/) | See also: [The US Debt Crisis \& The Stablecoin](/blog/US_economy/debt_stablecoin/)*
