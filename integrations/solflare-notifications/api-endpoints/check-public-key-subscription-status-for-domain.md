# Check Public Key Subscription Status for Domain

No authorization header is required.

```json
POST /v1/connector/public-key/check
{
  "domain": "localhost",
  "publicKey": "GC5F...k6gZ",
}
Response
{
  "data": {
    "domain": "localhost",
    "providedPublicKey": { //or null
      "publicKey": "GC5F...k6gZ",
      "account": "123...",
      "preferences": ["general", "security", "transactional"]
    },
    "account": {
      "_id": "123..",
      "name": "Localhost",
      "status": "active",
      "type": "provider",
      "logo": "https://localhost/logo.png",
      ...
    },
  }
}
```

[\
](https://docs.solflare.com/solflare/technical/solflare-notifications/api-endpoints/view-cast-endpoint)
