# Get an order

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
  "id": "SL-9014867155",
  "pair": "bito_eth",
  "price": "0.001",
  "avgExecutionPrice": "0",
  "action": "BUY",
  "type": "STOP_LIMIT",
  "timestamp": 1571032129185, // deprecated, using updatedTimestamp
  "status": -1,
  "originalAmount": "1000",
  "remainingAmount": "1000",
  "executedAmount": "0",
  "fee": "0",
  "feeSymbol": "bito",
  "bitoFee": "0",
  "total": "0",
  "seq": "BITOETH3946175424",
  "stopPrice": "0.002",
  "condition": ">=",
  "timeInForce": "GTC",
  "createdTimestamp": 1571032128185,
  "updatedTimestamp": 1571032129185
}
```

[Back](../rest.md)

