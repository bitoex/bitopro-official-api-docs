# ~Get order book~

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**

### Get the full order book of the specific pair

## `GET` /order-book/{pair}

## Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |
|  |  | limit | integer | No | The limit for the response. | 5 | 1, 5, 10, 20 | 1 |
|  |  | scale | integer | No | The scale for the response. Valid scale values are different by pair. For more detail, please refer the field `orderBookQuoteScaleLevel` of [Get the list of available pairs](https://api.bitopro.com/v2/provisioning/trading-pairs) | 0 | [Get the list of available pairs](https://api.bitopro.com/v2/provisioning/trading-pairs) | 1 |

## Response sample

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

[Back](../rest.md)

