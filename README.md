# 🚀 Jackramp Subgraph

A subgraph implementation for tracking Jackramp contract events and entities on the Holesky network. This subgraph indexes mint events, transfers, withdrawals, operators, and off-ramp transactions.

## 📧 Docs

Project Documentation : [https://kbaji.gitbook.io/jackramp-avs](https://kbaji.gitbook.io/jackramp-avs)

## 📋 Overview

This subgraph tracks the following events from the Jackramp contract:
- Off-ramp requests and fills
- Minting operations
- Token transfers
- Withdrawals
- Operators

Contract Address: `0xfb3970e6eb88815c485b3531a36d4c8b45db1135` (Holesky Network)

## 🏗 Schema

### OffRamp
Tracks off-ramping operations with their current status:
```graphql
type OffRamp @entity {
  id: Bytes!
  user: Bytes!
  requestedAmount: BigInt!
  requestedAmountRealWorld: BigInt!
  channelAccount: Bytes!
  channelId: Bytes!
  status: OffRampStatus!
  # ... additional fields
}
```

### Other Entities
- `Mint`: Records minting operations
- `Transfer`: Tracks token transfers
- `Withdraw`: Logs withdrawal events
- `Operator`: Logs operator events

## 🛠 Setup

1. Install dependencies:
```bash
npm install
```

2. Generate types:
```bash
graph codegen
```

3. Build the subgraph:
```bash
graph build
```

## 📝 Configuration

The subgraph is configured to start indexing from block `2609411` on the Holesky network. Key configurations:

- Spec Version: 1.0.0
- API Version: 0.0.7
- Network: Holesky
- Language: AssemblyScript

## 🔍 Event Handlers

The subgraph implements handlers for:
- `handleFillOfframp`: Processes off-ramp completion events
- `handleMint`: Records new minting operations
- `handleRequestOfframp`: Tracks new off-ramp requests
- `handleTransfer`: Monitors token transfers
- `handleWithdraw`: Records withdrawal events
- `handleTaskResponded`: Records operator events

## 📊 Querying Examples

Query off-ramp requests:
```graphql
{
  offRamps(first: 5) {
    id
    user
    requestedAmount
    status
    blockTimestamp
  }
}
```

Get recent mints:
```graphql
{
  mints(orderBy: blockTimestamp, orderDirection: desc) {
    user
    amount
    blockNumber
  }
}
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🔗 Links
- [The Graph Protocol Documentation](https://thegraph.com/docs/en/)
- [AssemblyScript Documentation](https://www.assemblyscript.org/)
- [GraphQL Documentation](https://graphql.org/learn/)