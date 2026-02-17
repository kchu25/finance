@def title = "The Complete Risk Map of Aave: What Can Actually Kill Your Position"
@def published = "17 February 2026"
@def tags = ["crypto", "math", "finance"]

# The Complete Risk Map of Aave
## What Can Actually Kill Your Position — and What Can't

@@toc@@

---

## 1. Why This Post Exists

The [Aave LINK position case study](/blog/defi/aave_link_position/) lists risks in a summary
table. But a table isn't enough. Each risk has *layers* — probability, severity, correlation with
other risks, mitigations, and failure modes of those mitigations.

This post is a comprehensive audit. Every risk that could destroy an Aave position, ranked by
actual danger, with the math to back it up.

The question isn't "is Aave safe?" The question is: **is the expected value of using Aave
positive after accounting for all risks, and is the position sized correctly for those risks?**

---

## 2. The Risk Taxonomy

Every Aave risk falls into one of six layers. Each layer is independent — they can compound,
and some can trigger others.

| Layer | Risk | Who controls it? |
|:-----:|:-----|:----------------:|
| 1 | Smart contract risk | Nobody (code) |
| 2 | Oracle risk | Chainlink |
| 3 | Liquidation risk | Market + you |
| 4 | Interest rate risk | Market |
| 5 | Governance risk | AAVE token holders |
| 6 | Regulatory risk | Governments |

Let's examine each one in full.

---

## 3. Layer 1 — Smart Contract Risk

### What it is

Aave is code. Code can have bugs. If there's a vulnerability in Aave's smart contracts, an
attacker could drain funds — including your collateral.

This is the **existential risk**: the one that can cause total, unrecoverable loss.

### The track record

**Aave has never been exploited for user funds in its history.**

