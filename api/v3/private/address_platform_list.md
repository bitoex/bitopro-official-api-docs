# Address Platform List

The allowed values of `addressPlatform` for [Create Withdraw Invoice](create_an_withdraw_invoice.md). The platforms are grouped by category (exchange / wallet), then by region (Taiwan / non-Taiwan) for exchanges or by type (hot / cold) for wallets. The number in the table is the value of `addressPlatform`, and `addressPlatformType` must match the category that the platform belongs to.

## Exchanges (`addressPlatformType=0`) - Taiwan

| addressPlatform | Name |
| :--- | :--- |
| 1 | Chainss |
| 2 | HOYA BIT |
| 3 | KryptoGO |
| 4 | MAX |
| 5 | TWEX |
| 6 | XREX |
| 7 | ZONE Wallet |
| 37 | BitoPro (the recipient information can be omitted entirely when this option is selected) |

## Exchanges (`addressPlatformType=0`) - Non-Taiwan

| addressPlatform | Name |
| :--- | :--- |
| 8 | Bitfinex |
| 9 | Bitget |
| 10 | Bybit |
| 11 | Binance |
| 12 | BingX |
| 13 | Coinbase Exchange |
| 14 | Crypto.com |
| 15 | Gate.io |
| 16 | HTX |
| 17 | KuCoin |
| 18 | Kraken |
| 19 | MEXC |
| 20 | OKX |
| 21 | Pionex |
| 22 | Upbit |
| 38 | Bitunix |

## Wallets (`addressPlatformType=1`) - Hot Wallets

| addressPlatform | Name |
| :--- | :--- |
| 23 | Binance Web3 Wallet |
| 24 | Bitget Wallet |
| 25 | Coinbase Wallet |
| 26 | Exodus |
| 27 | MetaMask |
| 28 | OKX Web3 Wallet |
| 29 | Phantom |
| 30 | Rabby Wallet |
| 31 | Trust Wallet |
| 32 | Zengo |

## Wallets (`addressPlatformType=1`) - Cold Wallets

| addressPlatform | Name |
| :--- | :--- |
| 33 | BitoPro (cold wallet, the recipient information is still required, the omission rule for BitoPro exchange does not apply) |
| 34 | Ledger |
| 35 | Tangem |
| 36 | Trezor |

## Not in the List

| addressPlatform | addressPlatformType | Name | Remark |
| :--- | :--- | :--- | :--- |
| 0 | 0 (exchange) | Other (exchange) | `addressPlatformOther` is required, and the recipient information is required |
| 0 | 1 (wallet) | Other (wallet) | `addressPlatformOther` is required, and please provide the recipient information |

> The platform list may be updated at any time, please refer to the latest BitoPro announcement.

[Back](create_an_withdraw_invoice.md)