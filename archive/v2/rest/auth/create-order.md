# ~Create an order~

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**

## Create an order

### `POST` /orders/{pair}

### Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |

## Request body

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| action | string | Yes | The action type of the order, should only be `BUY` or `SELL`. |
| amount | string | Yes | The amount of the order for the trading pair, please follow the [link](https://www.bitopro.com/ns/fees) to see the limitations. |
| price | string | Yes | The price of the order for the trading pair. |
| timestamp | integer | Yes | The client timestamp in millisecond. |
| type | string | Yes | The order type, should only be `LIMIT` or `MARKET`. |

### Response sample

```javascript
{
  "orderId": 1234567890,
  "action": "BUY",
  "amount": "250",
  "price": "0.000075",
  "timestamp": 1504262258000
}
```

[Back](../rest.md)

