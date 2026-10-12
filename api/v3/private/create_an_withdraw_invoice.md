# Create Withdraw Invoice

Submit withdraw request. Before using this api, you have to setup your withdraw address from this [webpage](https://www.bitopro.com/address).

> For cryptocurrency withdrawal, recipient information must be provided in accordance with the Travel Rule. Please refer to [Travel Rule Recipient Information](#travel-rule-recipient-information) for details.

# Api Request

**Rate limit:**

Allow `60` requests per minute per IP.

**`POST` /wallet/withdraw/{currency}**

**Parameters:**

You can find how to create payload and signature from [authentication document](../../../README.md#api-security-protocol).

| Header | Path | Query | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| X-BITOPRO-APIKEY | | | string | Yes | API Key | | | |
| X-BITOPRO-PAYLOAD | | | string | Yes | Payload | | | |
| X-BITOPRO-SIGNATURE | | | string | Yes | Signature | | | |
| | currency | | string | Yes | The currency to withdraw. Please follow the [link](https://www.bitopro.com/ns/fees) to check the currency list. Please provide only currency name without protocol, you can define protocol in request body. | | | twd, usdt, btc or eth |

**Request body:**

| Field | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| protocol | string | No | The protocol to send, case-insensitive. USDT have `ERC20`, `OMNI` and `TRX` to choose. It is ignored for TWD withdrawal. | `MAIN` | `MAIN`, `ERC20`, `OMNI`, `BNB`, `TRX`, `BSC`, `POLYGON`, `KAIA`. Other values will be rejected (`invalid_protocol`). | `ERC20` |
| address | string | No | The address to send fund. Required for non-TWD withdraw. It is not used for TWD withdrawal, the receiving bank account is determined by `bankSerial` and `bankAccountSerial`. | | | 1BitcoinAddressXXXXXXXXXXXXXXXX |
| amount | string | Yes | The amount of fund to send. | | > 0 | 0.01 |
| message | string | No | The message or note to be attached with withdraw. For some currencies, it is required, for example, EOS and BNB. | | | |
| bankAccountSerial | string | No | Bank account number for TWD withdrawal. It only takes effect when provided together with `bankSerial`. | Default to the verified bank account when it is not provided, or only one of `bankAccountSerial` and `bankSerial` is provided | Must be the verified bank account, otherwise the request will be rejected | 1020000286850710 |
| bankSerial | string | No | Bank code for TWD withdrawal. It only takes effect when provided together with `bankAccountSerial`. | Same as `bankAccountSerial` | Numeric string | 805 |

**Request body (Travel Rule fields):**

The following fields are only for cryptocurrency withdrawal. **TWD withdrawal to a bank account does not require any Travel Rule fields**, and providing them does not affect the withdrawal.

| Field | Type | Required | Description | Default | Range | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| recipientRelation | int32 | Yes | The relationship between you and the recipient. It is also required when the destination is BitoPro exchange (`addressPlatform=37`), unless the withdrawal is identified as an internal transfer (see [Internal Transfer](#internal-transfer-vs-addressplatform37)). | | `0`: Self, `1`: Others. Other values will be rejected. | 1 |
| recipientType | int32 | No | The type of the recipient, **only required** when recipient information is required (see [Recipient Information Rules](#recipient-information-rules)). **It is also required when the recipient is yourself (`recipientRelation=0`)**, the system will not fill in your account information automatically. | | `0`: Individual, `1`: Company / Institution. Other values will be rejected. | 0 |
| recipientFirstName | string | No | The first name of the recipient, **only required** when `recipientType` is `0` and recipient information is required. | | Up to 150 characters | Chun |
| recipientLastName | string | No | The last name of the recipient, **only required** when `recipientType` is `0` and recipient information is required. | | Up to 150 characters | Chen |
| recipientCompanyName | string | No | The company name of the recipient, **only required** when `recipientType` is `1` and recipient information is required. | | Up to 150 characters | ABC Trading Co., Ltd. |
| recipientCompanyTaxId | string | No | The tax ID / registration number / LEI of the recipient company, **only required** when `recipientType` is `1`, the amount reaches the [threshold](#amount-threshold) and the destination is not BitoPro exchange. Optional otherwise. | | | 12345678 |
| recipientCountry | string | No | The country of the recipient, **only required** when the amount reaches the [threshold](#amount-threshold) and the destination is not BitoPro exchange. It is also required when `recipientCity` is provided. | | ISO 3166-1 alpha-2 country code (2 letters), case-insensitive. Invalid codes will be rejected. | TW |
| recipientCity | string | No | The city of the recipient, **only required** when the amount reaches the [threshold](#amount-threshold) and the destination is not BitoPro exchange. | | For `TW`, it must be a code in the [Recipient City List (TW)](recipient_city_tw_list.md) (case-insensitive). For other countries, fill in the city name. | taipei or New York |
| addressPlatform | int32 | Yes | The platform that the receiving address belongs to. | | See [Address Platform List](address_platform_list.md). `0`: Other, only when the platform is not in the list | 3 |
| addressPlatformOther | string | No | The custom platform name when the platform is not in the list, **only required** when `addressPlatform` is `0`. | | Must not be blank or the same as the name of a platform in the list. Must not be provided when `addressPlatform` is not `0`. | |
| addressPlatformType | int32 | Yes | The category of the platform. **It must match the category of `addressPlatform`**, otherwise the request will be rejected. | | `0`: Exchange, `1`: Wallet | 0 |

## Travel Rule Recipient Information

### Quick Rules

| Rule | Description |
| :--- | :--- |
| Required for every withdrawal | `recipientRelation`, `addressPlatform` and `addressPlatformType` are required for every cryptocurrency withdrawal (`addressPlatformOther` is also required when `addressPlatform=0`). The other recipient fields depend on the destination and the amount, see the rules below. |
| Withdraw to BitoPro exchange | When `addressPlatformType=0` and `addressPlatform=37` (BitoPro exchange), the recipient information can be omitted entirely, but `recipientRelation`, `addressPlatform` and `addressPlatformType` are still required. BitoPro (`33`) in the cold wallet list is a different option: it is treated as an overseas platform, so the recipient information is required, the same as other wallets and non-Taiwan exchanges. |
| Withdraw to other platforms | Please provide complete recipient information. **It is also required when the recipient is yourself (`recipientRelation=0`).** |
| Optional field | `recipientCompanyTaxId` (tax ID / registration number) is optional except in specific cases, see [Amount Threshold](#amount-threshold). |

### Internal Transfer vs. `addressPlatform=37`

Whether a withdrawal is a BitoPro internal transfer is determined by the system from the receiving address, not by `addressPlatform`:

| Case | Travel Rule fields |
| :--- | :--- |
| The receiving address is a BitoPro account address (internal transfer, identified by the system) | None of the Travel Rule fields are validated, they can be omitted entirely. |
| The receiving address is not identified as internal, and you select `addressPlatform=37` (BitoPro exchange) | `recipientRelation`, `addressPlatform` and `addressPlatformType` are still required. Only the recipient information can be omitted. |
| TWD withdrawal | The Travel Rule fields do not apply. |

### Recipient Information Rules

| Destination | Recipient information | Description |
| :--- | :--- | :--- |
| BitoPro exchange (`37`) | Optional | It can always be omitted regardless of other conditions. |
| Other exchanges or wallets (including BitoPro cold wallet `33`, which is treated as an overseas platform) | Required | Please always provide complete recipient information to ensure the withdrawal is processed smoothly. |

> **Note**: The withdrawal request will be rejected if the recipient information is not provided as required. All provided fields must follow the format and the allowed values.

When recipient information is required, at least `recipientType` must be provided, plus `recipientFirstName` and `recipientLastName` for an individual, or `recipientCompanyName` for a company.

### Amount Threshold

When the amount of a single withdrawal (after deducting the fee) is equivalent to TWD 30,000 or more, and the destination is not BitoPro exchange, the following fields are additionally required:

| Recipient type | Additional required fields |
| :--- | :--- |
| Individual | `recipientCountry`, `recipientCity` |
| Company | `recipientCountry`, `recipientCity`, `recipientCompanyTaxId` |

## Validation Errors

When a field is missing or invalid, the withdrawal request will be rejected and no withdraw invoice will be created. The response is in the format of `{"error": "<error message>"}`, the table below lists the beginning of the English error messages:

| Case | Error message |
| :--- | :--- |
| `recipientRelation` is missing, or its value is not `0` or `1` | `Recipient relation (recipientRelation) is required ...` |
| `addressPlatform` or `addressPlatformType` is missing, `addressPlatformType` is not `0` or `1`, `addressPlatform=0` without `addressPlatformOther`, or `addressPlatformOther` is provided when `addressPlatform` is not `0` | `Invalid address platform: ...` |
| `addressPlatform` is not in the list (e.g. `9999`), or it does not match the category of `addressPlatformType` (e.g. `27` (MetaMask, wallet) with `addressPlatformType=0` (exchange)) | `Invalid address platform: ...` |
| `addressPlatformOther` is the same as the name of a platform in the list (please select that platform from the list instead) | `The custom platform name duplicates an existing option in the list. ...` |
| `recipientType` is not `0` or `1`, or it is missing when recipient information is required | `Recipient type (recipientType) is required ...` |
| The name (individual) or the company name (company) is missing when recipient information is required | `Invalid recipient name: ...` |
| `recipientCompanyTaxId` is missing for a company when the amount reaches the threshold and the destination is not BitoPro exchange | `Invalid recipient company tax ID: ...` |
| `recipientCountry` is not a valid ISO 3166-1 alpha-2 country code (misspelled or not 2 letters), `recipientCity` is provided without `recipientCountry`, or `recipientCountry` is missing when the amount reaches the threshold | `Invalid recipient country: ...` (lowercase such as `tw` is accepted) |
| `recipientCity` is not in the city code list for `TW` (e.g. `taipei123`), or it is missing when the amount reaches the threshold | `Invalid recipient city: ...` (case-insensitive) |
| The system is temporarily unable to complete the validation | `Unknown error.`, please try again later |
| A field has the wrong type (e.g. `"recipientRelation": "1"` as a string, or `"amount": 0.01` as a number) | HTTP `422`, `Invalid body` |

> If there are multiple errors, only one of them will be returned at a time. Please fix them one by one according to the error message and send the request again.

> Please fill in `recipientCountry`, `recipientCity` and `addressPlatform` according to the [allowed values](#allowed-values), invalid values will be rejected.

## Allowed Values

| Field | List |
| :--- | :--- |
| `addressPlatform` / `addressPlatformType` | [Address Platform List](address_platform_list.md) |
| `recipientCity` (when `recipientCountry=TW`) | [Recipient City List (TW)](recipient_city_tw_list.md) |

## Request Example

The following 5 examples show how to fill in the Travel Rule fields in common scenarios. The amounts are for illustration only, whether a withdrawal reaches the threshold depends on its TWD equivalent after deducting the fee, at the exchange rate at that time.

**Scenario (a): The recipient is yourself, withdrawing to XREX (a Taiwan exchange), below the threshold (less than TWD 30,000 equivalent)**

```javascript
// POST /wallet/withdraw/btc
{
  "protocol": "MAIN",
  "address": "1BitcoinAddressXXXXXXXXXXXXXXXX",
  "amount": "0.001",
  "recipientRelation": 0,
  "recipientType": 0,
  "recipientFirstName": "Chun",
  "recipientLastName": "Chen",
  "addressPlatform": 6,
  "addressPlatformType": 0
}
```

`addressPlatform=6` is XREX (a Taiwan exchange, recipient information is required). **Even if the recipient is yourself, you still need to provide `recipientType` and your own name.** As the amount is below the threshold, `recipientCountry` and `recipientCity` can be omitted.

**Scenario (b): The recipient is another person (individual), withdrawing to KryptoGO (a Taiwan exchange), reaching the threshold (TWD 30,000 equivalent or more)**

```javascript
// POST /wallet/withdraw/btc
{
  "protocol": "MAIN",
  "address": "1BitcoinAddressXXXXXXXXXXXXXXXX",
  "amount": "0.05",
  "recipientRelation": 1,
  "recipientType": 0,
  "recipientFirstName": "Chun",
  "recipientLastName": "Chen",
  "recipientCountry": "TW",
  "recipientCity": "taipei",
  "addressPlatform": 3,
  "addressPlatformType": 0
}
```

`addressPlatform=3` is KryptoGO, and `recipientCity="taipei"` is Taipei City in the [Recipient City List (TW)](recipient_city_tw_list.md). As the recipient is another person and the amount reaches the threshold, `recipientType`, the name, `recipientCountry` and `recipientCity` are required.

**Scenario (c): The recipient is another person (company), withdrawing to MAX (a Taiwan exchange), reaching the threshold (TWD 30,000 equivalent or more)**

```javascript
// POST /wallet/withdraw/btc
{
  "protocol": "MAIN",
  "address": "1BitcoinAddressXXXXXXXXXXXXXXXX",
  "amount": "0.05",
  "recipientRelation": 1,
  "recipientType": 1,
  "recipientCompanyName": "ABC Trading Co., Ltd.",
  "recipientCompanyTaxId": "12345678",
  "recipientCountry": "TW",
  "recipientCity": "taipei",
  "addressPlatform": 4,
  "addressPlatformType": 0
}
```

`recipientType=1` means the recipient is a company, so `recipientCompanyName` is provided instead of the name fields. When the amount reaches the threshold, a company **also requires `recipientCompanyTaxId`** (tax ID / registration number / LEI), otherwise the request will be rejected (`recipientFirstName` and `recipientLastName` are for individuals only and are not required for a company). `addressPlatform=4` is MAX.

**Scenario (d): The recipient is another person (individual) with an overseas address, withdrawing to a hot wallet (MetaMask)**

```javascript
// POST /wallet/withdraw/eth
{
  "protocol": "ERC20",
  "address": "0xasdfhaiuhsefv",
  "amount": "0.5",
  "recipientRelation": 1,
  "recipientType": 0,
  "recipientFirstName": "John",
  "recipientLastName": "Doe",
  "recipientCountry": "US",
  "recipientCity": "New York",
  "addressPlatform": 27,
  "addressPlatformType": 1
}
```

`addressPlatform=27` is MetaMask (a hot wallet). The amount in this example reaches the threshold, so `recipientCountry` and `recipientCity` are required. As the country is not `TW`, `recipientCity` is free text (`New York` in this example).

**Scenario (e): The platform is not in the list (use "Other")**

```javascript
// POST /wallet/withdraw/eth
{
  "protocol": "ERC20",
  "address": "0xasdfhaiuhsefv",
  "amount": "0.5",
  "recipientRelation": 1,
  "recipientType": 0,
  "recipientFirstName": "John",
  "recipientLastName": "Doe",
  "recipientCountry": "SG",
  "recipientCity": "Singapore",
  "addressPlatform": 0,
  "addressPlatformType": 0,
  "addressPlatformOther": "SomeNewExchangeName"
}
```

`addressPlatform=0` means "Other" (not in the list), and `addressPlatformOther` must be provided with the custom platform name. Use "Other" only when the platform is not in the list; if it is in the list, select that platform and do not provide `addressPlatformOther`. Selecting "Other" does not change the recipient information rules, it follows the same rules as other platforms (see [Recipient Information Rules](#recipient-information-rules)). The amount in this example reaches the threshold, so `recipientCountry` and `recipientCity` are also required.

# Api Response

**Response Example:**

The response of scenario (b) (BTC, `0.0499` is actually sent after deducting the fee):

```javascript
{
  "data": {
    "serial": "20260923BW51258295",
    "currency": "BTC",
    "protocol": "MAIN",
    "address": "1BitcoinAddressXXXXXXXXXXXXXXXX",
    "amount": "0.0499", //amount actually sent
    "fee": "0.0001", //fee deducted from initial amount
    "total": "0.05", //total amount deducted
    "id": "12368"
  }
}
```

**Response Fields:**

| Field | Type | Description |
| :--- | :--- | :--- |
| serial | string | The unique identifier for the withdrawal transaction. The format is `yyyyMMdd` + `BW` + 8 digits for cryptocurrency, and `yyyyMMdd` + `TW` + 8 digits for TWD |
| currency | string | The currency of the withdrawal, in uppercase |
| protocol | string | The protocol used for the withdrawal, always `MAIN` for TWD |
| address | string | The receiving address for cryptocurrency withdrawal. For TWD withdrawal, it is the bank name and the last five digits of the bank account, displayed according to the language (e.g. `XX銀行 後五碼 : 12345`) |
| amount | string | The amount actually sent (= `amount` in request - `fee`) |
| fee | string | The fee deducted from the initial amount, `0` for internal transfer or when a free withdrawal quota is available |
| total | string | The total amount deducted (amount + fee), which is the `amount` in request |
| message | string | The attached message, only returned for currencies that require a memo, omitted otherwise |
| id | string | Withdrawal transaction ID (encoded) |

> The Travel Rule fields are currently not included in the response.

[Back](../summary.md)