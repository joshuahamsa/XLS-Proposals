<pre>
Title:       <b>NFToken Trading</b>
Revision:    <b>1</b> (2024-08-23)

Author:      <a href="mailto:josh.hamsa@gmail.com">Joshua Hamsa</a>

Affiliation: <a href="https://letseffinggo.com">LFGO</a>
</pre>

# NFToken Trading

## Abstract
This proposal expands the `NFTokenOfferCreate` transactor to allow for an `NFTokenID` to be used as a medium of exchange. Currently only fungible tokens are supported to create an `NFTokenOffer` ledger object, which provides unneccesary friction for users who want to trade NFTs. 

The lack of this functionality has not stopped trading; instead requiring trust between two users or the inclusion of a mutually trusted third party to complete Peer-to-Peer trades. While this proposal creates a route for avoiding enforced royalties, the issue is moot when users trade P2P anyhow. 

By removing this limitation, the XRPL will be the first distributed ledger to support on-chain bartering as a means of exchanging value in a secure, trustless, auditable manner.


## 1. Overview

We propose:
* Modifying `NFTokenOfferCreate` transaction type.
* Modifying `NFTokenOffer` ledger object.

This feature will require an amendment, tentatively titled `NFTokenTrading`.

## 2. On-Ledger Object: `NFTokenOffer`

`NFTokenOffer` is an existing On-Ledger Object that is created when a user submits a valid `NFTokenOfferCreate` transaction. 

### 2.1. Fields

| Field Name | Required? | JSON Type | Internal Type | Description |
|------------|-----------|-----------|---------------|-------------|
|`LedgerIndex`| ✔️|`string`|`Hash256`|The unique ID of theledger object.|
|`LedgerEntryType`| ✔️|`string`|`UInt16`|The ledger object's type (`NFTokenOffer`).|
|`Account`| ✔️|`string`|`AccountID`|The account that created the offer.|
|`OwnerAccount`| ✔️|`string`|`AccountID`|The account received the offer.|
|`NFTokenID`| ✔️|`string`|`UInt16`|The NFT owned by the counter-party.|
|`NFTokenIssuer`| ✔️|`string`|`UInt16`|The issuer of the counter-party's NFT.|
|`Currency`| ✔️|`string`|`STArray`|The medium of exchange.|

#### 2.1.1. Object ID

#### 2.1.2.

### 2.2. Account Deletion

The `NFTokenOffer` object is not a [deletion blocker](https://xrpl.org/docs/concepts/accounts/deleting-accounts/#requirements).

## 3. Transaction: `NFTokenOfferCreate`

When offers are created using a non-XRP token / Issued Asset, the Array already requires the inclusion of the Issuer and the token ID (ticker) in hexadecimal format. By including the appropriate `Flag` the ledger recognizes that the ID string belongs to an `NFTokenID`.

### 3.1. Fields

| Field Name | Required? | JSON Type | Internal Type | Description |
|------------|-----------|-----------|---------------|-------------|
|`TransactionType`| ✔️|`string`|`UInt16`|The transaction type (`NFTokenOfferCreate`).|
|`Account`| ✔️|`string`|`AccountID`|The account sending the transaction.|
|`OwnerAccount`| ✔️|`string`|`AccountID`|The account receiving the transaction.|
|`LedgerIndex`| ✔️|`string`|`Hash256`|The unique ID of theledger object.|
|`NFTokenID`| ✔️|`string`|`UInt16`|The NFT owned by the counter-party.|
|`NFTokenIssuer`| ✔️|`string`|`UInt16`|The issuer of the counter-party's NFT.|
|`Currency`| ✔️|`string`|`STArray`|The medium of exchange.|

#### 3.1.1. 

### 3.2. Failure Conditions
The transaction will fail if:
* The Sender does not own the NFTokenID they are offering.
* The Receiver does not own the NFTokenID the offer is being made on.
* Either NFTokenID has the Non-Transferrable Flag set to True.

### 3.3. State Changes

If the transaction is successful:
* The 

## 4. RPC:

### 4.1. Request Fields

| Field Name | Required? | JSON Type | Description |
|------------|-----------|-----------|-------------|
|`account`|✔️|`string`|The account.|

### 4.2. Response Fields

| Field Name | Always Present? | JSON Type | Description |
|------------|-----------------|-----------|------------|
|`account`|✔️|`string`|The account.|

<!--
## 5. Examples
Chris won an NFT with a trait he is not collecting. Becky wanted to win and owns an NFT that Chris wants. Becky offers to trade her NFT for Chris's prize. 

## 6. Invariants

## 7. Security
-->

<!--
## n+1. Open Questions


<!--
# Appendix

## Appendix A: FAQ

### A.1: 

<!--
# Appendix B: Alternate Designs
