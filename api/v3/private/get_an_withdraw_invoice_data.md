# Get A Withdraw Invoice
**`GET` /wallet/withdraw/{currency}/{serial}**

# Api Request
**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path     | Query | Type   | Required | Description                                                                                                             | Default | Range | Example            |
| :------------------ | :------- | :---- | :----- | :------- | :---------------------------------------------------------------------------------------------------------------------- | :------ | :---- | :----------------- |
| X-BITOPRO-APIKEY    |          |       | string | Yes      | API Key                                                                                           |         |       |                    |
| X-BITOPRO-PAYLOAD   |          |       | string | Yes      | Payload                                                                                           |         |       |                    |
| X-BITOPRO-SIGNATURE |          |       | string | Yes      | Signature                                                                                       |         |       |                    |
|                     | currency |       | string | Yes      | The currency of the withdraw to get. Please follow the [link](https://www.bitopro.com/ns/fees) to check the currency list. |         |       | twd                |
|                     | serial   |       | string | Yes      | The serial of the withdraw.                                                                                             |         |       | 20200417TW51258295 |

# Api Response
**Response:**

```javascript
{
  "data": 
    {
      "serial": "20200417TW51258295",
      "datetime": "1601951443", //deprecated
      "protocol": "MAIN",
      "address": "64382xx3234",
      "amount": "12353", //amount actually sent
      "fee": "15", //fee deducted from initial amount
      "total": "12368",
      "status": "WAIT_PROCESS",
      "message": "test", //may not be included 
      "id": "3994629320",
      "timestamp": "1601951443123"
    }
}
```

**`GET` /wallet/withdraw/{currency}/id/{id}**

**Parameters:**

| Header              | Path     | Query | Type   | Required | Description                                                                                                             | Default | Range | Example    |
| :------------------ | :------- | :---- | :----- | :------- | :---------------------------------------------------------------------------------------------------------------------- | :------ | :---- | :--------- |
| X-BITOPRO-APIKEY    |          |       | string | Yes      | API Key                                                                                           |         |       |            |
| X-BITOPRO-PAYLOAD   |          |       | string | Yes      | Payload                                                                                          |         |       |            |
| X-BITOPRO-SIGNATURE |          |       | string | Yes      | Signature                                                                                      |         |       |            |
|                     | currency |       | string | Yes      | The currency of the withdraw to get. Please follow the [link](https://www.bitopro.com/ns/fees) to check the currency list. |         |       | twd        |
|                     | id       |       | string | Yes      | The id of the withdraw.                                                                                                 |         |       | 3994629320 |

**Response:**

```json
{
  "data": 
    {
      "serial": "20200417TW51258295",
      "datetime": "1601951443", //deprecated
      "protocol": "MAIN",
      "address": "64382xx3234",
      "amount": "12353", //amount actually sent
      "fee": "15", //fee deducted from initial amount
      "total": "12368",
      "status": "WAIT_PROCESS",
      "message": "test", //may not be included 
      "id": "3994629320",
      "timestamp": "1601951443123"
    }
}
```
[Back](../summary.md)