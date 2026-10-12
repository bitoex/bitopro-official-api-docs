# Get Ticker Data

The ticker provides a high-level overview of the state of the market. It displays the current best bid and ask prices, along with the last traded price. Additionally, it includes information about the daily trading volume and how much the price has moved over the last day.

> If you require real-time updates or a high-frequency trading environment, we recommend using the websocket ticker data api. For more details, please refer to this [link](../../../ws/public/ticker_stream.md).

# Api Request

**`GET` /tickers/{pair}**

**Parameters:**

| Header | Path | Query | Type   | Required | Description                                                                                                                  | Default | Range | Example   |
| :----- | :--- | :---- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------- | :------ | :---- | :-------- |
|        | pair |       | string | No       | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |         |       | bito\_eth |

# Api Response

**Response Example:**
```javascript
{
  "data": [
    {
      "high24hr": "0.03252800",
      "isBuyer": false,
      "lastPrice": "0.03252800",
      "low24hr": "0.03252800",
      "pair": "eth_btc",
      "priceChange24hr": "0",
      "volume24hr": "0.00000000"
    },
    {
      "high24hr": "541.00000000",
      "isBuyer": false,
      "lastPrice": "541.00000000",
      "low24hr": "541.00000000",
      "pair": "btg_twd",
      "priceChange24hr": "0",
      "volume24hr": "0.00000000"
    }
  ]
}
```
[Back](../summary.md)