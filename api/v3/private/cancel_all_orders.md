# Cancel All Orders

Cancel all open orders. 

> 
After cancelling an order, you can utilize the WebSocket streams for order history to continuously receive updated information about your orders in real-time.

# Api Request

**Rate Limit: `Allow `2` requests per second per IP & UID.`**

**`DELETE` /orders/all or /orders/{pair}**

If you send a request to /orders/all API. It will cancel all your active orders of all pairs.

**Rate limit:**
Allow `1` requests per second per IP.

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query | Type   | Required | Description                                                                                                               | Default | Range | Example   |
| :------------------ | :--- | :---- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------ | :------ | :---- | :-------- |
| X-BITOPRO-APIKEY    |      |       | string | Yes      | API Key                                                                                             |         |       |           |
| X-BITOPRO-PAYLOAD   |      |       | string | Yes      | Payload                                    |         |       |           |
| X-BITOPRO-SIGNATURE |      |       | string | Yes      | Signature                              |         |       |           |
|                     | pair |       | string | No       | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |         |       | bito\_eth |

# Api Response

**Response Example:**

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
[Back](../summary.md)
