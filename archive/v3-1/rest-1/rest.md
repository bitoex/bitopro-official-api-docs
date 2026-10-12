# Rest

## [Changelog](changelog.md)

**The API service is hosted at** [https://api.bitopro.com/v3](https://api.bitopro.com/v3)**. Our rate limit policy:**

* Open API
  * `600` requests per minute per IP
* Auth API
  * `600` requests per minute per IP
  * `600` requests per minute per user account

#### For all endpoints require authentication, you should create the API key at [BitoPro](https://www.bitopro.com/api_list)

## [Authentication](authentication.md)

## HTTP Status Codes

* 2xx Success
  * `200` OK
* 4xx Client errors
  * `401` Unauthorized api key
  * `403` Forbidden
  * `409` Try to send the same request more than once
  * `422` Data parsing error
  * `429` Rate limits exceed
* 5xx Server errors
  * `502` Bad gateway
  * `503` Service unavailable

## Order status

* `-1`: Not Triggered
* `0`:  In progress
* `1`:  In progress \(Partial deal\)
* `2`:  Completed
* `3`:  Completed \(Partial deal\)
* `4`:  Cancelled
* `6`:  Post-only Cancelled

## Fee fields

* `fee` as fee paid
* `feeSymbol` as symbol for `fee`
* `bitoFee` as fee paid in **BITO**

## Endpoints

### `Open`

| Endpoint | URL | Example |
| :--- | :--- | :--- |
| [Get order book](open/order-book.md) | `GET` /order-book/{pair} | [https://api.bitopro.com/v3/order-book/bito\_twd](https://api.bitopro.com/v3/order-book/bito_twd) |
| [Get the list of currencies](open/currencies.md) | `GET` /provisioning/currencies | [https://api.bitopro.com/v3/provisioning/currencies](https://api.bitopro.com/v3/provisioning/currencies) |
| [Get the list of available pairs](open/trading-pairs.md) | `GET` /provisioning/trading-pairs | [https://api.bitopro.com/v3/provisioning/trading-pairs](https://api.bitopro.com/v3/provisioning/trading-pairs) |
| [Get tickers](open/tickers.md) | `GET` /tickers/{pair} | [https://api.bitopro.com/v3/tickers](https://api.bitopro.com/v3/tickers) |
| [Get the recent trades](open/trades.md) | `GET` /trades/{pair} | [https://api.bitopro.com/v3/trades/bito\_twd](https://api.bitopro.com/v3/trades/bito_twd) |
| [Get trading history](open/trading-history.md) | `GET` /trading-history/{pair} | [https://api.bitopro.com/v3/trading-history/btc\_twd?resolution=1w&from=1550822974&to=1566375034](https://api.bitopro.com/v3/trading-history/btc_twd?resolution=1w&from=1550822974&to=1566375034) |
| [Get the limitations and fees](open/lims-fees.md) | `GET` /provisioning/limitations-and-fees | [https://api.bitopro.com/v3/provisioning/limitations-and-fees](https://api.bitopro.com/v3/provisioning/limitations-and-fees) |

### `Auth`

| Endpoint | URL | Example |
| :--- | :--- | :--- |
| [Get the account balance](auth/account-balance.md) | `GET` /accounts/balance | [https://api.bitopro.com/v3/accounts/balance](https://api.bitopro.com/v3/accounts/balance) |
| [Get all orders](https://github.com/bitoex/bitopro-offical-api-docs/tree/ef80d6723fc2328826093e88f9bcbdd232907e1e/v3-1/rest-1/auth/all-order.md) | `GET` /orders/all/{pair} | [https://api.bitopro.com/v3/orders/all/bito\_twd](https://api.bitopro.com/v3/orders/all/bito_twd) |
| [Get order list](auth/order-list.md) \(Deprecated\) | `GET` /orders/{pair} | [https://api.bitopro.com/v3/orders/bito\_twd](https://api.bitopro.com/v3/orders/bito_twd) |
| [Create an order](auth/create-order.md) | `POST` /orders/{pair} | [https://api.bitopro.com/v3/orders/bito\_twd](https://api.bitopro.com/v3/orders/bito_twd) |
| [Create batch limit/market orders](auth/create-batch-limitmarket.md) | `POST` /orders/batch | [https://api.bitopro.com/v3/orders/batch](https://api.bitopro.com/v3/orders/batch) |
| [Cancel an order](auth/cancel-order.md) | `DELETE` /orders/{pair}/{id} | [https://api.bitopro.com/v3/orders/bito\_twd/123456789](https://api.bitopro.com/v3/orders/bito_twd/123456789) |
| [Cancel all orders](auth/cancel-all.md) | `DELETE` /orders/all or /orders/{pair} | [https://api.bitopro.com/v3/orders/all](https://api.bitopro.com/v3/orders/all) or [https://api.bitopro.com/v3/orders/btc\_usdt](https://api.bitopro.com/v3/orders/btc_usdt) |
| [Cancel multiple orders](auth/cancel-batch.md) | `PUT` /orders | [https://api.bitopro.com/v3/orders](https://api.bitopro.com/v3/orders) |
| [Get an order](auth/get-order.md) | `GET` /orders/{pair}/{orderId} | [https://api.bitopro.com/v3/orders/bito\_twd/123456789](https://api.bitopro.com/v3/orders/bito_twd/123456789) |
| [Get Withdraw Information](auth/get-withdraw.md) | `GET` /wallet/withdraw/{currency}/{serial} | [https://api.bitopro.com/v3/wallet/withdraw/twd/123456](https://api.bitopro.com/v3/wallet/withdraw/123456) |
| [Withdraw](auth/withdraw.md) | `POST` /wallet/withdraw/{currency} | [https://api.bitopro.com/v3/wallet/withdraw/twd](https://api.bitopro.com/v3/wallet/withdraw/twd) |

