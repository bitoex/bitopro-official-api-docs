# List Deposit Invoices Data

# Api Request
**`GET` /wallet/depositHistory/{currency}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path     | Query          | Type   | Required | Description                                                                                                                              | Default                        | Range          | Example                |
| :------------------ | :------- | :------------- | :----- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------- | :------------- | :--------------------- |
| X-BITOPRO-APIKEY    |          |                | string | Yes      | API Key                                                                                                           |                                |                |                        |
| X-BITOPRO-PAYLOAD   |          |                | string | Yes      | Payload                                                                                                           |                                |                |                        |
| X-BITOPRO-SIGNATURE |          |                | string | Yes      | Signature                                                                                                       |                                |                |                        |
|                     | currency |                | string | Yes      | The currency of the withdraw to get. Please follow the [link](https://www.bitopro.com/ns/fees) to check the currency list.                  |                                |                | twd                    |
|                     |          | startTimestamp | int64  | No       | The start timestamp in unix timestap (miliesceond).                                                                                      | 90 days from the end timestamp |                | 1592203563000          |
|                     |          | endTimestamp   | int64  | No       | The end timestamp in unix timestap (miliesceond).                                                                                        | present timestamp              |                | 1592203563000          |
|                     |          | limit          | int64  | No       | The limit for the response.                                                                                                              | 20                             | min:1, max:100 | 30                     |
|                     |          | id             | string | No       | The id of the first data in the response. It can serve as an offset when it's sent as an id of the last data from the previous response. |                                |                | 3255779687             |
|                     |          | statuses       | string | No       | The status of the deposit. It is multiple values that are concatenated by a comma.                                                       |                                |                | CANCELLED,WAIT_PROCESS |
|                     |          | txID           | string | No       | The transaction ID to filter deposits. Not supported for fiat currencies (TWD, USD). Note: txID is not unique and may return multiple records. |                                |                | 414b4d22c07d815834213d83f368... |

- The start timestamp must be less than the end timestamp and the time between the start and end timestamp must be less and equal to 90 days.
- The deposit cryptocurrency status could be `PROCESSING`,`COMPLETE`,`EXPIRED`,`INVALID`,`WAIT_PROCESS`,`CANCELLED`.
- The deposit twd status could be `PROCESSING`,`COMPLETE`,`INVALID`,`WAIT_PROCESS`,`CANCELLED`, `FAILED`.
- **Note**: The `txID` parameter is only supported for cryptocurrency deposits and is not available for fiat currencies (TWD, USD). The txID is not unique and may return multiple records.

# Api Response

**Response Example:**

```javascript
{
    "data": [
        {
            "serial": "20210126BW05262128",
            "timestamp": "1611660419000",
            "address": "2N7sfszCocGkDst3mULPP7JmdctgDWeCpGf",
            "amount": "200000000",
            "fee": "0",
            "total": "200000000",
            "status": "WAIT_PROCESS",
            "txid": "00d618f6ecb5697c674a47cd1a40edf399c99eaeb045f0ff7ab3ee2be6f5",
            "message": "test", //may not be included 
            "protocol": "MAIN",
            "id": "3255779687"
        },
        {
            "serial": "20210126BW21101833",
            "timestamp": "1611660400000",
            "address": "2N7sfszCocGkDst3mULPP7JmdctgDWeCpGf",
            "amount": "300000000",
            "fee": "0",
            "total": "300000000",
            "status": "WAIT_PROCESS",
            "txid": "00e1d6aec3cb40080bace4ec70a3e4ad95af1ca7ca68ef7be02a3f59fcf9",
            "protocol": "MAIN",
            "id": "8378921292"
        },
        ...
    ]
}
```
[Back](../summary.md)