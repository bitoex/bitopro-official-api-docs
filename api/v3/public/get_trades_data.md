# Get Trades Data

Get a list of the most recent trades for the given symbol.

If you require real-time updates or a high-frequency trading environment, we recommend using the websocket trade api. For more details, please refer to this [link](../../../ws/public/trade_stream.md).

# Api Request

**`GET` /trades/{pair}**

**Parameters:**

| Header | Path | Query | Type   | Required | Description                                                                                                               | Default | Range | Example   |
| :----- | :--- | :---- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------ | :------ | :---- | :-------- |
|        | pair |       | string | Yes      | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |         |       | bito\_eth |

# Api Response

**Response Example:**
```javascript
{
  "data": [
    {
      "amount": "0.11000000",
      "isBuyer": false,
      "price": "126709.00000000",
      "timestamp": 1551753875
    },
    {
      "amount": "0.10000000",
      "isBuyer": false,
      "price": "126787.00000000",
      "timestamp": 1551753796
    }
  ]
}
```
[Back](../summary.md)