---
description: >-
  Quote the Celer Intent system to get the call data for Celer Intent
  transaction submitting
---

# API: rfqQuote

<mark style="color:green;">`POST`</mark> `https://cbridge-prod2.celer.app/v1/rfqQuote`

#### Request Body

| Name                                          | Type   | Description                                               |
| --------------------------------------------- | ------ | --------------------------------------------------------- |
| price<mark style="color:red;">\*</mark>       | JSON   | refer to the [Price Table](broken-reference)              |
| mmId<mark style="color:red;">\*</mark>        | String | market marker uniq id                                     |
| sender<mark style="color:red;">\*</mark>      | String | user wallet address                                       |
| receiver<mark style="color:red;">\*</mark>    | String | wallet address who receive the token on destination chain |
| refundTo<mark style="color:red;">\*</mark>    | String | refund address when source transaction failed             |
| srcDeadline<mark style="color:red;">\*</mark> | Number | srcDepositPeriod (price struct) + current timestamp       |
| dstDeadline<mark style="color:red;">\*</mark> | Number | dstTransferPeriod (price struct) + current timestamp      |
| srcNative<mark style="color:red;">\*</mark>   | Bool   | true when source token is a native token                  |
| dstNative<mark style="color:red;">\*</mark>   | Bool   | true when destination receive token is a native token     |

{% tabs %}
{% tab title="200: OK " %}
```json
// Response example
{
    "srcTokenUsdPrice": 1,
    "dstTokenUsdPrice": 1,
    "quote": {
        "hash": "0x99f8c9969000a8adca8282d278853dcbd822f48873152b2c951317173d656eb1",
        "srcToken": {
            "chainId": 5,
            "symbol": "USDC",
            "address": "0xCbE56b00d173A26a5978cE90Db2E33622fD95A28",
            "decimals": 6,
            "name": "USD Coin",
            "logoUri": "https://get.celer.app/cbridge-icons/USDC.png"
        },
        "srcAmount": "100000000",
        "srcReleaseAmount": "99900000",
        "dstToken": {
            "chainId": 97,
            "symbol": "USDC",
            "address": "0x855fC87f7F14Db747ef27603b02bAe579ba947B6",
            "decimals": 6,
            "name": "",
            "logoUri": ""
        },
        "dstAmount": "98826590",
        "srcDeadline": 1665563808,
        "dstDeadline": 1665564278,
        "nonce": 718699599,
        "sender": "0x82571c922D3FAaf48df53C74bB0f116e48C34f93",
        "receiver": "0x82571c922D3FAaf48df53C74bB0f116e48C34f93",
        "refundTo": "0x82571c922D3FAaf48df53C74bB0f116e48C34f93",
        "mmAddr": "0x58b529F9084D7eAA598EB3477Fe36064C5B7bbC1"
    }
}
```
{% endtab %}
{% endtabs %}

## Request Parameters

| Name        | Type                           | Description                                                                         |
| ----------- | ------------------------------ | ----------------------------------------------------------------------------------- |
| price       | [Price](api-rfqprice.md#price) |                                                                                     |
| mmId        | String                         | market marker uniq id                                                               |
| sender      | String                         | user wallet address                                                                 |
| receiver    | String                         | wallet address who receive the token on destination chain                           |
| refundTo    | String                         | refund address when source transaction failed                                       |
| srcDeadline | Number(Second)                 | srcDepositPeriod (from [priceRfq](broken-reference)) + current timestamp in second  |
| dstDeadline | Number(Second)                 | dstTransferPeriod (from [priceRfq](broken-reference)) + current timestamp in second |
| srcNative   | Bool                           | true when source token is a native token                                            |
| dstNative   | Bool                           | true when destination receive token is a native token                               |

### Response Parameters

| Name             | Type                           | Description                 |
| ---------------- | ------------------------------ | --------------------------- |
| srcTokenUsdPrice | String                         | source token usd price      |
| dstTokenUsdPrice | String                         | destination token usd price |
| quote            | [Quote](api-rfqquote.md#quote) |                             |

#### Quote

| Name        | Type                                   | Description                                                                              |
| ----------- | -------------------------------------- | ---------------------------------------------------------------------------------------- |
| hash        | String                                 | The quote hash, uniq id to mark this quote.                                              |
| srcToken    | [TokenInfo](api-rfqprice.md#tokeninfo) | source token                                                                             |
| srcAmount   | String                                 | Input amount with source token decimal                                                   |
| dstToken    | [TokenInfo](api-rfqprice.md#tokeninfo) | Receiving token on destination chain                                                     |
| dstAmount   | String                                 | quote received amount                                                                    |
| srcDeadline | Number(Second)                         | srcDepositPeriod (from [rfqPrice](api-rfqprice.md#price) API) + current timestamp        |
| dstDeadline | Number(Second)                         | dstTransferPeriod (from [priceRfq](api-rfqprice.md#price)) + current timestamp in second |
| nonce       | Number                                 | nonce for rfq contract transaction calling                                               |
| sender      | String                                 | sender address                                                                           |
| receiver    | String                                 | receive address                                                                          |
| refundTo    | String                                 | refund address when source transaction failed                                            |
| mmAddr      | String                                 | market marker address                                                                    |
