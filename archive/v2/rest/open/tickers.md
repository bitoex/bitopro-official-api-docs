# ~Get tickers~

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**

### The ticker is a high level overview of the state of the market. It shows you the current best bid and ask, as well as the last trade price. It also includes information such as daily volume and how much the price has moved over the last day

## `GET` /tickers/{pair}

## Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  | pair |  | string | No | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |

## Response sample

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

[Back](../rest.md)

