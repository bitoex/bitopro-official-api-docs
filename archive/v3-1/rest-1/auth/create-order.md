# Create an order

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

| Field | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| action | string | Yes | The action type of the order. | | `BUY`, `SELL` | SELL |
| amount | string | Yes | The amount of the order for the trading pair, please follow the [link](https://www.bitopro.com/ns/fees) to see the limitations. | | | 123.25 |
| price | string | Yes | The price of the order for the trading pair. | | | 0.000075  |
| timestamp | integer | Yes | The client timestamp in millisecond. | | | 1504262258000 |
| type | string | Yes | The order type. | | `LIMIT`, `MARKET`, `STOP_LIMIT` | MARKET |
| stopPrice | string | No | The price to trigger stop limit order, **only required** when `type` is `STOP_LIMIT`. | | | 3564.2563 |
| condition | string | No | The condition to match stop price, **only required** when `type` is `STOP_LIMIT`. | | `>=`, `<=` | <= |
| timeInForce | string | No | Time in force condition for orders. If type is `MARKET`, this will always be `GTC`. | `GTC` | `GTC`, `POST_ONLY` | POST_ONLY |
| clientId | integer | No | This information help users distinguish their orders. | | 1 ~ 2147483647 | 12345 |
| percentage | integer | No | The amount of the sell order which can be percentage of your balance. (e.g 1 mean 1%) | 1~100 | 100 |

### Response sample

```javascript
{
  "orderId": 1234567890,
  "action": "BUY",
  "amount": "250",
  "price": "0.000075",
  "timestamp": 1504262258000,
  "timeInForce": "POST_ONLY",
  "clientId": 12345
}
```

[Back](../rest.md)

