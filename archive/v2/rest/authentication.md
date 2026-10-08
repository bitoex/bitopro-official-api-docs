# Authentication

# V2 End-of-life (2021-06-30)
**We have already stopped any mantainance support on v2 API. We have scheduled to remove v2 API completely on 2021-06-30. Please migrate your program to you v3 ASAP.**


| Security scheme | Header parameter |
| :--- | :--- |
| API Key | X-BITOPRO-APIKEY |
| Payload | X-BITOPRO-PAYLOAD |
| Signature | X-BITOPRO-SIGNATURE |

## API Key

### Authentication is done using an API key and a secret. To generate this pair, go to the [API Access page](https://www.bitopro.com/api_list).

## Payload

### The body in JSON encoded into Base64.

### For `GET` and `DELETE`, use **{identity: USER\_EMAIL, nonce: TIMESTAMP}** as body instead.

### **\[payload = parameters-object -&gt; JSON, encode -&gt; base64\]** For `POST`, refer to [Create an order](authentication.md).

| object | payload |
| :--- | :--- |
| `{ "identity": "support@bitoex.com", "nonce": 1554380909131}` | `eyJpZGVudGl0eSI6InN1cHBvcnRAYml0b2V4LmNvbSIsIm5vbmNlIjoxNTU0MzgwOTA5MTMxfQ==` |
| `{ "action": "BUY", "type": "limit", "price": "1.123456789", "amount": "666", "timestamp": 1554380909131 }` | `eyJhY3Rpb24iOiJCVVkiLCJhbW91bnQiOiI2NjYiLCJwcmljZSI6IjEuMTIzNDU2Nzg5IiwidGltZXN0YW1wIjoxNTU0MzgwOTA5MTMxLCJ0eXBlIjoibGltaXQifQ==` |

## Signature

### The hex digest of an HMAC-SHA384 hash where the message is your **payload**, and use your API secret to sign it. **\[signature = HMAC-SHA384\(payload, api-secret\).digest\('hex'\)\]**

|  |  |
| :--- | :--- |
| **secret** | `bitopro` |
| **payload** | `eyJpZGVudGl0eSI6InN1cHBvcnRAYml0b2V4LmNvbSIsIm5vbmNlIjoxNTU0MzgwOTA5MTMxfQ` |
| **signature** | `98ddf62831afaa56fcd64220a2b60712a3990b404a5f28a8cf37069dc3cb77d634f576895906e238e36ba50c626dfadb` |

## Node.js example

```javascript
const request = require('request')
const crypto = require('crypto')

const apiKey = '[Your API key here]'
const apiSecret = '[Your API secret here]'
const baseUrl = 'https://api.bitopro.com/v2'

const url = '/accounts/balance'
const nonce = Date.now()
const completeURL = baseUrl + url
// This is the default body for the authenticated APIs using GET method
const body = { identity: '[Your account (email)]', nonce }

const payload = new Buffer(JSON.stringify(body)).toString('base64')


const signature = crypto
   .createHmac('sha384', apiSecret)
   .update(payload)
   .digest('hex')

const options = {
   url: completeURL,
   headers: {
     'X-BITOPRO-APIKEY': apiKey,
     'X-BITOPRO-PAYLOAD': payload,    // For the authenticated APIs using DELETE method, you don't need the payload field.
     'X-BITOPRO-SIGNATURE': signature
   },
   body: JSON.stringify(body)    // For the authenticated APIs using GET method, you don't need the body field.
}

// GET
return request.get(
   options,
   function(error, response, body) {
     console.log('response:', JSON.stringify(body, 0, 2))
   }
)

// POST
return request.post(
   options,
   function(error, response, body) {
     console.log('response:', JSON.stringify(body, 0, 2))
   }
)

// DELETE
return request.delete(
   options,
   function(error, response, body) {
     console.log('response:', JSON.stringify(body, 0, 2))
   }
)
```

[Back](rest.md)

