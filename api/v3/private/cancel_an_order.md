# Cancel an order

Cancel a specific order by give order id.

> 
After cancelling an order, you can utilize the WebSocket streams for order history to continuously receive updated information about your orders in real-time.

# Api Request
**Rate Limit: `Allow `900` requests per minute per IP & UID.`**

**`DELETE` /orders/{pair}/{orderId}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path    | Query | Type   | Required | Description                                                                                                               | Default | Range | Example    |
| :------------------ | :------ | :---- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------ | :------ | :---- | :--------- |
| X-BITOPRO-APIKEY    |         |       | string | Yes      | API Key                                                                                              |         |       |            |
| X-BITOPRO-PAYLOAD   |         |       | string | Yes      | Payload                                                                                              |         |       |            |
| X-BITOPRO-SIGNATURE |         |       | string | Yes      | Signature                                                                                          |         |       |            |
|                     | pair    |       | string | Yes      | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |         |       | bito\_eth  |
|                     | orderId |       | string | Yes      | The id of the order.                                                                                                      |         |       | 2959906694 |
|                     | isAllStrategyCanceled  |  | string | No      | set to true, it will delete all strategy settings for that order. Conversely, if set to false, it will not. default value is true. |  |  | true |

# Api Response

**Response Example:**

```javascript
{
  "action": "BUY",
  "amount": "2.3",
  "orderId": "12234566",
  "price": "1.2",
  "timestamp": 1504262258000
}
```
[Back](../summary.md)