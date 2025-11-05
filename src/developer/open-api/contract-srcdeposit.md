---
description: Celer Intent contract interaction reference
---

# Contract: srcDeposit

### Requirements

1. Get the quote result from [rfqQuote](broken-reference) API&#x20;
2. Find the corresponding contract address here

ABI (optional if you use the binding like Typechain)

{% file src="../../.gitbook/assets/rfq.json" %}

### srcDeposit/srcDepositNative

Lock the assets to source rfq contract. if the bridge token is a native token, use the srcDepositNative.

```
// typechain method example
  srcDeposit(
    _quote: RFQ.QuoteStruct,
    _submissionDeadline: BigNumberish,
    overrides?: PayableOverrides & { from?: string | Promise<string> }
  ): Promise<ContractTransaction>;

```

#### Request Parameters

| Name                 | Type            | Description                                                              |
| -------------------- | --------------- | ------------------------------------------------------------------------ |
| \_quote              | RFQ.QuoteStruct | refer to [RFQ.QuoteStruct](broken-reference)                             |
| \_submissionDeadline | Number          | get form [rfqQuote](broken-reference) srcDeadline filed                  |
| value(msg.value)     | String          | ERC20 bridge: msgFee, Native token bridge: msgFee  + source token amount |

#### RFQ.QuoteStruct

| Name              | Type           | Description                                                                   |
| ----------------- | -------------- | ----------------------------------------------------------------------------- |
| srcChainId        | Number         | source chain id                                                               |
| srcToken          | String         | source token address                                                          |
| srcAmount         | String         | Input amount with source token decimal                                        |
| srcReleaseAmount  |                | <mark style="color:red;">NOT REQUIRED</mark>                                  |
| dstChainId        | Number         | destination chain id                                                          |
| dstToken          | String         | Destination token address                                                     |
| dstAmount         | String         | get from [rfqQuote](api-rfqquote.md#quote) dstAmount filed                    |
| deadline          | Number(Second) | get from [rfqQuote](api-rfqquote.md#quote) dstDeadline filed                  |
| nonce             | Number         | get from [rfqQuote](api-rfqquote.md#quote) nonce filed                        |
| sender            | String         | rfq contract sender address                                                   |
| receiver          | String         | receive address                                                               |
| refundTo          | String         | refund address, Usually the user wallet address.                              |
| liquidityProvider | String         | market maker address, get form [rfqQuote](api-rfqquote.md#quote) mmAddr filed |



Once the transaction submitting, same as other EVM bridge,  user history can be found in [TransferHistory](broken-reference) API, and the transaction process status can be found in [GetTransferStatus](broken-reference) API.
