# Get OrderBook Data
Get the full order book of the specific pair

> If you require real-time updates or a high-frequency trading environment, we recommend using the websocket orderbook api. For more details, please refer to this [link](../../../ws/public/order_book_stream.md).

# Api Request

**`GET` /order-book/{pair}**

**Parameters:**

| Header | Path | Query | Type   | Required | Description | Default | Range | Example |
| :----- | :--- | :---- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------- | :------ | :---- | :-------- |
|        | pair |       | string | Yes      | The trading pair in format {BASE}_{QUOTE}. Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list.|  | | bito\_eth |
|        |      | limit | int32  | No       | The limit for the order book data.  | 5  | 1, 5, 10, 20, 30, 50 | 1         |
|        |      | scale | int32  | No       | The scale for the response. Valid scale values are different by pair. For more detail, please refer the field `orderBookQuoteScaleLevel` of [Get the list of available pairs](https://api.bitopro.com/v3/provisioning/trading-pairs) | 0       | [Get the list of available pairs](https://api.bitopro.com/v3/provisioning/trading-pairs) | 1         |

# Api Response

**Response Example:**
```javascript
{
  "asks": [
    {
      "amount": "10000000000",
      "count": 2,
      "price": "100000000",
      "total": "10000000000"
    }
  ],
  "bids": [
    {
      "amount": "10000000000",
      "count": 2,
      "price": "100000000",
      "total": "10000000000"
    }
  ]
}
```
[Back](../summary.md)