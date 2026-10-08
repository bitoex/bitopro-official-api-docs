# Get OHLC Data

Get open, high, low, close data in a period

# Api Request

**`GET` /trading-history/{pair}**

**Parameters:**

| Header | Path | Query      | Type   | Required | Description                                                                                                               | Default | Range                                             | Example    |
| :----- | :--- | :--------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------ | :------ | :------------------------------------------------ | :--------- |
|        | pair |            | string | Yes      | The trading pair in format {BASE}_{QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |         |                                                   | bito\_eth  |
|        |      | resolution | string | Yes      | Timeframe of the candlestick chart.                                                                                       |         | 1m, 5m, 15m, 30m, 1h, 3h, 4h, 6h, 12h, 1d, 1w, 1M | 1h         |
|        |      | from       | int64  | Yes      | Start time in unix timestamp.                                                                                             |         |                                                   | 1550822974 |
|        |      | to         | int64  | Yes      | End time in unix timestamp.                                                                                               |         |                                                   | 1566375034 |

⚠️ Note: 1m and 5m resolution only provide data for the last 365 days

# Api Response

**Response Example:**

```javascript
{
 "data": [
  {
   "timestamp": 1551052800000,
   "open": "4099.99",
   "high": "4444.47",
   "low": "3875.32",
   "close": "3955.8",
   "volume": "13.35162928"
  },
  {
   "timestamp": 1552262400000,
   "open": "4000",
   "high": "111111111.11",
   "low": "3955.8",
   "close": "3955.8",
   "volume": "2.00500074"
  },
  ...
 ]
}
```
[Back](../summary.md)