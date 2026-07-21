# Create An Order

Create an order api, this endpoint support to limit, market and stop-limit order. 

> 
After initiating an order, you can utilize the WebSocket streams for both [open orders](../../../ws/private/open_order_stream.md) and [history orders](../../../ws/private/history_order_stream.md) to continuously receive updated information about your orders in real-time.



# Api Request

**Rate Limit: `Allow `1200` requests per minute per IP & UID.`**

**`POST` /orders/{pair}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query | Type   | Required | Description                                                                                                               | Default | Range | Example   |
| :------------------ | :--- | :---- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------ | :------ | :---- | :-------- |
| X-BITOPRO-APIKEY    |      |       | string | Yes      | API Key                                                                                             |         |       |           |
| X-BITOPRO-PAYLOAD   |      |       | string | Yes      | Payload                                                                                         |         |       |           |
| X-BITOPRO-SIGNATURE |      |       | string | Yes      | Signature                                                                                     |         |       |           |
|                     | pair |       | string | Yes      | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/fees) to check the pair list. |         |       | bito\_eth |

**Request body:**

| Field       | Type    | Required | Description                                                                                                                  | Default | Range                           | Example       |
| :---------- | :------ | :------- | :--------------------------------------------------------------------------------------------------------------------------- | :------ | :------------------------------ | :------------ |
| action      | string  | Yes      | The action type of the order.                                                                                                |         | `BUY`, `SELL`                   | SELL          |
| amount      | string  | Yes      | The base amount of the order for the trading pair. **However, when executing a market buy order, this field represents the order's quote value.** Please check [this doc](../public/get_trading_pair_info.md) for limitation.  |         |                                 | 123.25        |
| price       | string  | Yes (No when `MARKET` type order )     | The price of the order for the trading pair.                                                   |         |                                 | 0.000075      |
| timestamp   | integer | Yes      | The client timestamp in millisecond.                                                                                         |         |                                 | 1504262258000 |
| type        | string  | Yes      | The order type.                                                                                                              |         | `LIMIT`, `MARKET`, `STOP_LIMIT` | MARKET        |
| stopPrice   | string  | No       | The price to trigger stop limit order, **only required** when `type` is `STOP_LIMIT`.                                        |         |                                 | 3564.2563     |
| condition   | string  | No       | The condition to match stop price, **only required** when `type` is `STOP_LIMIT`.                                            |         | `>=`, `<=`                      | <=            |
| timeInForce | string  | No       | Time in force condition for orders. If type are `MARKET`, `STOP_LIMIT`, this will always be `GTC`.                                          | `GTC`   | `GTC`, `POST_ONLY`              | POST_ONLY     |
| clientId    | uint64  | No       | This information help users distinguish their orders. If set to 0, it is treated the same as not providing this field (equivalent to not passing clientId). |         | 1 ~ 2147483647                  | 12345         |
| percentage  | uint64  | No       | The amount of the sell order which can be percentage of your balance. (e.g 1 mean 1%)                                        | 1~100   | 100                             |

# Api Response

**Response Body:**

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

> If `clientId` is `0` or not provided when the order was created, the `clientId` key will be omitted from the response.

[Back](../summary.md)