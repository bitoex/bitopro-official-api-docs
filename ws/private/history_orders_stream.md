# History Orders Stream
This channel pushes messages with history orders.

Note: When you initially establish a websocket connection, you will receive active orders from all trading pairs. After that, the websocket server will only push the updated history orders from the single trading pair.

# Ws Request

**`GET` wss://stream.bitopro.com:443/ws/v1/pub/auth/orders/histories**

**Authentication For Private Websocket Connection**

    | Security scheme | Header parameter    |
    | :-------------- | :------------------ |
    | API Key         | X-BITOPRO-APIKEY    |
    | Payload         | X-BITOPRO-PAYLOAD   |
    | Signature       | X-BITOPRO-SIGNATURE |
You can find how to create payload and signature from [authentication document](../../README.md#api-security-protocol).

# Ws Response

**Response:**

| 0    | Field             | Type    | Description                                                                         |
| :--- | :---------------- | :------ | :---------------------------------------------------------------------------------- |
| 0    | event             | string  | String literal for event name                                                       |
| 0    | eventID           | string  | event id for debug usage |
| 0    | timestamp         | integer | Unix Timestamp in milliseconds (seconds * 1000)                                     |
| 0    | datetime          | string  | ISO8601 datetime string with milliseconds                                           |
| 1    | id                | string  |                                                                                     |
| 1    | action            | string  | BUY or SELL                                                                         |
| 1    | price             | string  |                                                                                     |
| 1    | avgExecutionPrice | string  |                                                                                     |
| 1    | type              | string  | LIMIT, Market, STOP_LIMIT, SP_OCO_STOPLIMIT, SL_OCO_STOPLIMIT                                                        |
| 1    | createdTimestamp  | integer | Unix Timestamp in milliseconds (seconds * 1000)                                     |
| 1    | updatedTimestamp  | integer | Unix Timestamp in milliseconds (seconds * 1000)                                     |
| 1    | status            | integer | [see order status](../../model.md#order-status-enum)                                      |
| 1    | originalAmount    | string  |                                                                                     |
| 1    | remainingAmount   | string  |                                                                                     |
| 1    | executedAmount    | string  |                                                                                     |
| 1    | stopPrice         | string  |                                                                                     |
| 1    | condition         | string  | stop limit trigger condition                                                        |
| 1    | pair              | string  | lowercase string underscore-delimited literal of a pair of currencies               |
| 1    | fee               | string  |                                                                                     |
| 1    | feeSymbol         | string  |                                                                                     |
| 1    | bitoFee           | string  | bito currency fee                                                                   |
| 1    | total             | string  | total trading quote currency amount                                                 |
| 1    | seq               | string  | order sequence number                                                               |
| 1    | timeInForce       | string  | Time in force condition for orders. If type is `MARKET`, this will always be `GTC`. | `GTC` | `GTC`, `POST_ONLY` | POST_ONLY |
| 1    | clientID          | integer | This information help users distinguish their orders.                               |
 
To get detailed order model explanation, refer to [order model explanation.](../../model.md#order-model-explanation)

**Response Example:**

```javascript
{
    "event": "RECENT_HISTORY_ORDERS",
    "eventID": "dadf4ac1-665a-4f39-a139-ab95da102374",
    "timestamp": 1639552073346,
    "datetime": "2021-12-15T07:07:53.346Z",
    "data": {
        "sol_usdt": [
            {
                "id": "8917255503",
                "pair": "sol_usdt",
                "price": "107",
                "avgExecutionPrice": "0",
                "action": "SELL",
                "type": "LIMIT",
                "timestamp": 1639386803663,
                "updatedTimestamp": 1639386803663,
                "createdTimestamp": 1639386803663,
                "status": 0,
                "originalAmount": "0.02",
                "remainingAmount": "0.02",
                "executedAmount": "0",
                "fee": "0",
                "feeSymbol": "usdt",
                "bitoFee": "0",
                "total": "0",
                "seq": "SOLUSDT3273528249",
                "timeInForce": "GTC"
            }
        ],
        "usdc_twd": [
            {
                "id": "3452766477",
                "pair": "usdc_twd",
                "price": "10",
                "avgExecutionPrice": "0",
                "action": "BUY",
                "type": "LIMIT",
                "timestamp": 1638258713957,
                "updatedTimestamp": 1639386803663,
                "createdTimestamp": 1639386803663,
                "status": 0,
                "originalAmount": "0.01",
                "remainingAmount": "0.01",
                "executedAmount": "0",
                "fee": "0",
                "feeSymbol": "usdc",
                "bitoFee": "0",
                "total": "0",
                "seq": "USDCTWD2310459465"
                "timeInForce": "GTC"
            }
        ],
        "eth_twd": [
            { // SL_OCO_STOPLIMIT
              "id":"SL-397992807",
              "pair":"eth_twd",
              "price":"980",
              "avgExecutionPrice":"980",
              "action":"SELL",
              "type":"SL_OCO_STOPLIMIT",
              "timestamp":1701703883000,
              "status":2,
              "originalAmount":"1",
              "remainingAmount":"0",
              "executedAmount":"1",
              "fee":"0.588",
              "feeSymbol":"twd",
              "bitoFee":"0",
              "total":"980",
              "seq":"ETHTWD1508692221",
              "stopPrice":"980",
              "condition":"<=",
              "timeInForce":"GTC",
              "createdTimestamp":1701703831000,
              "updatedTimestamp":1701703883000,
              "stopLossesPricePercentage":"2",
              "stopProfitPricePercentage":"0",
              "parentID":"3829575872"
            }
        ]
    }
}
```
[Back](../summary.md)