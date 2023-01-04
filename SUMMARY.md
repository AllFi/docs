# Table of contents

## 🦹 zkBob Overview

* [zkBob](README.md)
* [Basic Concepts](zkbob-overview/basic-concepts/README.md)
  * [zk Privacy Solution Comparison](zkbob-overview/basic-concepts/zk-privacy-solution-comparison.md)
* [zkBob on Polygon](zkbob-overview/zkbob-on-polygon/README.md)
  * [zkBob Usage](zkbob-overview/zkbob-on-polygon/zkbob-usage.md)
* [Use Cases](zkbob-overview/use-cases/README.md)
  * [Employee Salary](zkbob-overview/use-cases/employee-salary.md)
  * [Vendor Purchasing](zkbob-overview/use-cases/vendor-purchasing.md)
* [Fees](zkbob-overview/fees.md)
* [Deposit & Withdrawal Limits](zkbob-overview/deposit-and-withdrawal-limits.md)
* [Compliance & Security](zkbob-overview/compliance-and-security/README.md)
  * [TRM Labs Integration](zkbob-overview/compliance-and-security/trm-labs-integration.md)
* [zkBob FAQ](zkbob-overview/faq.md)

## 🧙♂ BOB Stablecoin

* [BOB Highlights](bob-stablecoin/bob-details.md)
* [BOB Ecosystem](bob-stablecoin/bob-ecosystem.md)
* [Add BOB to Metamask](bob-stablecoin/add-bob-to-metamask.md)
* [Swap BOB with Metamask Swap](bob-stablecoin/swap-bob-with-metamask-swap.md)
* [BOB on Uniswap v3](bob-stablecoin/bob-on-uniswap-v3.md)
* [BOB Inventory](bob-stablecoin/bob-inventory/README.md)
  * [Inventory Management](bob-stablecoin/bob-inventory/inventory-management.md)
  * [BOB DAO](bob-stablecoin/bob-inventory/bob-dao.md)
* [BOB Stablecoin FAQ](bob-stablecoin/bob-stablecoin-faq.md)

## 🦸♂ zkBob Application <a href="#zkbob-app" id="zkbob-app"></a>

* [UI Overview](zkbob-app/zkbob-app.md)
* [Acknowledge Terms](zkbob-app/acknowledge-terms.md)
* [Account Creation](zkbob-app/account-creation/README.md)
  * [Metamask / Web3 Wallet Warning](zkbob-app/account-creation/metamask-web3-wallet-warning.md)
* [Deposits](zkbob-app/deposits.md)
* [Transfers](zkbob-app/transfers/README.md)
  * [Multitransfers](zkbob-app/transfers/multitransfers.md)
* [Withdrawals](zkbob-app/withdrawals.md)
* [Generate a Receiving Address](zkbob-app/generate-a-secure-address.md)
* [Get BOB](zkbob-app/get-bob.md)
* [Support ID](zkbob-app/support-id.md)

## 👷♂ Roadmap

* [On the Roadmap](roadmap/on-the-roadmap.md)
* [Exploratory Features](roadmap/exploratory-features/README.md)
  * [XP (Experience Points)](roadmap/exploratory-features/xp/README.md)
    * [XP-based Auctions](roadmap/exploratory-features/xp/xp-based-auctions.md)
  * [Multi-chain Custom Rollup Deployment](roadmap/exploratory-features/multi-chain-custom-rollup-deployment.md)
  * [Round-robin Operator Manager](roadmap/exploratory-features/round-robin-operator-manager.md)
  * [Compounding](roadmap/exploratory-features/compounding.md)

## 👩⚕ Technical Implementation <a href="#implementation" id="implementation"></a>

* [zkBob Application Overview](implementation/high-level-overview.md)
* [Deployed Contracts](implementation/deployed-contracts.md)
* [Smart Contracts](implementation/contracts-and-circuits/README.md)
  * [zkBob Pool Contract](implementation/contracts-and-circuits/the-pool-contract/README.md)
    * [Transaction Calldata](implementation/contracts-and-circuits/the-pool-contract/transaction-calldata.md)
  * [Bob Token Contract](implementation/contracts-and-circuits/token-contract.md)
  * [Verifier contracts](implementation/contracts-and-circuits/verifier-contracts.md)
  * [Operator Manager Contract](implementation/contracts-and-circuits/operator-manager-contract/README.md)
    * [Mutable Operator Manager](implementation/contracts-and-circuits/operator-manager-contract/mutable-operator-manager.md)
  * [Voucher (XP) Token Contract](implementation/contracts-and-circuits/voucher-token-contract.md)
* [Accounts and Notes](implementation/account-and-notes/README.md)
  * [Accounts](implementation/account-and-notes/accounts.md)
  * [Notes](implementation/account-and-notes/notes.md)
* [Relayer Node](implementation/relayer-node/README.md)
  * [Relayer Operations](implementation/relayer-node/relayer-operations.md)
  * [Optimistic State](implementation/relayer-node/optimistic-state.md)
  * [REST API](implementation/relayer-node/rest-api.md)
* [zkBob Keys](implementation/zkbob-keys/README.md)
  * [Address derivation](implementation/zkbob-keys/address-derivation.md)
  * [Ephemeral keys](implementation/zkbob-keys/ephemeral-keys.md)
* [zkSNARKs & Circuits](implementation/zksnarks-and-circuits/README.md)
  * [Transfer verifier circuit overview](implementation/zksnarks-and-circuits/transaction-verifier-circuit.md)
* [zkBob Merkle Tree](implementation/untitled/README.md)
  * [The Poseidon Hash](implementation/untitled/the-poseidon-hash.md)
* [Elliptic Curve Cryptography](implementation/elliptic-curve-cryptography.md)
* [Transaction Overview](implementation/transaction-overview/README.md)
  * [Common Structure](implementation/transaction-overview/common-structure.md)
  * [Memo Block](implementation/transaction-overview/untitled-1/README.md)
    * [Memo Block Encryption](implementation/transaction-overview/untitled-1/memo-block-encryption.md)
  * [Transaction Types](implementation/transaction-overview/transaction-types.md)
  * [Nullifiers](implementation/transaction-overview/the-nullifiers.md)
  * [Signing a Transaction](implementation/transaction-overview/signing-a-transaction.md)
  * [The Transaction Lifecycle](implementation/transaction-overview/the-transaction-lifecycle.md)

## 👩🏫 Deployment

* [Trusted Setup Ceremony](deployment/trusted-setup-ceremony.md)
* [Contract Deployment](deployment/contracts-deployment.md)
* [Relayer Subsystem](deployment/relayers-subsystem.md)

## 🧑💻 Jobs

* [Zero-Knowledge Researcher & Protocol Developer](jobs/zero-knowledge-researcher-and-protocol-developer.md)

## 🧩 Resources

* [Visual Assets](resources/visual-assets.md)
* [Hackathon](resources/hackathon.md)
* [Release Notes](resources/release-notes/README.md)
  * [January 2, 2023](resources/release-notes/january-2-2023.md)
  * [Releases 2022](resources/release-notes/releases-2022.md)
* [Github](https://github.com/zkbob)
* [Link tree](https://linktr.ee/zkbob)
