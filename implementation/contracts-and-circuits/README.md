---
description: EVM-based
---

# Smart Contracts

The zkBob solution is based on several interrelated smart contracts. The main purpose of the contract subsystem is to store the current [Merkle tree](../untitled/) state inside the base blockchain. Each zkBob transaction changes the Merkle tree, so it should be processed by a smart contract. See the subsystem below, where the Pool contract is the primary contract for processing transactions.

<figure><img src="../../.gitbook/assets/1_Light_Smart Contracts.jpg" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
[Contracts Github repo.](https://github.com/zkBob/zkbob-contracts) Contract code is also linked in the contract pages referenced below.
{% endhint %}

* [Pool contract ](the-pool-contract/)is the main contract which holds the current Merkle tree state. It process all transactions and holds a current Merkle tree root.
* [Token contract](token-contract.md) mints a shielded coin protected by the current zkBob solution. This token is deposited in the Pool contract and withdrawn from it.
* [Verifier contracts](verifier-contracts.md) are used by the Pool contract to check transaction correctness / validate zkSNARK proofs.
* [Operator contract](operator-manager-contract/) helps the Pool contract to determine whether transactions can be accepted from a sender. It is used in the multi-relayer configuration to serialize the transaction sequence from the different nodes and minimize transaction collisions.
* [Voucher token contract](voucher-token-contract.md) mints a token ([XP](../../roadmap/exploratory-features/xp/)) to reward users for their contribution in the anonymity set.

