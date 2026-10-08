# Cancel all orders

## `DELETE` /orders/all or /orders/{pair}

If you send a request to /orders/all API. It will cancel all your active orders of all pairs.

## Rate limit

Allow `1` requests per second per IP.

## Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | No | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |

## Response sample

```javascript
{
  "data": {
    "BTC_USDT": [
      "12234566", // cancelled orders
      "12234567"
    ],
    "ETH_USDT": [
      "44566712",
      "24552212"
    ]
  }
}
```

[Back](../rest.md)

