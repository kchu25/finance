@def title = "stake.link Tutorial Guide"
@def published = "2 December 2025"
@def tags = ["chainlink", "crypto"]

# stake.link Tutorial Guide

## What is stake.link?

stake.link is a liquid staking platform for the Chainlink ecosystem that allows you to stake LINK tokens while maintaining liquidity. Built by a consortium of 15 top-tier Chainlink node operators, it has evolved into the first on-chain Liquid Staking Token (LST) Index, now supporting both Chainlink (stLINK) and Polygon (stPOL).

### Key Benefits

- **Liquid Staking**: Receive stLINK tokens that represent your staked position
- **Auto-Compounding Rewards**: Your stLINK balance automatically increases through a rebasing mechanism (approximately every 2 days)
- **DeFi Composability**: Use stLINK across DeFi protocols while earning staking rewards
- **Faster Withdrawals**: Unstake in 1-7 days (sometimes instantly) vs. the native 28-day cooldown period
- **Higher Yields**: Access to exclusive Node Operator Pool rewards not available in standard community staking
- **Non-Custodial**: You maintain full control of your tokens through smart contracts

## Prerequisites

Before you start staking on stake.link, you'll need:

1. **LINK Tokens**: Purchase LINK from an exchange (Binance, Coinbase, Kraken, etc.)
2. **Ethereum Wallet**: MetaMask, Ledger, Trezor, or Trust Wallet that supports Ethereum
3. **ETH for Gas Fees**: A small amount of ETH to pay for transaction fees
4. **Web3 Connection**: Your wallet should be able to connect to web3 applications

### Using Hardware Wallets (Trezor/Ledger)

**Trezor and Ledger are fully compatible and recommended for maximum security!**

To use a hardware wallet with stake.link:
1. Install MetaMask browser extension
2. Connect your Trezor/Ledger to MetaMask ("Connect Hardware Wallet" option)
3. Select your Ethereum account
4. Connect to stake.link using MetaMask (secured by your hardware wallet)
5. All transactions require physical confirmation on your device

Your private keys never leave your hardware wallet - MetaMask just acts as an interface while your Trezor/Ledger does the actual signing.

## Step-by-Step Staking Guide

### Step 1: Prepare Your Wallet

1. Install and set up MetaMask (or your preferred wallet)
2. Transfer LINK tokens from your exchange to your wallet
3. Ensure you have some ETH for gas fees (0.01-0.05 ETH should be sufficient)

### Step 2: Connect to stake.link

