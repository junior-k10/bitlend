# BitLend Protocol

**Decentralized Bitcoin-backed Lending on Stacks**

BitLend is a sophisticated decentralized lending and borrowing protocol built on the [Stacks blockchain](https://www.stacks.co/). It enables users to unlock liquidity from their STX holdings while maintaining exposure to Bitcoin’s upside potential. The protocol implements over-collateralized lending with automated liquidation safeguards, governance-driven parameters, and robust security patterns.

---

## 📌 System Overview

BitLend revolutionizes Bitcoin DeFi by enabling:

* **Collateralized Lending:** Users deposit STX as collateral and borrow STX against it.
* **Capital Efficiency:** Dynamic collateral ratios balance borrower utility and lender safety.
* **Liquidation Protection:** Under-collateralized positions are liquidated through an incentivized mechanism to protect lenders.
* **Governance:** Protocol parameters (collateral ratios, liquidation thresholds, protocol fees) are adjustable via owner governance.
* **Risk Mitigation:** MEV-resistant liquidation incentives and automated risk controls ensure long-term solvency.

---

## ⚙️ Core Features

* ✅ Over-collateralized lending with customizable ratios
* ✅ Automated liquidation engine for under-collateralized debt
* ✅ Real-time interest calculation and compounding
* ✅ Governance-driven parameter adjustment
* ✅ Protocol fee mechanism for sustainability
* ✅ Security-first architecture with reentrancy and overflow protection

---

## 🏗️ Contract Architecture

The contract is composed of **four main layers**:

### 1. **Core Protocol Functions**

* `deposit` → Deposit STX as collateral
* `borrow` → Borrow STX against collateral (validated via collateral ratio)
* `repay` → Repay borrowed STX to reduce debt
* `withdraw` → Withdraw collateral while maintaining minimum ratio

### 2. **Risk & Liquidation Mechanism**

* `liquidate` → Allows third parties to liquidate under-collateralized users and claim collateral

### 3. **Governance & Administration**

* `set-minimum-collateral-ratio` → Adjust collateral requirements
* `set-liquidation-threshold` → Update liquidation thresholds
* `set-protocol-fee` → Adjust fee parameters

### 4. **Read-Only Functions**

* `get-user-position` → Retrieve a user’s collateral, borrowed amount, and loan stats
* `get-protocol-stats` → Retrieve global protocol metrics

---

## 📊 Data Structures

### Data Variables

* `minimum-collateral-ratio` → Protocol-wide minimum collateral requirement
* `liquidation-threshold` → Threshold at which positions can be liquidated
* `protocol-fee` → Fee charged on borrowing activity
* `total-deposits` → Aggregate STX collateral across users
* `total-borrows` → Aggregate borrowed STX

### Data Maps

* **loans** → Tracks individual loan details (collateral, debt, interest, status)
* **user-positions** → Aggregates collateral and borrowed balances per user

---

## 🔄 Data Flow

**Deposit Flow**

1. User deposits STX → STX transferred to contract
2. Collateral balance updated in `user-positions`
3. Protocol aggregates collateral in `total-deposits`

**Borrow Flow**

1. Borrow request validated against collateral ratio
2. STX transferred to borrower
3. Debt balance updated in `user-positions`
4. Protocol aggregates debt in `total-borrows`

**Repay Flow**

1. Borrower transfers STX repayment to contract
2. Debt reduced from `user-positions` and `total-borrows`

**Withdrawal Flow**

1. Request validated against collateral ratio
2. STX transferred back to user
3. Collateral balance reduced

**Liquidation Flow**

1. Collateral ratio falls below liquidation threshold
2. Liquidator pays debt, seizes collateral
3. User position is cleared, protocol state updated

---

## 🔐 Security & Compliance

* **Reentrancy Protection** → State updates precede external transfers
* **Safe Arithmetic** → Overflow/underflow prevention via checked operations
* **Access Control** → Admin-only governance functions
* **Immutable Logic** → Core protocol immutable, parameters adjustable
* **Error Handling** → Explicit error codes for validation and state checks

---

## 📈 Protocol Parameters

| Parameter                | Default | Range           | Description                       |
| ------------------------ | ------- | --------------- | --------------------------------- |
| Minimum Collateral Ratio | 150%    | 110% - 500%     | Required ratio to borrow          |
| Liquidation Threshold    | 130%    | ≥110% and ≤ MCR | Trigger for liquidation           |
| Protocol Fee             | 1%      | 0% - 10%        | Borrowing fee charged by protocol |

---

## 🚀 Future Extensions

* Multi-asset collateral support (sBTC, USDC on Stacks)
* Dynamic interest rate models (based on utilization)
* DAO-based governance with voting mechanisms
* Integration with decentralized liquidation markets

---

## 📜 License

MIT License. See [LICENSE](LICENSE) for details.
