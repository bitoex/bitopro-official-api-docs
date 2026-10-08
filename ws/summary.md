# General WebSocket Information
* The base endpoint is: **wss://stream.bitopro.com:443/ws**.
* Streams can be access either in `single pair` or `combinded pairs`.
* All pairs for streams are **uppercase** and with an **underscore** between the base and quote, except for the active order stream.
* The websocket server will send a `ping frame` every 20 seconds. If the websocket server doesn't receive a `pong frame` back from the client within a 5-second period, the connection will be disconnected.
* We'll always push the `latest` data when you successfully get the websocket connection.
* [Ws Stream List](../README.md#websocket-stream-list)
* Private ws stream authentication protocol can be found by [API Security Protocol](../README.md#api-security-protocol).

[Back](../README.md)