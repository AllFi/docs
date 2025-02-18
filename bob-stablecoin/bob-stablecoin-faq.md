---
description: What about $BOB
---

# BOB Stablecoin FAQ

{% hint style="info" %}
**FAQs**

* [How do I get BOB?](bob-stablecoin-faq.md#how-do-i-get-bob)
* [How does BOB remain stable?](bob-stablecoin-faq.md#how-does-bob-remain-stable)
* [How can I view BOB basic stats (tvl, volume etc)?](bob-stablecoin-faq.md#how-can-i-view-bob-basic-stats-tvl-volume-etc)
* [What are the BOB contract details?](bob-stablecoin-faq.md#what-are-the-bob-contract-details)
* [How is BOB inventory regulated?](bob-stablecoin-faq.md#how-is-bob-inventory-regulated)
* [Can I earn additional BOB through zkBob or in other ways?](bob-stablecoin-faq.md#can-i-earn-additional-bob-through-zkbob-or-in-other-ways)
* [What is the BOB public-facing website?](bob-stablecoin-faq.md#what-is-the-bob-public-website)
{% endhint %}

## How do I get BOB?

BOB is currently available on Polygon, Optimism, Arbitrum, BNB Chain and Ethereum. BOB can be acquired in several ways outside of the zkBob application.

* Sent between users to any 0x address on Polygon, Optimism, Arbitrum, BNB or Ethereum.
* Swap tokens for BOB using Metamask.&#x20;
  * [Instructions](add-bob-to-metamask/swap-bob-with-metamask-swap.md)
* Swap using a DEX or DEX aggregator
  * [Uniswap Instructions](bob-on-uniswap-v3.md)
  * [DefiLama meta-aggregator](https://swap.defillama.com/?chain=polygon\&from=0x2791bca1f2de4661ed88a30c99a7a9449aa84174\&to=0xb0b195aefa3650a6908f15cdac7d92f8a5791b0b)
  * [1inch](https://app.1inch.io/#/137/unified/swap/USDC/BOB)
  * [Kyberswap](https://kyberswap.com/swap/ethereum/bob-to-usdc)
  * [Paraswap](https://app.paraswap.io/#/?network=ethereum)
* Swap shielded BOB using [zkBob](../) and withdraw to an address on Polygon.
* Swap and bridge with the [Li.Fi widget](../zkbob-app/get-bob.md) directly in zkBob or at [https://jumper.exchange/](https://jumper.exchange/)

## How does BOB remain stable?

BOB token inventory is pre-minted and paired with an existing stable token (multi-collateral, for example USDC and BUSD) on decentralized exchanges featuring concentrated liquidity mechanisms (Uniswap v3, Kyberswap). The ability to set a narrow exchange rate range via ticks and provide concentrated liquidity for the pair results in very limited slippage to the stablecoin peg. [Learn More.](https://docs.uniswap.org/concepts/protocol/concentrated-liquidity)

Called an **inventory LP position**, this mechanism maintains BOB stability while providing the option for users to purchase BOB inventory.

To enter the circulating supply, BOB must be purchased from the inventory. Users can then create their own LP positions from this purchased BOB, resulting in additional **non-inventory LP positions** (BOB/WETH, BOB/GNO etc) within the ecosystem.&#x20;

## How can I view BOB basic stats (tvl, volume etc)?

The easiest way to see stats by chain is through the Uniswap interface. Overviews can also be found on [CoinGecko](https://www.coingecko.com/en/coins/bob) or [CoinMarketCap](https://coinmarketcap.com/currencies/bob/).

* [BOB on Polygon](https://app.uniswap.org/#/tokens/polygon/0xb0b195aefa3650a6908f15cdac7d92f8a5791b0b)
* [BOB on Optimism](https://app.uniswap.org/#/tokens/optimism/0xb0b195aefa3650a6908f15cdac7d92f8a5791b0b)
* [BOB on Ethereum](https://app.uniswap.org/#/tokens/ethereum/0xb0b195aefa3650a6908f15cdac7d92f8a5791b0b)
* [BOB on Arbitrum](https://app.uniswap.org/#/tokens/arbitrum/0xb0b195aefa3650a6908f15cdac7d92f8a5791b0b)

Current inventory, circulating supply as well as zkBob details can be viewed here: \
[https://dune.com/zkbob/zkbob](https://dune.com/zkbob/zkbob)

## What are the BOB contract details?

BOB token contracts start and end with B0B!

**BOB contracts on Polygon:**

* BOB Token: [0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B](https://polygonscan.com/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)&#x20;
* BOB Token Implementation: [0x98DB3A72BeF2145A8F8d8B94F81317341Af2b08C](https://polygonscan.com/address/0x98DB3A72BeF2145A8F8d8B94F81317341Af2b08C)

**BOB on Ethereum (same addresses):**&#x20;

* BOB Token: [0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B ](https://etherscan.io/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
* BOB Token Implementation: [0x98DB3A72BeF2145A8F8d8B94F81317341Af2b08C](https://etherscan.io/address/0x98DB3A72BeF2145A8F8d8B94F81317341Af2b08C)

**BOB on Optimism (same addresses):**

* BOB Token: [0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B](https://optimistic.etherscan.io/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
* BOB Token Implementation: [0x98DB3A72BeF2145A8F8d8B94F81317341Af2b08C](https://optimistic.etherscan.io/address/0x98db3a72bef2145a8f8d8b94f81317341af2b08c)

**BOB on BNB:**

* BOB Token: [0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B](https://bscscan.com/token/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
* BOB Token Implementation: [0xe0e184e850d24113ad512583b77621e35740befc](https://bscscan.com/address/0xe0e184e850d24113ad512583b77621e35740befc)&#x20;

**BOB on Arbitrum**

* BOB Token: [0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B](https://arbiscan.io/address/0xB0B195aEFA3650A6908f15CdaC7D92F8a5791B0B)
* BOB Token Implementation:[0xe0e184e850d24113ad512583b77621e35740befc](https://arbiscan.io/address/0xe0e184e850d24113ad512583b77621e35740befc)\


**BOB attributes:**

* ERC20-based fungible token
* Upgradeable & Mintable (note upgradeability account and minting account must never be the same account)
* Meta-transaction support
* EIP677 support for `transferAndCall` functionality
* Address block list capability (similar to USDC)
* Recovery function(s) for lost/mis-sent tokens

## How is BOB inventory regulated?

BOB inventory is increased in LP positions currently via a small governance multisig Safe. The goal is to balance inventory supply with demand and usage. Inventory details are described and [catalogued here](bob-governance-and-inventory/). A larger [DAO formation](bob-governance-and-inventory/bob-dao.md) is in the early stages to govern BOB minting, upgradeability and other critical operations moving forward.

## Can I earn additional BOB through zkBob or in other ways?

No, not through the protocol itself. BOB stablecoin is designed for utility and low fees. The protocol is able to collect revenue through fee collection and idle-capital compounding. These fees can then create a self-sustaining protocol which subsidizes low cost transactions for users. BOB holders can earn fees in other ways such as providing liquidity to non-inventory LP positions on DEXs like Uniswap, Quickswap and Kyberswap.

## What is the BOB public website

Explore more about BOB at [https://bob.zkbob.com/](https://bob.zkbob.com/)\


