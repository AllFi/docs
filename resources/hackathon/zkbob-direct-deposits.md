---
description: >-
  A decentralised way of depositing to a zkBob account without using zk core
  components
---

# zkBob Direct Deposits

## Introduction

zkBob supports 5 different operations:

1. Deposit - Add funds to your zkAccount.
2. Withdraw - Withdraw BOB tokens from your private account to a public 0x address.
3. Private transfer - Make an anonymous transfer from one user to another with their zkAddress.
4. Private multi-transfer - Make an anonymous atomic batch transfer to multiple zkAddresses
5. **Direct deposit -** Send BOB directly **** to someone’s zkAddress from outside the zkBob application.

The first 4 operations can only be performed by end users via zkBob clients, such as the zkBob UI.

However, with direct deposits, private deposits can be performed while abstracting away zk complexity. Depositors only need to know the private zkAddress of the receiver. This makes it very easy to integrate it into various automated web3 workflows.

Direct deposits allow any user, smart contract, or third party protocol to deposit any amount\* ([within accepted limits](zkbob-direct-deposits.md#direct-deposit-limits)) of BOB into the queue, which is then processed by the zkBob relayer in a trustless manner. The only function of the relayer is to include deposits in the state tree, providing a safe mechanism for deposits.

The relayer can process multiple direct deposits at once, however, users may need to wait some time - possibly up to a few hours - until the deposit is reflected in the zkBob account.

{% hint style="warning" %}
For now, pending or cancelled direct deposits are not shown in the zkBob UI. Users will only see already processed deposits.
{% endhint %}

## Direct deposits

Direct deposits allow end users, intermediary protocols and smart contracts to make private transfers directly to the receiver zk address. Any EVM-based workflow containing one or more stablecoin transfers might be easily integrated with zkBob direct deposits on the smart contract level, with very little modification required on the UI side.

Examples where zkBob direct deposits can be integrated:

* Swap and cross-chain bridge aggregators
* Payroll and funds streaming protocols
* Donation / fundraising / tipping applications
* Vendor purchases
* Open-source wallets and browser extensions

## Direct deposits integration

Direct deposits can be easily integrated on the smart contract level using the simple interface (available at [GitHub](https://github.com/zkBob/zkbob-contracts/blob/develop/src/interfaces/IZkBobDirectDeposits.sol)).

<details>

<summary>IZkBobDirectDeposits.sol</summary>

```solidity
// SPDX-License-Identifier: CC0-1.0

pragma solidity ^0.8.0;

interface IZkBobDirectDeposits {
    enum DirectDepositStatus {
        Missing, // requested deposit does not exist
        Pending, // requested deposit was submitted and is pending in the queue
        Completed, // requested deposit was successfully processed
        Refunded // requested deposit was refunded to the fallback receiver
    }

    struct DirectDeposit {
        address fallbackReceiver; // refund receiver for deposits that cannot be processed
        uint96 sent; // sent amount in BOB tokens (18 decimals)
        uint64 deposit; // deposit amount, after subtracting all fees (9 decimals)
        uint64 fee; // deposit fee (9 decimals)
        uint40 timestamp; // deposit submission timestamp
        DirectDepositStatus status; // deposit status
        bytes10 diversifier; // receiver zk address, part 1/2
        bytes32 pk; // receiver zk address, part 2/2
    }

    /**
     * @notice Retrieves the direct deposits from the queue by its id.
     * @param depositId id of the submitted deposit.
     * @return deposit recorded deposit struct
     */
    function getDirectDeposit(uint256 depositId) external view returns (DirectDeposit memory deposit);

    /**
     * @notice Performs a direct deposit to the specified zk address.
     * In case the deposit cannot be processed, it can be refunded later to the fallbackReceiver address.
     * @param fallbackReceiver receiver of deposit refund.
     * @param amount direct deposit amount.
     * @param zkAddress receiver zk address.
     * @return depositId id of the submitted deposit to query status for.
     */
    function directDeposit(
        address fallbackReceiver,
        uint256 amount,
        bytes memory zkAddress
    )
        external
        returns (uint256 depositId);

    /**
     * @notice Performs a direct deposit to the specified zk address.
     * In case the deposit cannot be processed, it can be refunded later to the fallbackReceiver address.
     * @param fallbackReceiver receiver of deposit refund.
     * @param amount direct deposit amount.
     * @param zkAddress receiver zk address.
     * @return depositId id of the submitted deposit to query status for.
     */
    function directDeposit(
        address fallbackReceiver,
        uint256 amount,
        string memory zkAddress
    )
        external
        returns (uint256 depositId);

    /**
     * @notice ERC677 callback for performing a direct deposit.
     * Do not call this function directly, it's only intended to be called by the token contract.
     * @param from original tokens sender.
     * @param amount direct deposit amount.
     * @param data encoded address pair - abi.encode(address(fallbackReceiver), bytes(zkAddress))
     * @return ok true, if deposit of submitted successfully.
     */
    function onTokenTransfer(address from, uint256 amount, bytes memory data) external returns (bool ok);

    /**
     * @notice Tells the direct deposit fee, in zkBOB units (9 decimals).
     * @return fee direct deposit submission fee.
     */
    function directDepositFee() external view returns (uint64 fee);

    /**
     * @notice Tells the timeout after which unprocessed direct deposits can be refunded.
     * @return timeout duration in seconds.
     */
    function directDepositTimeout() external view returns (uint40 timeout);

    /**
     * @notice Tells the nonce of next direct deposit.
     * @return nonce direct deposit nonce.
     */
    function directDepositNonce() external view returns (uint32 nonce);

    /**
     * @notice Refunds specified direct deposit.
     * Can be called by anyone, but only after the configured timeout has passed.
     * Function will revert for deposit that is not pending.
     * @param index deposit id to issue a refund for.
     */
    function refundDirectDeposit(uint256 index) external;

    /**
     * @notice Refunds multiple direct deposits.
     * Can be called by anyone, but only after the configured timeout has passed.
     * Function will do nothing for non-pending deposits and will not revert.
     * @param indices deposit ids to issue a refund for.
     */
    function refundDirectDeposit(uint256[] memory indices) external;
}

```

</details>

### Getting a zkAddress to send a direct deposit to

{% hint style="info" %}
The most convenient way for users to generate a receiving zkAddress is to use the zkBob UI to open an account and generate an address - [generate-a-secure-address.md](../../zkbob-app/generate-a-secure-address.md "mention")

zkAddresses can be [formatted in different ways](zkbob-direct-deposits.md#zkaddress-format) for direct deposit submission.&#x20;
{% endhint %}

### Submitting a direct deposit

Direct deposits can be submitted directly to the pool contract, using one of two approaches:

1. Common `approve` + `deposit` approach, suitable for a majority of use-cases.
2. Shortcut approach using `transferAndCall`, suitable for simple workflows.

{% hint style="info" %}
The  ERC677 `transferAndCall` approach is more gas efficient. However, it does not return the `depositId`. If you need to implement any post-submission logic in your application on the smart contract level and you need a `depositId`, please use the 1st approach.
{% endhint %}

Calling either of these methods requires 3 input arguments:

1. `fallbackReceiver` - regular user public 0x address, which will receive the funds in the unlikely scenario that the deposit is rejection by the system \
   (**DO NOT** **set this address to zero or address that does not belong to the intended receiver**)
2. `amount` - deposit BOB amount, 18 decimals. A small fee (0.1 BOB) is subtracted from each amount.
3. `zkAddress` - private zk address of the intended receiver, see info below for the supported address formats

```solidity
IERC20 bob = IERC20(0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B);
IZkBobDirectDeposits queue = IZkBobDirectDeposits(TBD);

bytes memory zkAddress = bytes("QsnTijXekjRm9hKcq5kLNPsa6P4HtMRrc3RxVx3jsLHeo2AiysYxVJP86mriHfN");

address fallbackReceiver = msg.sender;

// Option A, through pool contract
// Note that ether is an alias for 10**18 multiplier, as BOB token has 18 decimals
bob.approve(address(queue), 100 ether);
uint256 depositId = queue.directDeposit(fallbackReceiver, 100 ether, zkAddress);

// Option B, through ERC677 token interface
bob.transferAndCall(address(queue), 100 ether, abi.encode(fallbackReceiver, zkAddress));
```

Calls to either of the deposit methods can revert with corresponding revert reasons in case of the following scenarios:

1. Insufficient BOB allowance for `directDeposit` call.
2. Zero `fallbackReceiver` parameter.
3. Insufficient deposit amount to cover the implied deposit fee.
4. Deposit amount exceeding the single deposit limit for a particular user (1,000 BOB).
5. Sum of daily direct deposits exceeding daily deposit limit for a particular user (10,000 BOB).
6. Invalid zkAddress format/length/checksum.

The most straightforward way to test direct deposit submission is through the Etherscan UI:

![](<../../.gitbook/assets/Screenshot 2023-02-22 at 10.16.38 AM (1).png>)

{% hint style="warning" %}
Submitting a direct deposit in most scenarios will require the end user to pay transaction fees in Matic, which is not the same for regular zkBob operations.
{% endhint %}

### Checking deposit status

Submitted direct deposits are not executed immediately and instead are placed into the queue with `Pending` status to be later processed by the zkBob relayer.

In case your workflow requires any post-execution logic, you can request the actual deposit status from the pool contract.

```solidity
IZkBobDirectDeposits.DirectDeposit memory deposit = queue.getDirectDeposit(depositId);
require(deposit.status == IZkBobDirectDeposits.DirectDepositStatus.Completed);
```

### Refund pending direct deposit

In the unlikely event the deposit is rejected by the system due to compliance or AML reasons, a previously submitted direct deposit can be refunded back to the specified fallback receiver address 1 day following the deposit submission.

```solidity
queue.refundDirectDeposit(depositId);
```

### Request extra system information

```solidity
uint64 fee = queue.directDepositFee();
uint40 timeout = queue.directDepositTimeout();
uint32 nextDepositId = queue.directDepositNonce();
```

## zkAddress format

zkBob smart contracts supports 3 different zkAddress formats. These are identical to one to another with the exception of a small difference in their processing.

zkAddress consists of two main parts - a diversifier and a public key, look for more information here - [address-derivation.md](../../implementation/zkbob-keys/address-derivation.md "mention"). zkBob smart contracts support multiple address formats, which contain a different encoding of the two parts.

{% hint style="info" %}
The most convenient way to generate a receiving zkAddress is to use the zkBob UI to open an account and an address - [generate-a-secure-address.md](../../zkbob-app/generate-a-secure-address.md "mention")
{% endhint %}

1. zkBob UI format:
   * Example: `QsnTijXekjRm9hKcq5kLNPsa6P4HtMRrc3RxVx3jsLHeo2AiysYxVJP86mriHfN`
   * Base58 encoding of the following string: `bytes10(diversifier_le) ++ bytes32(pk_le) ++ bytes4(checksum)`
   * Length of up to 63 base58 symbols
   * Base58 decoding is done on the smart contract level at the moment of deposit submission and is gas intensive (\~610k gas)
2. Pre-decoded zkBob UI format (**recommended**):
   * Example: `0xda9ee1b1b651c87a76c2efe3e4b9b0a0e53e5b66ed19ad100afe5289ea732bfd5ac002969523f26e6f2ff4e1d3a9`
   * Same format as in the zkBob UI, but omitting the base58 encoding - `bytes10(diversifier_le) ++ bytes32(pk_le) ++ bytes4(checksum)`
   * Much more gas efficient decoding than the previous format (\~3,400 gas)
3. Raw format:
   * Example: `0xc2767ac851b6b1e19eda2f6f6ef223959602c05afd2b73ea8952fe0a10ad19ed665b3ee5a0b0b9e4e3ef`
   * Raw format without checksum - `bytes10(diversifier_be) ++ bytes32(pk_be)`
   * Most gas efficient decoding (\~1,100 gas)
   * Addresses without checksums can be error-prone and are generally not recommended for usage

{% hint style="warning" %}
Note the difference in endianness between encodings. Addresses coming from zkBob UI use little endian for zk address encoding.

Sending direct deposit to the incorrectly serialized address might result in the loss of funds.
{% endhint %}

### Checksum

zkBob address checksum is first 4 bytes of `keccak(bytes10(diversifier_le) ++ bytes32(pk_le))`

### Solidity Library

zkBob smart contracts use the following Solidity library for address parsing - [GitHub](https://github.com/zkBob/zkbob-contracts/blob/develop/src/libraries/ZkAddress.sol)

Use it to test off-chain zkAddress validation logic, or call read-only `parseZkAddress` function to convert zkBob UI address format to raw format&#x20;

## Direct deposit limits

All submitted direct deposits are subject to per-user limits at the time of their submission. Submission of direct deposits exceeding configured limits will revert.

Default direct deposits limits for all users:

1. Max amount of a single deposit - **1,000 BOB**
2. Max daily sum of all single user deposits - **10,000 BOB**

## Direct deposit fee

Apart from associated gas costs for the deposit transaction submission, which is paid by the user, each direct deposit submission will also cost 0.1 **BOB** to process.

## FAQs

### zkBOB is on Polygon, does that mean my app also needs to be deployed there?

The easiest way to integrate is to deploy directly on Polygon. However, we are excited about ideas for adding multichain composability using bridges. This will require some workarounds, as there are no native bridges for BOB currently.

### Does a direct deposit operation require MATIC?

Yes, MATIC is required to pay the gas fees for a direct deposit transaction. In addition, a fee of 0.10 BOB will be charged for each direct deposit tx. For regular deposits, transfers or withdrawals within the zkBob application, MATIC is not required.





