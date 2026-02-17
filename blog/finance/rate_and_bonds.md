@def title = "Interest Rates and Bond Markets: The Inverse Dance"
@def published = "1 February 2026"
@def tags = ["macro"]

# Interest Rates and Bond Markets: The Inverse Dance

## The Core Relationship

When interest rates rise, bond prices fall. When rates fall, bond prices rise. This is the fundamental inverse relationship.

**Why?** Simple: if you're holding a bond paying 3% and new bonds are issued at 5%, yours is less attractive. Its price drops until its effective yield matches the market.

## The Math Behind It

### Basic Bond Pricing Formula

The price of a bond is the present value of all future cash flows:

$$P = \sum_{t=1}^{n} \frac{C}{(1+r)^t} + \frac{F}{(1+r)^n}$$

Where:
- $$P$$ = Bond price
- $$C$$ = Coupon payment
- $$r$$ = Current market interest rate (yield)
- $$F$$ = Face value
- $$n$$ = Number of periods until maturity

### What Happens When Rates Change?

**Example:** You own a 10-year bond with:
- Face value: \$1,000
- Coupon rate: 4% (\$40/year)
- Originally issued when market rates were 4%

**Scenario 1: Rates rise to 5%**

$$P = \sum_{t=1}^{10} \frac{40}{(1.05)^t} + \frac{1000}{(1.05)^{10}} \approx \$922$$

Your bond is now worth **~\$922** (down \$78 or 7.8%)

**Scenario 2: Rates fall to 3%**

$$P = \sum_{t=1}^{10} \frac{40}{(1.03)^t} + \frac{1000}{(1.03)^{10}} \approx \$1,085$$

Your bond is now worth **~\$1,085** (up \$85 or 8.5%)

## Duration: The Sensitivity Measure

**Duration** tells you approximately how much a bond's price will change for a 1% rate move.

$$\text{Duration} = \frac{\sum_{t=1}^{n} t \cdot \frac{C}{(1+r)^t} + n \cdot \frac{F}{(1+r)^n}}{P}$$

**Rule of thumb:**
$$\Delta P \approx -\text{Duration} \times \Delta r \times P$$

**Example:** A bond with duration of 7 years and price of \$1,000:
- If rates rise 1%, price drops: $$-7 \times 0.01 \times \$1,000 = -\$70$$
- If rates fall 0.5%, price rises: $$-7 \times (-0.005) \times \$1,000 = +\$35$$

## Government Refinancing Impact

### When Governments Need to Refinance

If a government issued bonds at 2% and now must refinance at 5%:

**Old debt:** \$1 billion at 2% = \$20 million/year in interest
**New debt:** \$1 billion at 5% = \$50 million/year in interest

**Cost increase:** \$30 million/year (150% more!)

### Market-Wide Effects

1. **Outstanding bonds lose value:** Existing 2% bonds trade at steep discounts
2. **Investor losses:** Bondholders see portfolio values drop
3. **Fiscal pressure:** Government budgets strained by higher interest costs
4. **Crowding out:** Higher government borrowing costs can push up all rates

## The Takeaway

The bond market is essentially a giant seesaw:
- **Rates up** → Bond prices down → Governments pay more to refinance
- **Rates down** → Bond prices up → Governments save on borrowing costs

The longer the maturity, the bigger the swing (higher duration = higher sensitivity).

This is why central banks move carefully—every rate change ripples through trillions in outstanding bonds.