1. Visit [stake.link](https://stake.link/)
2. Click "Connect Wallet" in the top right corner
3. Select your wallet provider (MetaMask, WalletConnect, etc.)
4. Approve the connection request in your wallet

### Step 3: Navigate to Stake LINK

1. Once connected, go to the "Stake LINK" section
2. You'll see your current LINK balance displayed
3. Review the current APY (Annual Percentage Yield) shown on the interface

### Step 4: Choose Your Staking Option

**Priority Pool Option:**
- Check the "Priority Pool" box for potentially faster staking
- The Priority Pool queues your LINK and stakes it when space becomes available in the native Chainlink pool
- This option helps you get around the filled community staking pool

### Step 5: Enter Staking Amount

1. Enter the amount of LINK you want to stake
2. Leave some LINK or ETH for future gas fees
3. Review the estimated stLINK you'll receive (typically 1:1 ratio)

### Step 6: Approve and Deposit

1. Click "Approve" to allow the smart contract to interact with your LINK
   - This is a one-time approval transaction
   - Confirm the transaction in your wallet
   - Wait for confirmation (1-2 minutes)

2. Click "Deposit" to stake your LINK
   - Review the transaction details
   - Confirm in your wallet
   - Wait for the transaction to complete

### Step 7: Receive stLINK

- Once the transaction completes, you'll receive stLINK tokens in your wallet
- stLINK represents your staked position
- Your stLINK balance will automatically increase as rewards accrue (rebasing occurs approximately every 2 days)

**Important: What Actually Happens to Your Tokens**

When you stake on stake.link:
- Your LINK tokens are **sent to the stake.link smart contract** (they leave your wallet)
- In return, you receive **stLINK tokens back to your wallet**
- The stLINK tokens represent your claim to the staked LINK plus rewards
- You maintain custody through the stLINK tokens - the protocol is non-custodial (no company controls them)
- You can unstake anytime by converting stLINK back to LINK

Think of it like exchanging dollars for a receipt at a coat check - your original LINK goes into the staking pool, but you get liquid stLINK tokens that you control and can trade/use anywhere.

## Using Your stLINK

### Hold for Rewards
Simply hold stLINK in your wallet and watch your balance grow as rewards automatically compound.

### DeFi Integration
Use stLINK in other DeFi protocols:
- **Curve Finance**: Provide liquidity in the stLINK/LINK pool
- **Lending Protocols**: Use stLINK as collateral
- **DEX Trading**: Trade stLINK on decentralized exchanges

### Track Your Position
- Visit stake.link to view your staked amount
- Monitor your rewards accumulation
- Check current APY rates

## Unstaking Your LINK

### Option 1: Instant Swap
- Swap stLINK back to LINK on a DEX (may involve a small premium/discount)
- Immediate liquidity with no waiting period

### Option 2: Protocol Withdrawal
1. Go to stake.link and connect your wallet
2. Navigate to the "Unstake" section
3. Enter the amount of stLINK to withdraw
4. Submit the withdrawal request
5. Wait for processing (typically 1-7 days)
6. Complete the withdrawal once the cooldown period ends

## Understanding Rewards

### How Rewards Work
- Staking rewards come from the Chainlink staking pools
- stake.link aggregates rewards from both Community Pool and Node Operator Pool
- The displayed APY is the **net rate after all fees**

### Fee Structure
- **Protocol Fees**: A portion goes to SDL stakers (stake.link's governance token holders)
- **Delegation Fees**: Node operators receive fees for providing staking capacity
- **Your Net Yield**: The APY shown on the website is what you actually earn

### Reward Distribution
- Rewards are distributed through rebasing
- Your stLINK balance increases proportionally every ~2 days
- No manual claiming required
- Rewards auto-compound for maximum efficiency

## SDL Token (Optional)

stake.link has a native governance token called SDL:

- **Governance Rights**: Vote on protocol proposals
- **Revenue Sharing**: SDL stakers receive a share of protocol fees
- **Not Required**: You don't need SDL to stake LINK
- **Optional Enhancement**: Holding SDL can provide additional benefits

## Safety and Security

### How stake.link is Different from Centralized Platforms

**NOT Like BlockFi/Celsius/FTX:**

stake.link is fundamentally different from failed centralized platforms:

| Centralized Platforms (BlockFi) | stake.link (DeFi) |
|--------------------------------|-------------------|
| Company controls your funds | Smart contracts control funds |
| Lent crypto to risky borrowers | Direct staking in Chainlink contracts |
| Made bad business decisions | No lending or trading with your funds |
| Bankruptcy = you lose everything | Protocol continues even if company disappears |
| Opaque operations | Transparent, open-source code |

**Key Difference**: Your LINK goes directly to Chainlink's official staking contracts, not to a company that can mismanage it. If stake.link the company disappeared tomorrow, your stLINK still works and is backed by real LINK in Chainlink's contracts.

### Security Measures

**Multiple Security Audits:**
- Audited by five leading security firms: CodeHawks, Cyfrin, Sigma Prime, Trust Security, and Zellic
- All contracts are open-source and publicly verifiable

**Active Security Monitoring:**
- 24/7 real-time threat monitoring with Hypernative
- Bug bounty program with Immunefi offering up to \$100,000 for critical findings
- Continuous security assessments

**Governance Protection:**
- Critical operations secured by 6-of-8 multi-signature wallet
- Requires at least six independent approvals for any significant transaction
- Built by consortium of 15 top-tier Chainlink node operators

**Track Record:**
- Operating since 2022 with no major security incidents
- Over \$100 million in total value locked
- Battle-tested for 2+ years

### Smart Contract Audits
- stake.link contracts have been audited by reputable firms
- The protocol is built by experienced Chainlink node operators

### Risk Assessment

**Risk Level: Low-Medium** (significantly lower than centralized platforms)

**What This Protocol Does Well:**
- ✅ No counterparty risk from bad lending decisions
- ✅ Transparent, audited smart contracts
- ✅ Proven 2+ year track record
- ✅ Strong security infrastructure
- ✅ Decentralized operation

**Remaining Risks:**
- ⚠️ Smart contract bugs (minimized but not eliminated by audits)
- ⚠️ Oracle manipulation (very unlikely given Chainlink's reputation)
- ⚠️ Governance attacks (mitigated by multisig)
- ⚠️ Market/liquidity risk in extreme conditions

**NOT at Risk From:**
- ❌ Company bankruptcy
- ❌ Misuse of funds for risky loans
- ❌ Founder fraud or exit scams
- ❌ FTX/BlockFi-style collapse

### Understanding Your Actual Risk

**Your Trezor Protects:**
- ✅ Your stLINK tokens from wallet hackers
- ✅ Your private keys (never leave the device)
- ✅ Transaction signing security

**Your Trezor CANNOT Protect:**
- ❌ Smart contract vulnerabilities in stake.link's code
- ❌ The underlying LINK held in staking contracts
- ❌ DeFi protocol-level risks

**Important Clarification**: When you stake, your actual LINK tokens are held in smart contracts, not your wallet. Your Trezor securely holds the stLINK tokens (the "receipt"), but if the smart contract holding the LINK gets exploited, your stLINK could lose value even though it's safely in your cold wallet.

Think of it this way:
- **Trezor = Safe in your home** (protects your receipt from theft)
- **Smart contract = Bank vault** (where your actual LINK is stored)
- If the bank vault is compromised, your receipt becomes worthless regardless of how secure your home safe is

### Risk Considerations
- **Smart Contract Risk**: As with all DeFi, smart contract vulnerabilities exist
- **Market Risk**: LINK price can fluctuate
- **Slashing Risk**: Minimal (node operators bear most slashing risk)
- **Liquidity Risk**: stLINK/LINK ratio can vary slightly on secondary markets

### Best Practices
- Start with a small amount to test the process
- Never share your seed phrase or private keys
- Always verify you're on the official stake.link website
- Keep your wallet software updated

## Should You Stake? Pros and Cons

### Pros of Staking on stake.link

**Financial Benefits:**
- **Earn Passive Income**: Generate yield on LINK you'd otherwise just hold (typically 4-7% APY)
- **Auto-Compounding**: Rewards automatically compound every ~2 days without manual action
- **Higher Yields**: Access to Node Operator Pool rates, often higher than community staking
- **No Opportunity Cost**: Keep earning even while using stLINK in other DeFi protocols

**Flexibility Advantages:**
- **Maintain Liquidity**: Unlike native staking, you can exit positions quickly
- **Faster Withdrawals**: 1-7 days vs. 28-day native cooldown (or instant via DEX swaps)
- **DeFi Composability**: Use stLINK as collateral, in liquidity pools, or trade it
- **No Lock-up Period**: Your capital isn't completely frozen

**User Experience:**
- **Simplified Staking**: No need to manage individual validator selection
- **Professional Management**: Built by consortium of top Chainlink node operators
- **Set It and Forget It**: Rewards accrue automatically without claiming

### Cons of Staking on stake.link

**Risks to Consider:**
- **Smart Contract Risk**: Bugs or exploits in stake.link contracts could result in loss of funds
- **Additional Layer of Risk**: More complex than just holding LINK in your wallet
- **Slashing Risk**: Though minimal, validators could theoretically be slashed for poor performance
- **Protocol Dependency**: You rely on stake.link's continued operation and security

**Financial Considerations:**
- **Fee Structure**: Protocol takes a cut of staking rewards (though APY shown is already net of fees)
- **Gas Fees**: Staking and unstaking require ETH for transaction costs
- **Price Variance**: stLINK may trade at slight premium/discount to LINK on secondary markets
- **Impermanent Loss**: If using stLINK in liquidity pools, you face IL risk

**Liquidity and Market Risks:**
- **stLINK Liquidity**: In extreme market conditions, stLINK/LINK liquidity could dry up
- **Regulatory Uncertainty**: Staking regulations are still evolving globally
- **Market Volatility**: LINK price can still drop regardless of staking rewards
- **Exit Delays**: Protocol withdrawals still take 1-7 days (not truly instant)

**Technical Considerations:**
- **Complexity**: Requires understanding of DeFi, wallets, and smart contracts
- **No FDIC Insurance**: Unlike traditional savings, no deposit protection
- **Tax Implications**: Staking rewards are taxable events in many jurisdictions
- **Maintenance**: Need to monitor protocol health and any governance changes

### When Staking Makes Sense

Consider staking if you:
- Plan to hold LINK long-term (6+ months)
- Want to earn yield on idle assets
- Understand and accept smart contract risks
- Have enough LINK to justify gas fees (suggested minimum: 10-50 LINK)
- Are comfortable with DeFi protocols
- Want to participate in DeFi while earning staking rewards

### When You Might Skip Staking

Consider NOT staking if you:
- Need immediate access to funds without any delay
- Are uncomfortable with smart contract risk
- Have very small amounts where gas fees eat into returns
- Plan to actively trade LINK frequently
- Are new to crypto and want to start simple
- Cannot afford to potentially lose the funds
- Are staking solely because of FOMO without understanding risks

### Risk Mitigation Strategies

If you decide to stake:
- **Start Small**: Test with a small amount first
- **Diversify**: Don't stake 100% of your LINK holdings
- **Research**: Read audit reports and monitor protocol health
- **Use Hardware Wallets**: Trezor/Ledger for maximum security
- **Understand Costs**: Calculate if rewards justify gas fees for your amount
- **Stay Informed**: Follow stake.link announcements and governance

### The Bottom Line

Staking on stake.link offers a compelling way to earn passive income on LINK while maintaining flexibility, but it's not risk-free. The decision should align with your:
- **Risk tolerance**: Can you handle smart contract and market risks?
- **Time horizon**: Are you a long-term holder?
- **Capital size**: Do rewards outweigh transaction costs?
- **Technical comfort**: Are you confident navigating DeFi?

There's no universal right answer - it depends on your individual situation and goals.

## FAQ

**Q: Do I need SDL tokens to stake LINK?**  
A: No, SDL is not required. You only need LINK and ETH for gas fees.

**Q: What's the minimum amount to stake?**  
A: There's no strict minimum, but consider gas fees when staking small amounts.

**Q: Can I unstake immediately?**  
A: You can swap stLINK to LINK instantly on DEXs, or use the protocol withdrawal (1-7 days).

**Q: How often do rewards compound?**  
A: The rebasing mechanism updates approximately every 2 days.

**Q: Is my LINK locked?**  
A: No, you receive liquid stLINK tokens that can be traded or used in DeFi anytime.

**Q: What's the difference from native Chainlink staking?**  
A: stake.link offers liquidity, auto-compounding, and access to higher node operator yields.

## Additional Resources

- **Official Website**: [stake.link](https://stake.link/)
- **Documentation**: [docs.stake.link](https://docs.stake.link/)
- **Governance Forum**: [talk.stake.link](https://talk.stake.link/)
- **GitHub**: [github.com/stakedotlink](https://github.com/stakedotlink)

## Conclusion

stake.link provides an efficient way to stake LINK while maintaining liquidity and earning competitive yields. The liquid staking model offers flexibility that traditional staking can't match, making it ideal for users who want both rewards and DeFi composability.

Remember to always do your own research, understand the risks, and never invest more than you can afford to lose.