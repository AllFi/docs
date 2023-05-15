---
description: When deriving a zkBob account using MetaMask
---

# Metamask / Web3 Wallet Warning

zkBob provides a convenient method to create an account using Metamask (MM) or another web3 wallet using Wallet Connect. When deriving an account with a web3 wallet there is no need to write down or remember a new secret phrase for your shielded account.&#x20;

<figure><img src="../../.gitbook/assets/mm-wc.png" alt=""><figcaption></figcaption></figure>

With this method, a zkBob private key is derived using your Metamask private key. You sign a message to enable this derivation. There is no fee, the operation is performed on your local machine and nothing is sent to the blockchain. The zkBob application collects your signature and creates a private key for the shielded account.&#x20;

No one can reproduce the signature without access to your Metamask private key. If you change your browser or device, simply authorize Metamask and sign the same message in the zkBob application to get access to your shielded funds.&#x20;

This method is secure and anonymous; it is not possible to reveal your private key through signature analysis.

{% hint style="danger" %}
**Security Warning**

Be vigilant when using Metamask or another web3 wallet, as an adversary can ask you to sign the _same message_ on a spoofed site.

If you provide a signature to the attacker your zkBob private key is leaked and the attacker can steal all funds from the zkBob account. To protect against this threat you must always **check the source URL** sending the signing request.&#x20;

The genuine application is hosted on [**https://app.zkbob.com/**](https://app.zkbob.com/) only.

<img src="../../.gitbook/assets/sig-origin-request (1).png" alt="" data-size="original">
{% endhint %}
