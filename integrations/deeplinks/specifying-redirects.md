# Specifying Redirects

All Methods support a `redirect_link=` param that lets Solflare know how to get back to the original app. The URI specified by this param should be URL encoded.

The following is an example of a `mydapp://onSolflareConnected` redirect URI:

```json
redirect_link%3Dmydapp%3A%2F%2FonSolflareConnected
```

If the deeplink request to Solflare comes with a response, Solflare will append the results as query parameters in the `redirect_link=` upon redirecting.

```json
redirect_link=mydapp://onSolflareConnected?data=...
```
