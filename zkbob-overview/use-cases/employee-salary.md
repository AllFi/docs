# Employee Salary

Businesses often prefer to keep salary information private. This creates issues for some businesses who want to use blockchain for payments but also want to keep salary information confidential.  With zkBob, employers can keep information private and use the blockchain to send salaries.&#x20;

Several prominent projects in the ecosystem are already using zkBob for salary payments. These [Tier 1](../deposit-and-withdrawal-limits.md#tiered-limits) projects are able to deposit higher amounts of BOB into the protocol for sending salary to known employees of the business. Since employees are KYC'd by their employers, this KYC is automatically inherited into the protocol.

Upcoming multi-sender functionality and integrations with projects like [Request Finance](https://request.network/en/) will make salary processing even easier as more users onboard to zkBob.

## Generic Use Case: Carl :man\_office\_worker: the Small Business Employer

<figure><img src="../../.gitbook/assets/Carl small business.png" alt=""><figcaption><p>Carl pays his employees through zkBob for stability and privacy purposes.</p></figcaption></figure>

Carl has 5 employees he pays monthly with crypto. Carl’s preference is to keep salaries private while still processing them on-chain and using a stable asset for payment. zkBob makes it easy.

1. Carl and his employees each create their own zkBob zkAccounts, using either a seed phrase or wallet private key.
2. Carl swaps his monthly amount of payment in USDC for BOB stable tokens on Uniswap v3 on Polygon.
3. Carl deposits the BOB he receives into the zkBob application.
4. Each employee sends Carl their zkAddress in a private DM on Slack.
5. Carl transfers BOB to each employee for their monthly salary.
6. Once it is received (or at a later time to improve anonymity) employees withdraw any amount of BOB into a 0x wallet on Polygon. This can be a brand new address (which is also sent 0.1 MATIC for txs) or a prior 0x address.
7. &#x20;Employees can convert their BOB to a coin/token of their choice, and use however they wish (ie send to an exchange, bank, pay with crypto etc). &#x20;
8. The history tab within each account makes it easy for employees to track and report their own transfers and withdrawals.
9. The process is repeated monthly, with employees DM’ing Carl a newly generated zkAddress at the beginning of each month.&#x20;