Check the [rekt.news leaderboard](https://rekt.news/leaderboard/) — a comprehensive list of
every major DeFi hack since 2020, totaling over \$10 billion in losses. Aave is not on it.

For context, here's what *has* been exploited:

| Protocol | Loss | Year |
|:---------|:----:|:----:|
| Ronin Network | \$624M | 2022 |
| Poly Network | \$611M | 2021 |
| Euler Finance | \$197M | 2023 |
| Compound | \$147M | 2021 |
| Cream Finance | \$130M + \$19M | 2021 |
| Hundred Finance | \$11M + \$7M | 2022-23 |
| Exactly Protocol | \$7.2M | 2023 |

Lending protocols *do* get hacked. Compound, Cream, Euler, Hundred — all exploited. But Aave,
despite being the largest DeFi lending protocol with **billions** in TVL since 2020, has not.

### Why Aave has survived

1. **Audit density.** Aave has been audited more times than almost any protocol in DeFi:
   - V2: Consensys Diligence, Certik, PeckShield, SigmaPrime (2020)
   - V3: ABDK, SigmaPrime, Certora (formal verification), PeckShield, Trail of Bits (2022)
   - V3.1 through V3.6: Continuous audits from Certora, MixBytes, Pashov, Oxorio, Sherlock
     contest, ABDK, StErMi, Blackthorn (2024-2025)

   This is not one audit. This is **dozens of audits** from different firms using different
   methodologies, over five years. Each version gets re-audited by multiple independent teams.

2. **Formal verification.** Certora has formally verified Aave's core invariants since V3.
   This isn't just "we read the code" — it's mathematical proof that certain properties hold
   under all possible inputs. This is the gold standard of smart contract security.

3. **Battle testing.** Aave has processed tens of billions in cumulative volume since 2020
   through multiple market crashes, governance attacks, and ecosystem-wide stress events. The
   contracts have been "fuzz-tested by reality."

4. **Bug bounty.** Aave runs an [Immunefi bug bounty](https://immunefi.com/bug-bounty/aave/)
   offering significant rewards for critical vulnerabilities. This economically incentivizes
   white-hat discovery over black-hat exploitation.

5. **Simplicity.** Aave's core lending logic is conceptually simple: deposit collateral, borrow
   against it, get liquidated if health factor drops below 1. There are no complex multi-hop
   strategies, flash loan composability traps, or exotic derivative pricing. Simpler code =
   smaller attack surface.

### The honest assessment

Despite all of this, smart contract risk is **never zero**. Every new version (V3.1, V3.2, ...,
V3.6, upcoming V4) introduces new code and new potential vulnerabilities. The audit-then-deploy
cycle reduces risk but doesn't eliminate it.

**Historical probability of Aave exploit: 0% (6 years, 0 exploits)**

**Bayesian estimate going forward: ~0.5–2% per year** — this accounts for the base rate of
lending protocol exploits in DeFi (several per year across the ecosystem), discounted by Aave's
superior security practices.

### What it would look like

If Aave *were* exploited:
- **Best case:** A contained exploit affecting one market or one chain deployment (Aave deploys
  across Ethereum, Polygon, Arbitrum, Optimism, Avalanche, Base, etc.). Loss is limited to that
  deployment.
- **Worst case:** A fundamental logic bug in the core lending contracts that allows draining of
  all pools. Total loss of deposited collateral.
- **The Umbrella backstop:** Aave now has an "Umbrella" safety module worth ~\$247M in staked
  assets that acts as a backstop for protocol insolvency. This wouldn't cover a catastrophic
  drain but would cover bad debt from liquidation failures.

### Mitigation in the position

The [case study](/blog/defi/aave_link_position/) puts only **28% of total LINK** on Aave. If
the protocol is fully drained:
- **Loss:** 28% of total LINK holdings
- **Surviving:** 72% in cold storage, untouchable
- **Recovery:** Still hold the vast majority of the position

This is the correct approach. Never put 100% of any asset on any single protocol, no matter how
well-audited.

---

## 4. Layer 2 — Oracle Risk

### What it is

Aave doesn't know the price of LINK on its own. It relies on **Chainlink price feeds** — external
oracles that report asset prices to the smart contract. If the oracle reports a wrong price,
catastrophic things happen:

- **Oracle reports price too low** → Healthy positions get liquidated unfairly
- **Oracle reports price too high** → Borrowers can extract more than their collateral is worth
  (bad debt for the protocol)
- **Oracle goes stale** → Prices stop updating, positions can't be liquidated or managed

### The irony

Here's the recursive beauty: **you're collateralizing LINK on a protocol that uses Chainlink
to price LINK.** Your collateral asset *is* the oracle infrastructure securing your position.

If Chainlink fails, your Aave position has problems — but so does most of DeFi, and the
price of LINK itself would likely collapse. The risks are correlated but in a way that's
hard to exploit.

### Chainlink's track record

Chainlink price feeds have been operational since 2019 and currently secure over **\$75 billion**
in smart contract value across DeFi. They have not suffered a major manipulation or failure
event affecting Aave.

How they work:
1. Multiple independent node operators (not just one) report prices
2. Prices are aggregated (median) to eliminate outliers
3. Deviation thresholds trigger updates (typically 0.5–1% for major assets)
4. Heartbeat mechanism ensures periodic updates even in stable markets
5. Circuit breakers halt feeds if anomalies are detected

### What could go wrong

1. **Node operator collusion.** If a majority of Chainlink nodes collude to report a false price,
   the oracle would be compromised. This is theoretically possible but requires coordinating
   dozens of independent, reputable operators (many of whom are institutional — Deutsche Telekom,
   Swisscom, etc.).

2. **Flash crash / extreme volatility.** If LINK drops 50% in minutes, oracle updates might
   lag real market prices. This could delay liquidations, creating bad debt. Aave's liquidation
   mechanism handles this through bonus incentives for liquidators, but extreme speed matters.

3. **Feed deprecation.** Chainlink could deprecate the LINK/USD feed. This is practically
   impossible since LINK is Chainlink's own token and one of the most widely used feeds in DeFi.

4. **L1 congestion.** On Ethereum mainnet, extreme gas prices during crashes can delay oracle
   updates and liquidation transactions. This was a real problem during March 2020 (Black
   Thursday) — MakerDAO suffered \$6M in bad debt because liquidation bots couldn't get
   transactions through. Aave has since added L2 deployments and improved liquidation mechanisms
   to mitigate this.

### Probability and severity

| Scenario | Probability | Impact on position |
|:---------|:----------:|:------------------:|
| Oracle stale for >1 hour | Low | Moderate (delayed liquidation in crash) |
| Oracle reports wrong price (temporary) | Very low | Low-High (depends on direction) |
| Oracle permanently compromised | Negligible | Critical (but would destroy all of DeFi) |
| L1 congestion delays updates | Medium (during crashes) | Low-Moderate |

### Mitigation

- **Use Ethereum mainnet or mature L2s** where Chainlink feeds are most robust
- **The LINK-specific advantage:** LINK is one of Chainlink's highest-priority feeds. It will
  never be the last feed to get updated or the first to be deprecated
- **The position's HF buffer of 2.15** means even a significant oracle lag during a crash
  leaves substantial room before liquidation

---

## 5. Layer 3 — Liquidation Risk

### What it is

If the health factor drops below 1.0, anyone can call the liquidation function and buy your
collateral at a discount. This is the most *visible* risk and the one most people fixate on.

### How Aave liquidation works

When HF < 1.0:

1. A **liquidator** (usually a bot) repays up to 50% of your debt
2. In exchange, the liquidator receives collateral worth the debt repaid **plus a liquidation
   bonus** (typically 5–10% for LINK)
3. Your position is partially closed — you keep the remaining collateral minus the penalty

**Key insight: liquidation is not total loss.** You lose the liquidation bonus (5–10% of the
liquidated portion), not your entire collateral. In a partial liquidation:

$$\text{Loss} = \text{Debt Repaid} \times \text{Liquidation Bonus} = 0.5 \times D_{\text{new}} \times 0.05 = 0.025 \times D_{\text{new}}$$

That's a 2.5% penalty on your total debt, not a wipeout. After partial liquidation, your
health factor improves and the remaining position survives.

### When liquidation becomes total loss

Full liquidation occurs when:
1. HF drops **far** below 1.0 (deep underwater)
2. The collateral value minus liquidation bonus is less than the debt
3. Multiple partial liquidations cascade

This requires an extreme, rapid crash where:
- LINK drops 53%+ from entry
- No collateral is added from reserves
- No partial debt repayment is made

### The position's defense

From the [case study](/blog/defi/aave_link_position/):

| Defense Layer | Details |
|:-------------|:--------|
| Health Factor | 2.15 (53% buffer) |
| Cold storage reserve | 72% of total LINK available to add as collateral |
| Debt ratchet | Systematic debt reduction at each price doubling |
| Monitoring | On-chain position is publicly visible 24/7 |

The position would require LINK to drop 53% *and* complete inaction to face liquidation.
With cold storage reserves, the effective liquidation threshold is much lower — closer to a
70-80% crash with paralysis.

### Historical context

LINK's worst drawdowns:

| Period | Peak to Trough | Duration |
|:-------|:--------------:|:--------:|
| Jan 2018 → Dec 2018 | −94% | 12 months |
| May 2021 → Jun 2022 | −89% | 13 months |
| Nov 2021 → Jun 2022 | −82% | 7 months |

Yes, LINK *has* dropped more than 53%. But these were peak-to-trough drawdowns over months —
not sudden crashes. A slow grind down gives time to add collateral. The dangerous scenario is a
**sudden** 53%+ crash with no time to react.

**Has LINK ever dropped 53% in a single day?** No. The worst single-day drop was ~30% (during
May 2021 and March 2020). A 53% single-day crash would require an event worse than any in
LINK's history.

### Honest risk assessment

Liquidation risk is **real but manageable** for this position because:
1. The buffer (53%) exceeds any historical single-day drop
2. Cold storage reserves provide emergency collateral
3. Slow grinds (like 2022 bear market) give weeks/months to react
4. Partial liquidation is painful but not fatal

---

## 6. Layer 4 — Interest Rate Risk

### What it is

Aave uses **variable interest rates**. The 3.8% borrow rate for USDC is not fixed — it changes
based on utilization (how much of the USDC pool is borrowed).

### How rates change

Aave uses a **kinked rate model**:

$$r = \begin{cases} r_0 + \frac{U}{U_{\text{optimal}}} \times r_{\text{slope1}} & \text{if } U \leq U_{\text{optimal}} \\[6pt] r_0 + r_{\text{slope1}} + \frac{U - U_{\text{optimal}}}{1 - U_{\text{optimal}}} \times r_{\text{slope2}} & \text{if } U > U_{\text{optimal}} \end{cases}$$

Where:
- $U$ = current utilization (borrowed / total supplied)
- $U_{\text{optimal}}$ = target utilization (typically 80-90% for stablecoins)
- $r_{\text{slope1}}$ = gradual rate increase below optimal
- $r_{\text{slope2}}$ = steep rate increase above optimal (the "kink")

**Below optimal utilization:** Rates rise gradually. At 80% utilization, USDC might be ~4%.

**Above optimal utilization:** Rates spike. At 95% utilization, rates could hit 20-50%+. This
is by design — it incentivizes repayment and discourages excessive borrowing.

### What rate spikes look like

| Utilization | Approximate USDC Rate | Impact |
|:-----------:|:---------------------:|:------:|
| 50% | 2-3% | Very cheap |
| 70% | 3-4% | Cheap |
| 80% | 4-5% | Normal |
| 85% | 5-8% | Elevated |
| 90% | 8-15% | Expensive |
| 95% | 20-50% | Painful |
| 99% | 50-100%+ | Emergency |

### Does rate risk kill the position?

**No.** Here's why:

1. **Rate spikes are temporary.** When rates spike, borrowers repay and suppliers flood in.
   The utilization drops, and rates normalize. This is the self-correcting mechanism. Sustained
   rates above 10% are rare (days, not months).

2. **Rate ≠ liquidation.** High borrow rates increase carrying cost. They do *not* reduce
   your health factor. You won't get liquidated because rates spike. You'll just pay more
   interest.

3. **The math still works at higher rates.** The [sensitivity analysis](/blog/defi/borrowed_link_growth/)
   showed that even at 5% average borrow rate (vs 3.8% current), the position remains
   overwhelmingly positive as long as LINK appreciates more than 5%/yr.

4. **You can repay during spikes.** If rates hit 15%+, partially repay debt to reduce carrying
   cost. When rates normalize, borrow again. This is annoying but not dangerous.

### The real cost of rate volatility

Assume rates average 5% instead of 3.8% over 25 years (realistic given historical fluctuations):

$$\text{Extra annual cost} = D_{\text{new}} \times (0.05 - 0.038) = D_{\text{new}} \times 0.012$$

That's 1.2% of the debt per year in additional interest. On a position where the asset is
expected to appreciate 10-50% annually, this is noise.

**Interest rate risk severity: Low.** It affects returns at the margin. It does not threaten
the position's survival.

---

## 7. Layer 5 — Governance Risk

### What it is

Aave is governed by AAVE token holders who can vote on protocol changes. These changes can
affect your position directly:

- Changing liquidation thresholds for LINK
- Changing interest rate parameters
- Deprecating LINK as collateral
- Adding new risk parameters
- Freezing or pausing markets

### Why this matters

A governance vote could *theoretically*:
1. **Lower LINK's liquidation threshold** from 0.71 to, say, 0.50. This would instantly reduce
   your health factor from 2.15 to ~1.51. Still safe, but buffer drops from 53% to ~34%.

2. **Freeze LINK market.** No new borrows against LINK. Existing positions remain but can't be
   modified. This has happened to other assets (certain stablecoins, low-liquidity tokens).

3. **Deprecate LINK.** Force users to migrate positions or face suboptimal parameters. This is
   extreme and unlikely for a major asset like LINK.

### Historical precedent

Aave governance has made parameter changes many times:
- CRV parameters were tightened after the November 2022 Avi Eisenberg manipulation attempt
- Various low-cap assets have been frozen or deprecated
- Liquidation bonuses and thresholds have been adjusted for risk management

But LINK is a **core collateral asset** — top-10 in TVL, deeply liquid, with the strongest
oracle infrastructure in DeFi (since Chainlink runs the oracles). It would be one of the
*last* assets to face adverse parameter changes.

### The CRV incident — a case study in governance risk

In November 2022, Avi Eisenberg attempted to manipulate the CRV market on Aave. He:
1. Borrowed heavily against CRV collateral
2. Tried to short CRV on DEXs to profit
3. CRV didn't crash as expected
4. His position was liquidated but left ~\$1.6M in bad debt for Aave

**What happened next:**
- Aave governance tightened CRV parameters (lower LTV, higher liquidation bonus)
- The Aave treasury and safety module absorbed the bad debt
- No regular users lost funds
- The protocol demonstrated its resilience

**The lesson:** Governance can and does change parameters in response to risk events. This is
actually *good* — it shows active risk management. But it means your position parameters are
not guaranteed to remain constant.

### Mitigation

- LINK is a blue-chip collateral asset — parameter changes will be gradual and well-telegraphed
- Governance proposals require multi-day voting periods — you have time to react
- The position's conservative LTV (33.1%) means even significant parameter tightening leaves
  a comfortable buffer
- Follow [Aave governance forum](https://governance.aave.com/) for proposals affecting LINK

---

## 8. Layer 6 — Regulatory Risk

### What it is

Governments could:
1. Ban DeFi lending in your jurisdiction
2. Require KYC for DeFi protocols
3. Sanction Aave's smart contracts (like Tornado Cash)
4. Tax DeFi positions aggressively
5. Restrict on/off-ramps between fiat and crypto

### Current landscape

As of February 2026:
- The US has moved toward clearer crypto regulation (MiCA-equivalent frameworks under discussion)
- The EU's MiCA framework is in effect, creating regulatory clarity for DeFi in Europe
- Aave has not been targeted by any sanctions or enforcement actions
- The GENIUS Act is progressing through Congress, focusing primarily on stablecoins

### The Tornado Cash precedent

In August 2022, the US Treasury sanctioned Tornado Cash smart contracts. This was unprecedented —
sanctioning *code*, not a person or company. However:
- Tornado Cash was a mixer specifically designed for anonymity
- Aave is a *lending protocol* — fundamentally different use case
- Aave has governance, a known development team, and legitimate institutional users (JPMorgan,
  Fireblocks, etc. are listed as building on Aave)
- Sanctioning Aave would affect billions in legitimate economic activity

### What regulation could look like

| Scenario | Probability | Impact | Mitigation |
|:---------|:----------:|:------:|:-----------|
| KYC requirement for frontends | Medium | Low | Use contract directly, no frontend needed |
| Tax reporting requirements | High | Low | Already tracking for tax purposes |
| On/off-ramp restrictions | Medium | Medium | Can unwind position if needed |
| Protocol sanctions | Very low | High | Withdraw before enforcement |
| Complete DeFi ban | Negligible | Critical | Protocol exists on-chain regardless |

### The key insight

Regulatory risk is **slow-moving**. Laws don't appear overnight. There are proposal periods,
comment periods, legal challenges, and implementation delays. A well-monitored position can
be unwound long before any regulation takes effect.

**Regulatory risk severity: Low to Medium.** It's real, but the speed of government action
vs. the speed of on-chain withdrawal heavily favors the user.

---

## 9. The Correlated Risks — What Kills You

Individual risks are manageable. **Correlated risks** are dangerous. Here are the scenarios
where multiple risks compound:

### Scenario A — Market crash + gas spike + oracle lag

1. LINK drops 40% in hours (crypto bear event)
2. Ethereum gas spikes to 500+ gwei (everyone rushing to manage positions)
3. Chainlink oracle updates lag by minutes
4. Health factor drops below 1.0 based on real market price, but oracle still shows old price
5. When oracle updates, cascade of liquidations

**Probability:** Low (has elements of March 2020 Black Thursday)

**Impact:** Partial liquidation with penalty, not total loss

**Mitigation:** Use L2 deployments (lower gas), maintain large HF buffer, keep cold storage reserves

### Scenario B — Governance attack + market manipulation

1. Attacker accumulates large AAVE governance position
2. Proposes malicious parameter change (e.g., set LINK liquidation threshold to 0)
3. Executes governance attack

**Probability:** Very low. Aave governance has timelocks, guardians, and requires significant
capital to pass proposals. The Aave DAO also has a "Guardian" multisig that can veto malicious
proposals.

**Mitigation:** Governance proposals are visible days in advance. Exit before execution.

### Scenario C — Smart contract exploit + total loss

1. Zero-day vulnerability in Aave V3 core contracts
2. Attacker drains all pools before anyone can react
3. Total loss of collateralized LINK

**Probability:** Very low (~0.5-2% per year, decreasing over time)

**Impact:** Loss of 28% of LINK (only the portion on Aave)

**Mitigation:** This is exactly why only 28% is on Aave. The 72% in cold storage survives.

### Scenario D — Regulatory + market crash + rate spike

1. Major regulatory announcement (e.g., US bans DeFi lending)
2. Crypto market crashes 40%+ on the news
3. Aave borrow rates spike as users rush to unwind
4. Gas prices surge, making transactions expensive
5. LINK HF drops into danger zone

**Probability:** Very low

**Mitigation:** Monitor regulatory news, maintain cold storage reserves, keep gas ETH ready
for emergency transactions

---

## 10. Risk-Adjusted Expected Value

The final question: **after all risks, is the position worth it?**

### The expected loss calculation

| Risk | Prob/yr | Loss if occurs | Expected annual loss |
|:-----|:-------:|:--------------:|:--------------------:|
| Smart contract exploit | 1% | 28% of LINK | 0.28% of total LINK |
| Liquidation (no mitigation) | 0.5% | 5-10% of collateral | 0.014-0.028% of total LINK |
| Adverse governance change | 2% | 0% (just exit) | ~0% (can react) |
| Regulatory disruption | 1% | 0% (just exit) | ~0% (can react) |
| Oracle failure | 0.1% | Variable | ~0.01% of total LINK |

**Total expected annual loss: ~0.3% of total LINK**

### The expected gain

From the [case study](/blog/defi/aave_link_position/):

- Leveraged exposure adds ~28% × LTV × (LINK growth − borrow rate) in additional returns
- At 25% LINK growth and 3.8% borrow rate: incremental gain = 28% × 33.1% × (25% − 3.8%)
  = 28% × 33.1% × 21.2% = **1.96% additional annual return** on total portfolio

### The ratio

$$\frac{\text{Expected gain}}{\text{Expected loss}} = \frac{1.96\%}{0.3\%} = 6.5\times$$

**The expected value is positive by a factor of 6.5.** Even if we double the risk estimates
(2% exploit probability, higher liquidation risk), the ratio remains above 3×.

### When the position *doesn't* make sense

The strategy fails if:
1. **Smart contract risk is much higher than estimated** (>5% per year) — possible for new,
   unaudited protocols, but unlikely for Aave
2. **LINK growth is below the borrow rate long-term** — this means the fundamental thesis is
   wrong, not just the Aave strategy
3. **Too much capital on Aave** — putting 80%+ on protocol defeats the risk management framework
4. **No cold storage reserves** — inability to add collateral in a crash makes liquidation risk
   dramatically worse
5. **No monitoring** — positions left unmanaged for months during volatile markets

---

## 11. The Verdict

### What the position gets right

| Decision | Why it's correct |
|:---------|:----------------|
| Only 28% on Aave | Limits smart contract exposure to survivable loss |
| 72% cold storage | Emergency collateral + protocol failure insurance |
| LTV of 33.1% (HF 2.15) | 53% buffer exceeds any historical single-day LINK crash |
| Borrowing USDC (stablecoin) | No liquidation risk from debt asset appreciating |
| Using Chainlink-secured protocol | Best oracle infrastructure in DeFi |
| Variable rate (not leveraged tokens) | No auto-liquidation, no funding rate blowups |
| 25-year time horizon | Can survive multiple bear markets |
| Debt ratchet strategy | Systematic de-risking on each leg up |

### What to watch

| Signal | Action |
|:-------|:-------|
| Aave governance proposal changing LINK parameters | Review, potentially reduce position |
| USDC borrow rate sustained above 10% | Partially repay to reduce carrying cost |
| LINK drops 30%+ | Monitor closely, prepare to add collateral |
| LINK drops 40%+ | Add collateral from cold storage |
| Major DeFi exploit (any protocol) | Audit Aave exposure, consider reducing |
| Regulatory announcement targeting DeFi | Begin unwinding if legislation is credible |
| Aave V4 migration | Wait for full audit cycle before migrating |

### The bottom line

Aave is the most battle-tested lending protocol in DeFi. Six years of operation, billions in
TVL, dozens of audits, zero user fund exploits, formal verification, and a \$247M safety
backstop.

The risks are real:
- Smart contract risk: **~1% per year**, mitigated by 28% allocation cap
- Liquidation risk: **manageable** with 53% buffer and cold storage reserves
- Rate risk: **noise** on a 25-year horizon
- Governance risk: **visible and slow-moving** — you can react
- Regulatory risk: **slow-moving** — you can exit
- Oracle risk: **low** — Chainlink is the gold standard, and you're collateralizing the
  oracle's own token

**The position is well-structured.** The strategy doesn't eliminate risk — it *sizes* risk
correctly. The 28/72 split between Aave and cold storage is the key architectural decision.
It transforms smart contract risk from "existential" to "painful but survivable."

The expected value is strongly positive. The risks are understood, quantified, and mitigated.
The position is sound.

---

## Related

- [Case Study: A Conservative Aave LINK Position](/blog/defi/aave_link_position/) — the position this post evaluates
- [The Mathematics of Debt](/blog/finance/debt_finance/) — Kelly criterion framework
- [The Perpetual Debt Playbook](/blog/finance/perpetual_debt/) — managing no-maturity DeFi loans
- [Why Keeping Debt Feels Wrong But Is Right](/blog/finance/debt_intuition/) — five mental models
- [Inflation Is a Debt Eraser](/blog/finance/inflation_debt/) — why inflation favors borrowers
