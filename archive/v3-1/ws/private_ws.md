# WebSocket Private Streams for BitoPro

* [WebSocket Private Streams for BitoPro](private_ws.md#websocket-private-streams-for-bitopro)
  * [General Private WebSocket Information](private_ws.md#general-private-websocket-information)
  * [Authentication For Private Websocket Connection](private_ws.md#authentication-for-private-websocket-connection)
  * [Detailed Private Stream Information](private_ws.md#detailed-stream-information)
    * [Orders](private_ws.md#active-orders)
    * [Account Balance](private_ws.md#account-balance)

## General Private WebSocket Information

* The base endpoint is: **wss://stream.bitopro.com:9443/ws**.
* Streams can be access either in `single pair` or `combinded pairs`.
* All pairs for streams are **uppercase** and with **underscore** between base and quote except the active order stream.
* The websocket server will send a `ping frame` every 20 seconds. If the websocket server doesn't receive a `pong frame` back from the client within a 5 seconds period, the connection will be disconnected.
* We'll always push the `latest` data when you successfully get the websocket connection.

## Authentication For Private Websocket Connection

| Security scheme | Header parameter |
| :--- | :--- |
| API Key | X-BITOPRO-APIKEY |
| Payload | X-BITOPRO-PAYLOAD |
| Signature | X-BITOPRO-SIGNATURE |

You can find how to create payload and signature from [authentication document.](../rest-1/authentication.md)

## Detailed Stream Information

### Active Orders

This channel push message with active orders.

Note: You will receive active orders from all trading pairs when you build a websocket connection at first. After that, websocket server only push the updated active orders from single trading pair.

* Response

| 0 | Field | Type | Description |
| :--- | :--- | :--- | :--- |
| 0 | event | string | String literal for event name |
| 0 | timestamp | integer | Unix Timestamp in milliseconds \(seconds \* 1000\) |
| 0 | datetime | string | ISO8601 datetime string with milliseconds |
| 1 | id | string | |
| 1 | action | string | BUY or SELL |
| 1 | price | string | |
| 1 | avgExecutionPrice | string | |
| 1 | type | string | LIMIT, Market or STOP_LIMIT  |
| 1 | createdTimestamp | integer | Unix Timestamp in milliseconds \(seconds \* 1000\) |
| 1 | updatedTimestamp | integer | Unix Timestamp in milliseconds \(seconds \* 1000\) |
| 1 | status | integer | [see order status](../rest-1/rest.md#order-status) |
| 1 | originalAmount | string | |
| 1 | remainingAmount | string | |
| 1 | executedAmount | string | |
| 1 | stopPrice | string | |
| 1 | condition | string | stop limit trigger condition |
| 1 | pair | string | lowercase string underscore-delimited literal of a pair of currencies |
| 1 | fee | string | |
| 1 | feeSymbol | string | |
| 1 | bitoFee | string | bito currency fee |
| 1 | total | string | total trading quote currency amount |
| 1 | seq | string | order sequence number |
| 1 | timeInForce | string | Time in force condition for orders. If type is `MARKET`, this will always be `GTC`. | `GTC` | `GTC`, `POST_ONLY` | POST_ONLY |
 

* URL

`GET` **wss://stream.bitopro.com:9443/ws/v1/pub/auth/orders**

Sample

```javascript
GET wss://stream.bitopro.com:9443/ws/v1/pub/auth/orders

{
    "event": "ACTIVE_ORDERS",
    "timestamp": 1639552073346,
    "datetime": "2021-12-15T07:07:53.346Z",
    "data": {
        "sol_usdt": [
            {
                "id": "8917255503",
                "pair": "sol_usdt",
                "price": "107",
                "avgExecutionPrice": "0",
                "action": "SELL",
                "type": "LIMIT",
                "timestamp": 1639386803663,
                "updatedTimestamp": 1639386803663,
                "createdTimestamp": 1639386803663,
                "status": 0,
                "originalAmount": "0.02",
                "remainingAmount": "0.02",
                "executedAmount": "0",
                "fee": "0",
                "feeSymbol": "usdt",
                "bitoFee": "0",
                "total": "0",
                "seq": "SOLUSDT3273528249",
                "timeInForce": "GTC"
            }
        ],
        "usdc_twd": [
            {
                "id": "3452766477",
                "pair": "usdc_twd",
                "price": "10",
                "avgExecutionPrice": "0",
                "action": "BUY",
                "type": "LIMIT",
                "timestamp": 1638258713957,
                "updatedTimestamp": 1639386803663,
                "createdTimestamp": 1639386803663,
                "status": 0,
                "originalAmount": "0.01",
                "remainingAmount": "0.01",
                "executedAmount": "0",
                "fee": "0",
                "feeSymbol": "usdc",
                "bitoFee": "0",
                "total": "0",
                "seq": "USDCTWD2310459465"
                "timeInForce": "GTC"
            }
        ]
    }
}
```

### Account Balance

This channel push message with account balance.

* Response

| 0 | Field | Type | Description |
| :--- | :--- | :--- | :--- |
| 0 | event | string | String literal for event name |
| 0 | timestamp | integer | Unix Timestamp in milliseconds \(seconds \* 1000\) |
| 0 | datetime | string | ISO8601 datetime string with milliseconds |
| 1 | currency | string | uppercase string |
| 1 | amount | string | Total amount |
| 1 | available | string | |
| 1 | stake | string | |
| 1 | tradable | bool | |

* URL

`GET` **wss://stream.bitopro.com:9443/ws/v1/pub/auth/account-balance**

Sample

```javascript
GET wss://stream.bitopro.com:9443/ws/v1/pub/auth/account-balance

{
    "event": "ACCOUNT_BALANCE",
    "timestamp": 1639553303365,
    "datetime": "2021-12-15T07:28:23.365Z",
    "data": {
        "ADA": {
            "currency": "ADA",
            "amount": "999999999999.99999999",
            "available": "999999999999.99999999",
            "stake": "0",
            "tradable": true
        },
        "ALLN": {
            "currency": "ALLN",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": false
        },
        "BCD": {
            "currency": "BCD",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": true
        },
        "BCH": {
            "currency": "BCH",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": true
        },
        "BCHSV": {
            "currency": "BCHSV",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": true
        },
        "BITO": {
            "currency": "BITO",
            "amount": "9999799",
            "available": "9999799",
            "stake": "0",
            "tradable": true
        },
        "BNB": {
            "currency": "BNB",
            "amount": "8500",
            "available": "8500",
            "stake": "0",
            "tradable": true
        },
        "BTC": {
            "currency": "BTC",
            "amount": "999999999999.99999999",
            "available": "999999999999.99999999",
            "stake": "0",
            "tradable": true
        },
        "DOGE": {
            "currency": "DOGE",
            "amount": "999999999999.99999999",
            "available": "999999999999.99999999",
            "stake": "0",
            "tradable": true
        },
        "EOS": {
            "currency": "EOS",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": true
        },
        "MITH": {
            "currency": "MITH",
            "amount": "0",
            "available": "0",
            "stake": "0",
            "tradable": false
        },
        ...
    }
}
```