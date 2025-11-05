
# API: rfqPrice

<mark style="color:green;">`POST`</mark> `https://cbridge-prod2.celer.app/v1/rfqPrice`

#### Request Body

| Name                                        | Type   | Description                                           |
| ------------------------------------------- | ------ | ----------------------------------------------------- |
| srcToken<mark style="color:red;">\*</mark>  | JSON   | source token description                              |
| dstToken<mark style="color:red;">\*</mark>  | JSON   | destination receive token description                 |
| srcAmount<mark style="color:red;">\*</mark> | String | input amount with source token decimal                |
| dstNative<mark style="color:red;">\*</mark> | Bool   | true when destination receive token is a native token |



```javascript
// quote reponse example
{
    "price": {
        "srcToken": {
            "chainId": 5,
            "symbol": "USDC",
            "address": "0xCbE56b00d173A26a5978cE90Db2E33622fD95A28",
            "decimals": 0,
            "name": "",
            "logoUri": ""
        },
        "srcAmount": "100000000",
        "dstToken": {
            "chainId": 97,
            "symbol": "USDC",
            "address": "0x855fC87f7F14Db747ef27603b02bAe579ba947B6",
            "decimals": 0,
            "name": "",
            "logoUri": ""
        },
        "srcReleaseAmount": "99900000",
        "dstAmount": "99700000",
        "feeAmount": "200000",
        "validThru": 1665553346,
        "mmAddr": "0x58b529F9084D7eAA598EB3477Fe36064C5B7bbC1",
        "sig": "286bc92a206d79c936897a386f0a8cd1486c5f9b2cf6205ca31c7f11634029d507e681cb4a12a41f121b9d4c7bea98631cda34eeb81ae5d982a462c96d315e6100",
        "srcDepositPeriod": 250,
        "dstTransferPeriod": 720
    },
    "fee": "300000",
    "mmId": "mm003",
    "txMsgFee": "132000000000000"
}
```



## Request Parameters

| Name      | Type                                   | Description                                          |
| --------- | -------------------------------------- | ---------------------------------------------------- |
| srcToken  | [TokenInfo](api-rfqprice.md#undefined) | source token                                         |
| dstToken  | [TokenInfo](api-rfqprice.md#undefined) | receiving token on destination chain                 |
| srcAmount | String                                 | Input amount with token decimal                      |
| dstNative | Bool                                   | receiving token is native token on destination chain |

## Response Parameters

#### Response Body

<table><thead><tr><th></th><th width="249"></th><th></th></tr></thead><tbody><tr><td>price</td><td><a href="api-rfqprice.md#price">Price</a></td><td>rfq price for this quote</td></tr><tr><td>fee</td><td>string</td><td>Protocol fee + market maker charged fee</td></tr><tr><td>mmId</td><td>string</td><td>The uniq id of market marker</td></tr><tr><td>txMsgFee</td><td>string</td><td>SGN charges fees to sync, store, and sign messages</td></tr></tbody></table>

#### Price

| Name              | type                                   | Description                                                                                                                                               |
| ----------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| src token         | [TokenInfo](api-rfqprice.md#undefined) | Source token information                                                                                                                                  |
| dst token         | [TokenInfo](api-rfqprice.md#undefined) | Destination receive token information                                                                                                                     |
| srcAmount         | string                                 | Input amount with src token decimal                                                                                                                       |
| dstAmount         | string                                 | Estimated received amount on destination chain                                                                                                            |
| feeAmount         | string                                 | market maker fee + msg fee + src tx gas cost + dst tx gas cost                                                                                            |
| validThru         | timestamp                              | Unix epoch milliseconds. the time before which the price response is valid for Quote                                                                      |
| mmAddr            | string                                 | Market maker address                                                                                                                                      |
| sig               | string                                 | Market marker uses this signature to verify the price content is agreed by them previously                                                                |
| srcDepositPeriod  | number                                 | Unit second. The maximum src deposit period that is expected by  market maker, will be started from the time when mm receives the quote request.          |
| dstTransferPeriod | number                                 | Unit second. The minimum destination transfer period that is expected by market maker, will be started from the time when mm receives the quote request.  |

#### TokenInfo

| Name      | Type   | Description   |
| --------- | ------ | ------------- |
| chain\_id | number | Chain id      |
| symbol    | string | Token Symbol  |
| address   | string | Token address |
