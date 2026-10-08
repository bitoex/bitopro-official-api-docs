# Get trade list

### `GET` /orders/trades/{pair}

### Parameters

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY |  |  | string | Yes | [API Key](../authentication.md#api-key) |  |  |  |
| X-BITOPRO-PAYLOAD |  |  | string | Yes | [Payload](../authentication.md#payload) |  |  |  |
| X-BITOPRO-SIGNATURE |  |  | string | Yes | [Signature](../authentication.md#signature) |  |  |  |
|  | pair |  | string | Yes | The trading pair in format ${BASE}\_${QUOTE}, Please follow the [link](https://www.bitopro.com/ns/fees) to check the pair list. |  |  | bito\_eth |
|  |  | startTimestamp | integer | No | The start timestamp in unix timestap (miliesceond). | 90 days from the end timestamp  |  | 1592203563000 |
|  |  | endTimestamp | integer | No | The end timestamp in unix timestap (miliesceond). | present timestamp  | | 1592203563000 |
|  |  | orderId | string | No | The id of the order.	 | | | 6995795641 |
|  |  | tradeId | string | No | The id of the first trade in the response. It can serve as an offset when it's sent as an id of the last data from the previous response. | | | 8473494907 |
|  |  | limit | integer | No | The limit for the response. | 100 | min:0, max:1000 | 100 |

### Response sample

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
        {
            "tradeId": "7986220603",
            "orderId": "7731705024",
            "price": "530",
            "action": "BUY",
            "baseAmount": "600",
            "quoteAmount": "318000",
            "fee": "0.18",
            "feeSymbol": "ETH",
            "isTaker": false,
            "timestamp": 1628054695032,
            "createdTimestamp": 1628054695032
        },
        {
            "tradeId": "7986220603",
            "orderId": "2608563419",
            "price": "530",
            "action": "SELL",
            "baseAmount": "600",
            "quoteAmount": "318000",
            "fee": "349.8",
            "feeSymbol": "ETH",
            "isTaker": true,
            "timestamp": 1628054695032,
            "createdTimestamp": 1628054695032
        },
        {
            "tradeId": "2863078998",
            "orderId": "2362280208",
            "price": "630",
            "action": "BUY",
            "baseAmount": "600",
            "quoteAmount": "378000",
            "fee": "0.66",
            "feeSymbol": "ETH",
            "isTaker": true,
            "timestamp": 1628054709521,
            "createdTimestamp": 1628054709521
        },
        {
            "tradeId": "2863078998",
            "orderId": "7485421813",
            "price": "630",
            "action": "SELL",
            "baseAmount": "600",
            "quoteAmount": "378000",
            "fee": "113.4",
            "feeSymbol": "ETH",
            "isTaker": false,
            "timestamp": 1628054709521,
            "createdTimestamp": 1628054709521
        },
        {
            "tradeId": "2616795787",
            "orderId": "1869713786",
            "price": "400",
            "action": "SELL",
            "baseAmount": "600",
            "quoteAmount": "240000",
            "fee": "264",
            "feeSymbol": "ETH",
            "isTaker": true,
            "timestamp": 1628060675491,
            "createdTimestamp": 1628060675491
        },
        {
            "tradeId": "7739937392",
            "orderId": "2115996997",
            "price": "700",
            "action": "BUY",
            "baseAmount": "600",
            "quoteAmount": "420000",
            "fee": "0.18",
            "feeSymbol": "ETH",
            "isTaker": false,
            "timestamp": 1628060675491,
            "createdTimestamp": 1628060675491
        },
        {
            "tradeId": "7739937392",
            "orderId": "1869713786",
            "price": "700",
            "action": "SELL",
            "baseAmount": "600",
            "quoteAmount": "420000",
            "fee": "462",
            "feeSymbol": "ETH",
            "isTaker": true,
            "timestamp": 1628060675491,
            "createdTimestamp": 1628060675491
        },
        {
            "tradeId": "7493654181",
            "orderId": "6992855391",
            "price": "300",
            "action": "BUY",
            "baseAmount": "700",
            "quoteAmount": "210000",
            "fee": "0.21",
            "feeSymbol": "ETH",
            "isTaker": false,
            "timestamp": 1628060675491,
            "createdTimestamp": 1628060675491
        }
    ]
}
```

[Back](../rest.md)

