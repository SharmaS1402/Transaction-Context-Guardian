# Transaction Context Guardian

A comprehensive blockchain transaction security system that protects users from various threats through multi-layer analysis.

## Overview

Transaction Context Guardian is a sophisticated security system that analyzes blockchain transactions through multiple risk dimensions to detect and prevent various threats. By employing a layered approach, it can identify patterns that single-vector analysis might miss.

## How It Works

The system intercepts transactions before execution, collects contextual data, performs multi-layer analysis, calculates a comprehensive risk score, and provides appropriate responses based on the risk level.

### Architecture

1. **Transaction Interception**
   - Captures pending transactions before execution
   - Creates a detection request with transaction data and context

2. **Data Collection & Enrichment**
   - Gathers historical data, cross-chain activity, social graph information
   - Enriches transactions with metadata like contract verification status

3. **Multi-Layer Analysis**
   - Each analyzer examines a different security aspect
   - Individual risk scores are calculated for each dimension

4. **Risk Calculation**
   - Combines individual scores with contextual weighting
   - Implements correlation boosting for multi-vector risks

5. **Decision Engine**
   - Evaluates final risk score against thresholds
   - Determines appropriate response (allow, warn, block)

6. **Learning & Improvement**
   - Transaction outcomes feed back into the system
   - User decisions help refine the model

## Custom Detectors

### 1. Phishing Custom Detector
Detects transactions initiated from malicious or fake dApp interfaces that aim to trick users.

**Triggers:**
- Transaction originates from a known phishing domain
- Domain has suspicious characteristics (similarity to legitimate services, recent registration)
- UI manipulation markers detected

**Example Transaction:**
A transaction from a legitimate wallet to `0x7a250d5630b4cf539739df2c5dacb4c659f2488d` (Uniswap Router) but originating from the domain `uniswap-exchange.org` (not the legitimate Uniswap domain).

### 2. Approvals Custom Detector
Identifies malicious, risky, or deceptive token approvals that could give attackers access to assets.

**Triggers:**
- Unlimited token approvals (maximum uint256 value)
- Approvals to recently deployed or unverified contracts
- setApprovalForAll for NFT collections

**Example Transaction:**
An ERC20 approval transaction to an unverified contract with function signature `0x095ea7b3` and unlimited approval amount `0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff`.

### 3. 2FA Custom Detector
Enables users to use authenticator apps to confirm high-risk transactions.

**Triggers:**
- Transaction risk level is MEDIUM or HIGH
- Transaction involves large value transfers
- Transaction matches user-configured 2FA triggers

**Example Scenario:**
A transaction with a final risk score above 40 will require 2FA verification before proceeding.

### 4. MEV Custom Detector
Prevents value extraction attacks like sandwich trades that exploit users during swaps.

**Triggers:**
- DEX swap transactions with low slippage tolerance
- Swaps involving low-liquidity pairs
- Transactions during high gas price periods

**Example Transaction:**
A swap on Uniswap (`0x7a250d5630b4cf539739df2c5dacb4c659f2488d`) with function signature `0x38ed1739` (swapExactTokensForTokens) and minimal slippage protection.

### 5. Rugpull (Smart Contract) Custom Detector
Analyzes smart contracts for hidden risks that could allow developers to drain funds.

**Triggers:**
- Interactions with unverified contracts
- Contracts with suspicious code patterns
- Recently deployed contracts with high-risk functions

**Example Transaction:**
A transaction to a contract created within the last 7 days that is unverified on block explorers.

### 6. Multisig Protection Custom Detector
Enhances security for multisig wallets by detecting unusual signing patterns.

**Triggers:**
- Deviation from established signing sequences
- Attempts to change owner addresses
- Unusual timing of signature submissions

**Example Transaction:**
A transaction from a known multisig wallet attempting to execute an owner replacement function.

## Implementation Details

The Transaction Context Guardian implements all required custom detectors using a modular architecture where each analyzer focuses on a specific security aspect. The risk calculator combines these individual analyses into a comprehensive risk assessment.

The implementation carefully balances security with usability by:
- Only blocking transactions with HIGH risk scores
- Requiring 2FA for MEDIUM risk transactions
- Providing detailed explanations for any flagged transactions

## Testing

The system has been tested against various attack scenarios including:
- Simulated phishing attacks
- Malicious approval scenarios
- MEV attack patterns
- Contract-based attack vectors

All detectors have been validated with both positive test cases (should trigger) and negative test cases (shouldn't trigger).

## Future Improvements

1. **Machine Learning Integration**
   - Train models on historical attack data
   - Implement adaptive thresholds based on user behavior

2. **Enhanced Cross-Chain Monitoring**
   - Expand bridge contract database
   - Implement real-time bridge activity tracking

3. **Community Threat Intelligence**
   - Anonymous sharing of attack vectors
   - Rapid distribution of new threat signatures