# Get Open Orders Data

Fetches all open orders and descending ordered by updated time.

If you need real-time updates to obtain unfilled orders, we recommend using the websocket open orders api. For more details, please refer to this [link](../../../ws/private/open_orders_stream.md).


# Api Request

**Rate Limit: `Allow `5` requests per second per IP & UID.`**

**`GET` /orders/open**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query          | Type   | Required | Description                                                                                                                                                                                                                                    | Default           | Range                                 | Example       |
| :------------------ | :--- | :------------- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------- | :------------------------------------ | :------------ |
| X-BITOPRO-APIKEY    |      |                | string | Yes      | API Key                                                                                                                                                                                                                   |                   |                                       |               |
| X-BITOPRO-PAYLOAD   |      |                | string | Yes      | Payload                                                                                                                                                                                                                  |                   |                                       |               |
| X-BITOPRO-SIGNATURE |      |                | string | Yes      | Signature                                                                                                                                                                                                              |                   |                                       |               |
|                     |  |  pair  | string | No      | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. Response all pair orders if pair is empty.                                                                                                                    |                   |                                       | bito\_eth     |

# Api Response

To get detailed order model explanation, refer to [order model explanation.](../../../model.md#order-model-explanation)

**Response Example:**
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
      "id": "SL-1133804403",
      "originalAmount": "1000",
      "pair": "bito_eth",
      "price": "0.05",
      "remainingAmount": "1000",
      "seq": "BITOETH4618822599",
      "status": -1,
      "createdTimestamp": 1570591525690,
      "updatedTimestamp": 1570601523550,
      "total": "0",
      "type": "LIMIT",
      "timeInForce": "GTC",
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
[Back](../summary.md)