# Create Batch Orders

Create batch orders, this endpoint support to create up to `10 limit or market orders at a time`.

> 
After initiating an order, you can utilize the WebSocket streams for both open orders and order history to continuously receive updated information about your orders in real-time.


# Api Request
**Rate Limit: `Allow `90` requests per minute per IP & UID.`**

**`POST` /orders/batch**

**Headers:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query | Type   | Required | Description                       | Default | Range | Example |
| :------------------ | :--- | :---- | :----- | :------- | :-------------------------------- | :------ | :---- | :------ |
| X-BITOPRO-APIKEY    |      |       | string | Yes      | API Key     |         |       |         |
| X-BITOPRO-PAYLOAD   |      |       | string | Yes      | Payload    |         |       |         |
| X-BITOPRO-SIGNATURE |      |       | string | Yes      | Signature|         |       |         |
|                     |      |       |        |          |                                   |         |       |         |

**Parameters:**

| Field       | Type   | Required | Description                                                                                                                  | Default | Range              | Example       |
| :---------- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------- | :------ | :----------------- | :------------ |
| pair        | string | Yes      | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/fees) to check the pair list.    |         |                    | bito\_eth     |
| action      | string | Yes      | The action type of the order, should only be `BUY` or `SELL`.                                                                |         | `BUY` or `SELL`    | `BUY`         |
| amount      | string | Yes      | The base amount of the order for the trading pair. **However, when executing a market buy order, this field represents the order's quote value.** Please check [this doc](../public/get_trading_pair_info.md) for limitation. |         | > 0                | 100           |
| price       | string | Yes      | The price of the order for the trading pair.                                                                                 |         | > 0                | 10            |
| timestamp   | int64  | Yes      | The client timestamp in millisecond.                                                                                         |         |                    | 1504262258000 |
| type        | string | Yes      | The order type, should only be `LIMIT`, `MARKET`.                                                                            |
| timeInForce | string | No       | Time in force condition for orders. If type is `MARKET`, this will always be `GTC`.                                          | `GTC`   | `GTC`, `POST_ONLY` | POST_ONLY     |
| clientId    | uint64 | No       | This information help users distinguish their orders. If set to 0, it is treated the same as not providing this field (equivalent to not passing clientId). |         | 1 ~ 2147483647     | 12345         |


**Request Example:**

```javascript
[
  {
    pair: "BTC_TWD",
    action: "BUY",
    type: "LIMIT",
    price: "210000",
    amount: "1",
    timestamp: 1504262258000,
    timeInForce: "GTC",
    clientId: 123
  }, 
  {
    pair: "BTC_TWD",
    action: "SELL",
    type: "MARKET",
    amount: "2",
    timestamp: 1504262258000
  }
]
```

# Response

**Response Example:**

```javascript
{
  "data": [{
    "orderId": 1234567890,
    "action": "BUY",
    "price": "210000",
    "amount": "1",
    "timestamp": 1504262258000,
    "timeInForce": "GTC",
    "clientId": 123
  }, {
    "orderId": 3234567891,
    "action": "SELL",
    "amount": "2",
    "timestamp": 1504262258000,
    "timeInForce": "GTC"
  }]
}
```

> If `clientId` is `0` or not provided when the order was created, the `clientId` key will be omitted from the response.

[Back](../summary.md)