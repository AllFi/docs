# Basic Concepts

{% hint style="info" %}
Below are descriptions of basic concepts underlying BOB and zkBob functionality. For more thorough details, see the [technical overview](broken-reference) section.
{% endhint %}

### Bob

Bob is a stablecoin protocol, and BOB is the stablecoin optimized for the protocol. BOB can be swapped 1-to-1 with USDC. BOB can be used in conjunction with the zkBob application to enable small, anonymous transactions between users.

### zkBob

zkBob is an application within the Bob protocol. It accepts BOB stablecoins for deposit, and transforms these into shBOB, which can be transferred anonymously between participants. On exit from the application, shBOB is converted back to BOB.&#x20;

### Zero-Knowledge Proofs

zkBob uses zero-knowledge proofs to verify an action has been completed (deposit, transfer, withdrawal) without providing any other identifying details about that action. Zkproofs confirm that the chain state has changed without divulging information about amounts, initiators, or receivers of transactions. [Learn more about zero-knowledge proofs](https://en.wikipedia.org/wiki/Zero-knowledge\_proof).

### zkBob Account

A zkBob account is linked to a user via a private key. The private key is used to identify the account balance, generate proofs to transfer tokens, and withdraw tokens from the pool.&#x20;

zkBob accounts are created either from the private key of an existing wallet or from a stand-alone seed phrase. Users can decide how they would like to create an account following a step-by-step process.

Accounts never appear unencrypted in a public field and can only be decrypted by the account owner.

### zkBob Address

A zkBob account doesn't contain a fixed address for receiving funds. Rather, the user generates a private zkBob address using the application. Through the UI, a new address is generated for each incoming transaction.&#x20;

It is not possible to link different private addresses to one another or to the primary account. Only the account owner can confirm ownership of a private address.

Each created address is encoded in base58 format. For example `5fkW3dXTvA8Kizt1EbuRyjWofuqR4Ud1YTjGgY1r8nGosDeSaUreq6bwfF61jWL`

### **Deposits**

Deposits can be made by sending Bob tokens (from a zkBob Account) to the zkBob pool contract. Depositors complete 2 steps to get started.&#x20;

1. Approve the contract to access the funds
2. Create and send the deposit.&#x20;

Transactions are routed via a relayer to the pool contract.

### **Transfers**

Transfers also use relayers to send private transactions. A user can transfer funds to another zkBob account by sending zk-proofs anonymously to a relayer. The relayer then publishes the transaction to the zkBob contract.

### Withdrawals

Similar to deposits, a user can send a transaction to the zkBob contract to withdraw tokens from the pool. The transaction contains a zero-knowledge proof of token ownership generated using the private key associated with the corresponding zkBob account.

### **BOB Stable Token**

BOB tokens are stable tokens paired with USDC on a Uniswap v3 pool. Using range settings in Uniswap v3 slippage can be minimized so that BOB remains stable. BOB is designed to function specifically with the zkBob privacy pool. They can be acquired through Uniswap v3 with USDC, then transferred to the Bob rollup and zkBob application through the user interface.

### **shBOB Token**

shBOB is shielded BOB, a secure token used for transfers within the zero-knowledge pool.  BOB is automatically converted to shBOB when completing a deposit, and shBOB is converted back to BOB on withdrawal.

### Relayer

The relayer acts as an intermediary between the user and the smart contracts. Transactions are sent to the relayer which collects transactions, calculates Merkle tree proofs, orders them in a queue, then sends this information to the contract. The relayer cannot see transaction amounts and preserves anonymity by abstracting gas fees for operations. Relayer interaction occurs via a [REST API](../implementation/relayer-node/rest-api.md).

