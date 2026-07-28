# Get Orders Data

Fetches all orders of specific pair within 90 days, and ordered by create time desc.

If you need real-time updates to obtain unfilled orders, we recommend using the websocket open orders api. For more details, please refer to this [link](../../../ws/private/open_orders_stream.md).


# Api Request
**`GET` /orders/all/{pair}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query          | Type   | Required | Description                                                                                                                                                                                                                                    | Default           | Range                                 | Example       |
| :------------------ | :--- | :------------- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------- | :------------------------------------ | :------------ |
| X-BITOPRO-APIKEY    |      |                | string | Yes      | API Key                                                                                                                                                                                                                   |                   |                                       |               |
| X-BITOPRO-PAYLOAD   |      |                | string | Yes      | Payload                                                                                                                                                                                                                  |                   |                                       |               |
| X-BITOPRO-SIGNATURE |      |                | string | Yes      | Signature                                                                                                                                                                                                              |                   |                                       |               |
|                     | pair |                | string | Yes      | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/fees) to check the pair list.                                                                                                                   |                   |                                       | bito\_eth     |
|                     |      | startTimestamp | int64  | No       | The start time of orders.                                                                                                                                                                                                                      | 90 days           |                                       | 1605857448852 |
|                     |      | endTimestamp   | int64  | No       | The end time of orders.                                                                                                                                                                                                                        | current timestamp |                                       | 1605857448852 |
|                     |      | statusKind     | string | No       | Filter order based on status kind, `OPEN` all active orders, `DONE` all finished orders, `ALL` for all. `OPEN` includes order status of -1, 0 and 1, `DONE` includes order status of 2 and 3. For order status, [see](../../../model.md#order-status-explanation) | `ALL`             | `OPEN`, `DONE`, `ALL`                 | ALL           |
|                     |      | status         | int32  | No       | Filter order base on specific status. Take precedence over `statusKind`.                                                                                                                                                                       |                   | See [status](../../../model.md#order-status-explanation) | -1            |
|                     |      | orderId        | string | No       | If specified, list starts with order with id `<=` `orderId`.                                                                                                                                                                                     |                   |                                       | 6432441674    |
|                     |      | limit          | int32  | No       | The number of records to retrieve.                                                                                                                                                                                                             | 100               | 1 ~ 1000                              | 100           |
|                     |      | clientId       | int32  | No       | This information help users distinguish their orders. If set to 0, it is treated the same as not providing this filter (i.e. no clientId filter is applied and orders of all clientId values are returned).                                    |                   | 1 ~ 2147483647                        | 12345         |
| | | ignoreTimeLimitEnable | bool | No | This parameter can only be used with the `query orders with OPEN status`. If set to true, it will respond with all open orders without a time range limitation. | | | false |

The `startTimestamp` and `endTimestamp` can only be 90 days apart. If the range is greater than 90 days, the parameter will be adjusted accordingly, and the behavior is undefined. If both `startTimestamp` and `endTimestamp` are not defined, `startTimestamp` will be set to 90 days before the current time, and `endTimestamp` will be set to the current time.

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
    },
    { // LIMIT order with SP_OCO_STOPLIMIT setting
      "id":"6202635890",
      "pair":"eth_twd",
      "price":"100",
      "avgExecutionPrice":"100",
      "action":"BUY",
      "type":"LIMIT",
      "createdTimestamp":1707039441341,
      "updatedTimestamp":1707039510358,
      "status":2,
      "originalAmount":"1",
      "remainingAmount":"0",
      "executedAmount":"1",
      "fee":"0.0006",
      "feeSymbol":"eth",
      "bitoFee":"0",
      "total":"100",
      "seq":"ETHTWD7445691022",
      "timeInForce":"GTC",
      "stopProfitSetting":
      {
        "stopPrice":"100",
        "price":"220",
        "pricePercentage":"120.000",
        "priceInputType":2,
        "strategiesID":"6263708251",
        "strategySettingID":"401717013",
        "orderID":"SL-648784180",
        "parentOrderID":"6202635890"
      }
    },
    { // SL_OCO_STOPLIMIT order
      "id":"SL-648784180",
      "pair":"eth_twd",
      "price":"220",
      "avgExecutionPrice":"220",
      "action":"SELL",
      "type":"SP_OCO_STOPLIMIT",
      "createdTimestamp":1707039510455,
      "updatedTimestamp":1707039580165,
      "status":2,
      "originalAmount":"0.9994",
      "remainingAmount":"0",
      "executedAmount":"0.9994",
      "fee":"0.1319208",
      "feeSymbol":"twd",
      "bitoFee":"0",
      "total":"219.868",
      "seq":"ETHTWD1740658317",
      "condition":">=",
      "timeInForce":"GTC",
      "selfOrderStrategySetting":
      {
        "orderStrategySettingID":"401717013",
        "orderStrategiesID":"6263708251",
        "parentOrderID":"6202635890",
        "orderID":"SL-648784180",
        "condition":">=",
        "stopPrice":"100",
        "price":"220",
        "pricePercentage":"120.000",
        "amount":"0.9994",
        "timestamp":1707039441000,
        "orderType":3,
        "priceInputType":2,
        "triggeredTimestamp":1707039510000,
        "base":"eth",
        "quote":"twd"
      }
    },
    { // LIMIT order with SL_OCO_STOPLIMIT setting
      "id":"4391867898",
      "pair":"btc_twd",
      "price":"100",
      "avgExecutionPrice":"100",
      "action":"BUY",
      "type":"LIMIT",
      "createdTimestamp":1707039634662,
      "updatedTimestamp":1707039779521,
      "status":2,
      "originalAmount":"1",
      "remainingAmount":"0",
      "executedAmount":"1",
      "fee":"0.0006",
      "feeSymbol":"btc",
      "bitoFee":"0",
      "total":"100",
      "seq":"BTCTWD1796315895",
      "timeInForce":"GTC",
      "stopLossSetting":
      {
        "stopPrice":"90",
        "price":"90",
        "pricePercentage":"10.000",
        "priceInputType":1,
        "strategiesID":"1140566646",
        "strategySettingID":"5278575407",
        "orderID":"SL-9277712889",
        "parentOrderID":"4391867898"
      }
    },
    { // SL_OCO_STOPLIMIT order
      "id":"SL-9277712889",
      "pair":"btc_twd",
      "price":"90",
      "avgExecutionPrice":"90",
      "action":"SELL",
      "type":"SL_OCO_STOPLIMIT",
      "createdTimestamp":1707039779597,
      "updatedTimestamp":1707039856455,
      "status":2,
      "originalAmount":"0.9994",
      "remainingAmount":"0",
      "executedAmount":"0.9994",
      "fee":"0.0539676",
      "feeSymbol":"twd",
      "bitoFee":"0",
      "total":"89.946",
      "seq":"BTCTWD6091283189",
      "condition":"<=",
      "timeInForce":"GTC",
      "selfOrderStrategySetting":
      {
        "orderStrategySettingID":"5278575407",
        "orderStrategiesID":"1140566646",
        "parentOrderID":"4391867898",
        "orderID":"SL-9277712889",
        "condition":"<=",
        "stopPrice":"90",
        "price":"90",
        "pricePercentage":"10.000",
        "amount":"0.9994",
        "timestamp":1707039634000,
        "orderType":4,
        "priceInputType":1,
        "triggeredTimestamp":1707039779000,
        "base":"btc",
        "quote":"twd"
      }
    }
  ]
}
```
[Back](README.md)