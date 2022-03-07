---
description: Public and secret parts
---

# Common Structure

The transaction transferred to the zkBob contract contains the following fields:

* Account nullifier - helps protect from the double-spending
* Transaction commitment - transaction's subtree root hash
* Transfer index
* Energy amount - for withdrawal transaction
* Token amount - a positive value for the deposit transaction, negative - for withdrawal
* Transaction proof
* Merkle tree root after transaction including
* Merkle tree proof
* [Transaction type](transaction-types.md)
* Transaction specific fields (depends on transaction type)
* Memo block which contain encrypted transaction details (accounts and notes)
* Deposit signature - to retrieve source account (exist in the deposit transaction only)

In general, a transaction sender must prepare all of these fields before submitting to the contract. In case of using relayer it should calculate proofs and send the transaction to the contract.

The sender forms two transaction parts when it's created. There are public and secret parts for the transaction. The public part contains encrypted transaction data and other fields which cannot disclosure sender, receiver, internal transfer amount, etc. The secret transaction's part contains unencrypted data such as input and output accounts and notes, proofs and EDDSA signature.

#### The public transaction components

* The current Merkle tree root (before transaction processing by the contract)
* Input account nullifier
* Transaction commitment
* Delta value (a composition of the transaction index, token delta and energy delta)
* Memo block

#### The secret transaction components

* A set of unencrypted input\output account and notes for the transaction
* Input account and notes proofs
* Transaction signature $$(S, R)$$
* Transaction verifier key $$A$$ to verify signature


