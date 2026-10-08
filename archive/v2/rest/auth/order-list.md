# ~Get order list~

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**


## Deprecated, use [All Orders](https://github.com/bitoex/bitopro-offical-api-docs/tree/fce0d2ff98b20e331fedb24319dfdbc3ad49edaf/v3-1/rest-1/auth/all-order.md) instead

## Get order list

### `GET` /orders/{pair}

### Rate limit

Allow `1` request per second per IP.

### Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |
|  |  | page | integer | No | The page number for the query. | 1 |  | 1 |
|  |  | active | bool | No | The flag to specify if only active\(in progress\) orders will return. | `false` | `true`, `false` | true |

### Response sample

```javascript
{
  "data": [
    {
      "action": "BUY",
      "avgExecutionPrice": "100000.00000000",
      "bitoFee": "0.00000000",
      "executedAmount": "1.00000000",
      "fee": "0.00100000",
      "feeSymbol": "BTC",
      "id": "123",
      "originalAmount": "1.00000000",
      "pair": "btc_twd",
      "price": "100000.00000000",
      "remainingAmount": "0.00000000",
      "status": 2,
      "timestamp": 1508753757000,
      "type": "LIMIT",
      "total": "123.00"
    },
    {
      "action": "BUY",
      "avgExecutionPrice": "100000.00000000",
      "bitoFee": "0.00000000",
      "executedAmount": "1.00000000",
      "fee": "0.00200000",
      "feeSymbol": "BTC",
      "id": "456",
      "originalAmount": "1.00000000",
      "pair": "btc_twd",
      "price": "100000.00000000",
      "remainingAmount": "0.00000000",
      "status": 2,
      "timestamp": 1508753787000,
      "type": "LIMIT",
      "total": "123.00"
    }
  ],
  "page": 1,
  "totalPages": 10
}
```

[Back](../rest.md)

