# Get all orders

## `GET` /orders/all/{pair}

Fetches all orders of specific pair within 90 days, and ordered by create time.

## Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |
|  |  | startTimestamp | integer | No | The start time of orders. | 90 days |  | 1605857448852 |
|  |  | endTimestamp | integer | No | The end time of orders. | current timestamp |  | 1605857448852 |
|  |  | statusKind | string | No | Filter order based on status kind, `OPEN` all active orders, `DONE` all finished orders, `ALL` for all. `OPEN` includes order status of -1, 0 and 1, `DONE` includes order status of 2 and 3. For order status, [see](../rest.md#order-status)| `ALL` | `OPEN`, `DONE`, `ALL` | ALL |
|  |  | status | int | No | Filter order base on specific status. Take precedence over `statusKind`. |  | See [status](../rest.md#order-status) | -1 |
|  |  | orderId | string | No | If specified, list starts with order with id >= `orderId`. | | | 6432441674 |
|  |  | limit | integer | No | The number of records to retrieve. | 100 | 1 ~ 1000 | 100 |
| | | clientId | integer | No | This information help users distinguish their orders. | | 1 ~ 2147483647 | 12345 |


`startTimstamp` and `endTimestamp` can only be 90 days apart. If range greater than 90 days, parameter will be adjusted accordingly and behavior is not defined. If both are not defined, `startTimestamp` is defined as 90 days before from current time, and `endTimestamp` is defined as current time.

## Response sample

```javascript
{
  "data": [
    {
      "action": "BUY",
      "avgExecutionPrice": "0",
      "bitoFee": "0",
      "executedAmount": "0",
      "fee": "0",
      "feeSymbol": "bito",
      "id": "887521192",
      "originalAmount": "1000",
      "pair": "bito_eth",
      "price": "0.005",
      "remainingAmount": "1000",
      "seq": "BITOETH8913789893",
      "status": 0,
      "createdTimestamp": 1570591525592,
      "updatedTimestamp": 1570601523551,
      "total": "0",
      "type": "LIMIT",
      "timeInForce": "GTC",
      "clientId": 123
    },
    {
      "action": "BUY",
      "avgExecutionPrice": "0",
      "bitoFee": "0",
      "condition": ">=",
      "executedAmount": "0",
      "fee": "0",
      "feeSymbol": "bito",
      "id": "SL-1133804403",
      "originalAmount": "1000",
      "pair": "bito_eth",
      "price": "0.05",
      "remainingAmount": "1000",
      "seq": "BITOETH4618822599",
      "status": -1,
      "stopPrice": "10",
      "timestamp": 1570591225827,
      "total": "0",
      "type": "STOP_LIMIT",
      "timeInForce": "GTC",
      "clientId": 123
    },
    {
      "action": "BUY",
      "avgExecutionPrice": "0",
      "bitoFee": "0",
      "condition": ">=",
      "executedAmount": "0",
      "fee": "0",
      "feeSymbol": "bito",
      "id": "SL-6256946008",
      "originalAmount": "1000",
      "pair": "bito_eth",
      "price": "0.05",
      "remainingAmount": "1000",
      "seq": "BITOETH2471338952",
      "status": -1,
      "stopPrice": "10",
      "createdTimestamp": 1570591525690,
      "updatedTimestamp": 1570601523550,
      "total": "0",
      "type": "STOP_LIMIT",
      "timeInForce": "GTC",
      "clientId": 123
    }
  ]
}
```

[Back](../rest.md)

