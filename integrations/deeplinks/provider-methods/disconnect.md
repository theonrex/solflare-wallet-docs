# Disconnect

### **Disconnecting from Solflare**

After establishing an initial [connection](connect.md), an app can disconnect from Solflare at any time. Once disconnected, Solflare will reject all signature requests until a new connection is established.

***

### **Base URL**

```http
https://solflare.com/ul/v1/disconnect
```

***

### **Query String Parameters**

| Parameter                         | Required | Description                                                                                                                                                                |
| --------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **dapp\_encryption\_public\_key** | Yes      | The app's original encryption public key used during the existing Connect session.                                                                                         |
| **`nonce`**                       | Yes      | A base58-encoded nonce used to encrypt the request.                                                                                                                        |
| **`redirect_link`**               | Yes      | The URI to redirect the user after disconnecting. Must be URL-encoded. See [Specifying Redirects](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) for details. |
| **`payload`**                     | Yes      | An encrypted JSON string containing the session token from the Connect method. See example below.                                                                          |

### **Payload Example**

```json
{
  "session": "..." // token received from the connect method
}
```

| Field         | Type   | Description                                                           |
| ------------- | ------ | --------------------------------------------------------------------- |
| **`session`** | String | <p>The session token received </p><p>during the Connect process. </p> |

{% hint style="success" %}
Refer to [Handling Sessions](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) for details.
{% endhint %}

***

### **Returns**

**Approve**

No query parameters are returned upon successful disconnection.

### **Reject**

If the disconnection request fails, the following query parameters are returned:

| Parameter          | Description                    |
| ------------------ | ------------------------------ |
| **`errorCode`**    | A code identifying the error.  |
| **`errorMessage`** | A description of the error.    |

{% hint style="success" %}
Refer to the [Errors](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) section for a list of possible error codes.
{% endhint %}

### **Reject Example**

```json
{
  "errorCode": "...",
  "errorMessage": "..."
}
```

***

### **Example**

{% hint style="success" %}
For a working implementation of the disconnect method, refer to the [demo application](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640).
{% endhint %}

