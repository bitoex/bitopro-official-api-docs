# User Trade Stream
This channel pushes messages with your trade data.

# Ws Request

**`GET` wss://stream.bitopro.com:443/ws/v1/pub/auth/user-trades**

**Authentication For Private Websocket Connection**

    | Security scheme | Header parameter    |
    | :-------------- | :------------------ |
    | API Key         | X-BITOPRO-APIKEY    |
    | Payload         | X-BITOPRO-PAYLOAD   |
    | Signature       | X-BITOPRO-SIGNATURE |
You can find how to create payload and signature from [authentication document](../../README.md#api-security-protocol).

# Ws Response

**Response:**

| 0    | Field             | Type    | Description                                                                         |
| :--- | :---------------- | :------ | :---------------------------------------------------------------------------------- |
| 0    | event             | string  | String literal for event name                                                       |
| 0    | eventID           | string  | event id for debug usage |
| 0    | timestamp         | integer | Unix Timestamp in milliseconds (seconds * 1000)                                     |
| 0    | datetime          | string  | ISO8601 datetime string with milliseconds                                           |
| 1    | side              | string  | ask (i.e sell) or bid (ie buy)                                                                         |
| 1    | price             | string  | match price                                                                                  |
| 1    | volume            | string  |   match base amount                                                                              |
| 1    | fee              | string  | match fee amount                                                         |
| 1    | feeCurrency  | string | match fee currency                                     |
| 1    | transactionTimestamp  | integer | Unix Timestamp of match time                                      |
| 1    | eventTimestamp  | integer | trade process time in server, unix timestamp in second |
| 1    | orderID    | string  |      match order ID                                                                               |
| 1    | orderType   | string  |      match order type, refer to [order type enum](../../model.md#order-type-enum) |
| 1    | matchID    | string  |       match id                                                                              |
| 1    | isMarket         | string  | if it true mean that the matched order is market type order                                                         |
| 1    | isMaker         | string  | if it true mean that the match is matched as maker side                                                         |
 

**Response Example:**

```javascript
{
    "event": "USER_TRADE",
    "eventID": "dadf4ac1-665a-4f39-a139-ab95da102374",
    "timestamp": 1694667358782,
    "datetime": "2023-09-14T12:55:58.782Z",
    "data": {
        "base": "usdt",
        "quote": "twd",
        "side": "ask",
        "price": "32.039",
        "volume": "1",
        "fee": "6407800",
        "feeCurrency": "twd",
        "transactionTimestamp": 1694667358,
        "eventTimestamp": 1694667358,
        "orderID": 390733918,
        "orderType": "LIMIT",
        "matchID": "bd07673a-94b1-419e-b5ee-d7b723261a5d",
        "isMarket": false,
        "isMaker": false
    }
}
```
[Back](../summary.md)