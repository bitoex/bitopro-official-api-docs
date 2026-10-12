# List Trades

History is available only for the past 90 days.

# Api Request
**`GET` /orders/trades/{pair}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query          | Type   | Required | Description                                                                                                                               | Default                        | Range           | Example       |
| :------------------ | :--- | :------------- | :----- | :------- | :---------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------- | :-------------- | :------------ |
| X-BITOPRO-APIKEY    |      |                | string | Yes      | API Key                                                                                                             |                                |                 |               |
| X-BITOPRO-PAYLOAD   |      |                | string | Yes      | Payload                                                                                                             |                                |                 |               |
| X-BITOPRO-SIGNATURE |      |                | string | Yes      | Signature                                                                                                         |                                |                 |               |
|                     | pair |                | string | Yes      | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list.              |                                |                 | bito\_eth     |
|                     |      | startTimestamp | int64  | No       | The start timestamp in unix timestap (miliesceond).                                                                                       | 90 days from the end timestamp |                 | 1592203563000 |
|                     |      | endTimestamp   | int64  | No       | The end timestamp in unix timestap (miliesceond).                                                                                         | present timestamp              |                 | 1592203563000 |
|                     |      | orderId        | string | No       | The id of the order.                                                                                                                      |                                |                 | 6995795641    |
|                     |      | tradeId        | string | No       | The id of the first trade in the response. It can serve as an offset when it's sent as an id of the last data from the previous response. If this parameter is included, the response will comprise data with IDs less than or equal to the tradeId provided. |                                |                 | 8473494907    |
|                     |      | limit          | int64  | No       | The limit for the response.                                                                                                               | 100                            | min:0, max:1000 | 100           |


# Api Response
**Response:**

```javascript
{
    "data": [
        {
            "tradeId": "3109362209",
            "orderId": "7977988235",
            "price": "530",
            "action": "SELL",
            "baseAmount": "600",
            "quoteAmount": "318000",
            "fee": "95.4",
            "feeSymbol": "ETH",
            "isTaker": false,
            "timestamp": 1628054591943, // deprecated, using createdTimestamp
            "createdTimestamp": 1628054591943
        },
        {
            "tradeId": "3109362209",
            "orderId": "2854846630",
            "price": "530",
            "action": "BUY",
            "baseAmount": "600",
            "quoteAmount": "318000",
            "fee": "0.66",
            "feeSymbol": "ETH",
            "isTaker": true,
            "timestamp": 1628054591943, 
            "createdTimestamp": 1628054591943
        },
        ...
    ]
}
```
[Back](../summary.md)
