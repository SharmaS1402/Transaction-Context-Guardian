# Transaction Context Guardian

A comprehensive blockchain transaction security system that protects users from various threats through multi-layer analysis.

## Overview

Transaction Context Guardian is a sophisticated security system that analyzes blockchain transactions through multiple risk dimensions to detect and prevent various threats. By employing a layered approach, it can identify patterns that single-vector analysis might miss.

## How It Works

The system intercepts transactions before execution, collects contextual data, performs multi-layer analysis, calculates a comprehensive risk score, and provides appropriate responses based on the risk level.

### Architecture

flowchart TD
    subgraph "User Interaction"
        A[User Initiates Transaction] --> B{Transaction Interceptor}
    end

    subgraph "Data Collection Layer"
        B --> C[Historical Data Aggregator]
        B --> D[Cross-Chain Monitor]
        B --> E[Social Graph Analyzer]
        B --> F[Transaction Enrichment]
    end

    subgraph "Analysis Engine"
        C --> G[Temporal Pattern Analyzer]
        D --> H[Cross-Chain Risk Analyzer]
        E --> I[Social Graph Risk Analyzer]
        F --> J[Approval Intelligence Engine]
        
        G --> K[Temporal Risk Score]
        H --> L[Cross-Chain Risk Score]
        I --> M[Social Graph Risk Score]
        J --> N[Approval Risk Score]
        
        K --> O[Risk Score Calculator]
        L --> O
        M --> O
        N --> O
        
        O --> P[Final Risk Score]
    end

    subgraph "Decision Engine"
        P --> Q{Risk Assessment}
        Q -->|Low Risk| R[Allow Transaction]
        Q -->|Medium Risk| S[Warning + 2FA Option]
        Q -->|High Risk| T[Block + Alert]
    end

    subgraph "Response Management"
        R --> U[Transaction Proceeds]
        S --> V[User Decides]
        V -->|Confirm with 2FA| U
        V -->|Cancel| W[Transaction Cancelled]
        T --> W
    end

    subgraph "Learning & Improvement"
        U --> X[Feedback Loop]
        W --> X
        X --> Y[Model Refinement]
        Y --> C
    end
    
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

## Implementation Details

The Transaction Context Guardian implements all required custom detectors using a modular architecture where each analyzer focuses on a specific security aspect. The risk calculator combines these individual analyses into a comprehensive risk assessment.

The implementation carefully balances security with usability by:
- Only blocking transactions with HIGH risk scores
- Requiring 2FA for MEDIUM risk transactions
- Providing detailed explanations for any flagged transactions
