# ~Get an order~

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**

## `GET` /orders/{pair}/{orderId}

## Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |
|  | orderId |  | string | Yes | The id of the order. |  |  | 2959906694 |

## Response sample

```javascript
{
  "action": "SELL",
  "avgExecutionPrice": "112000.00000000",
  "bitoFee": "103.70370360",
  "executedAmount": "1.00000000",
  "fee": "0.00000000",
  "feeSymbol": "TWD",
  "id": "123",
  "originalAmount": "1.00000000",
  "pair": "btc_twd",
  "price": "112000.00000000",
  "remainingAmount": "0.00000000",
  "status": 2,
  "timestamp": 1508753757000,
  "type": "LIMIT",
  "total": "123.00"
}
```

[Back](../rest.md)

