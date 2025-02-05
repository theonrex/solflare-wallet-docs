# Unicast Endpoint

```json
POST /v1/casts/unicast
Headers
{
  "Authorization": "Basic 5LQWBmQ1...FQD"
}
Body (JSON)
{
  "title": "New feature",
  "body": "We are releasing super cool feature at 1PM CET",
  "icon": "https://solflare.com/assets/logo-128.png",
  "image": null,
  "publicKey": "GC5F...k6gZ",
  "platform": "all", 
  "topic": "general",
  "actionUrl": null
}
Response
{
  "data": {
      "_id": "123...",
      "status": "pending",
      "title": "New feature",
      "body": "We are releasing super cool feature at 1PM CET",
      "icon": "https://solflare.com/assets/logo-128.png",
      "image": null,
      "publicKey": "GC5F...k6gZ",
      "platform": "all", 
      "topic": "general",
      "actionUrl": null,
      ...
    }
}
```
