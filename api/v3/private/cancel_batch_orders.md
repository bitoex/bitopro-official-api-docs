# Cancel Batch Orders

Cancel multiple orders by given group of order ids.

# Api Request:
**`PUT` /orders**

Send a json format request to cancel multiple orders at a time.

**Rate limit:**
Allow `2` requests per second per IP.

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header              | Path | Query | Type   | Required | Description                       | Default | Range | Example |
| :------------------ | :--- | :---- | :----- | :------- | :-------------------------------- | :------ | :---- | :------ |
| X-BITOPRO-APIKEY    |      |       | string | Yes      | API Key     |         |       |         |
| X-BITOPRO-PAYLOAD   |      |       | string | Yes      | Payload    |         |       |         |
| X-BITOPRO-SIGNATURE |      |       | string | Yes      | Signature|         |       |         |

**Request Example:**

```javascript
{
  "BTC_USDT": [
    "12234566",  // order id
    "12234567"
  ],
  "ETH_USDT": [
    "44566712",
    "24552212"
  ]
}
```

# Api Response:
**Response Example:**

```javascript
{
  "data": {
    "BTC_USDT": [
      "12234566", // cancelled orders
      "12234567"
    ],
    "ETH_USDT": [
      "44566712",
      "24552212"
    ]
  }
}
```
[Back](../summary.md)