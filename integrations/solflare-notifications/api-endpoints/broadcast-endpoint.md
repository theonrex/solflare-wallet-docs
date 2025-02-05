# Broadcast Endpoint

Broadcast messages have to go through the process of being manually approved before they are sent out at their scheduled time.

```json
POST /v1/casts/broadcast
Headers
{
  "Authorization": "Basic 5LQWBmQ1...FQD"
}
Body (JSON)
{
  "title": "New feature",
  "body": "We are releasing super cool feature at 1PM CET",
  "icon": "https://solflare.com/assets/logo-128.png",
  "image": "https://solflare.com/assets/logo-128.png",
  "platform": "all", 
  "topic": "general" ,
  "actionUrl": "https://solflare.com",
  "castAt": "2022-04-30T15:00:00.254Z" //UTC
}
Response
{
  "data": {
      "_id": "123...",
      "status": "pending",
      "title": "New feature",
      "body": "We are releasing super cool feature at 1PM CET",
      "icon": "https://solflare.com/assets/logo-128.png",
      "image": "https://solflare.com/assets/logo-128.png",
      "platform": "all", 
      "topic": "general" ,
      "actionUrl": "https://solflare.com",
      "castAt": "2022-04-30T15:00:00.254Z" //UTCjso
      ...
    }
}
```
