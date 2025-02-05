# Connect

**Connecting with Solflare**

To interact with Solflare, an app must first establish a connection. This connection request prompts the user to share their public key, signifying their willingness to proceed.

When a user successfully connects, Solflare returns a session parameter, which must be included in all subsequent method calls.&#x20;

{% hint style="info" %}
For additional details, refer to the [Handling Sessions](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) section.
{% endhint %}

***

### **Base URL**

```plaintext
https://solflare.com/ul/v1/connect
```

***

### **Query String Parameters**

| Parameter                        | Required      |                                                                                                                                                                                          |
| -------------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`app_url`**                    | Yes           | A URL used to retrieve the app's metadata (e.g., title, icon). It must be URL-encoded.                                                                                                   |
| **`dapp_encryption_public_key`** | Yes           | A public key used for end-to-end encryption to generate a shared secret. _See_ [_Encryption_](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) _for details_.                 |
| **`redirect_link`**              | Yes           | The URI where Solflare should redirect the user upon connection. Must be URL-encoded. _Refer to_ [_Specifying Redirects_](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640)_._ |
| **`cluster`**                    | No (Optional) | The Solana network for interactions. Options: _**`mainnet-beta`**_, `testnet`, or `devnet`. Defaults to `mainnet-beta`.                                                                  |

***

### **Response**

**Approve**

{% hint style="success" %}
If the connection is approved, Solflare returns the following parameters:
{% endhint %}

| Parameter                             | Type           | Description                                                                                                                                                              |
| ------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **solflare\_encryption\_public\_key** | Base58-encoded | Encryption public key used by Solflare to establish a shared secret.                                                                                                     |
| **`nonce`**                           | Base58-encoded | A nonce used to encrypt the response.                                                                                                                                    |
| **`data`**                            | Base58-encoded | An encrypted JSON string. Apps must decrypt this using the shared secret. Refer to [Encryption](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) for details. |

### **Decrypted `data` Parameter**

The decrypted `data` object contains the following:

```json
{
  "public_key": "3huUrtWW5s5ew98eUFRYz9LPsDUQTujNzzYaB9DBkppQ",
  "session": "..."
}
```

| Field            | Type           | Description                                                                                                             |
| ---------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **`public_key`** | Base58-encoded | The user's public key.                                                                                                  |
| **`session`**    | Base58-encoded | A session token used for subsequent deeplink requests. Sessions do not expire and must be included in all future calls. |

{% hint style="warning" %}
**Note:** Treat the `session` parameter as opaque; it is only required for passing alongside other parameters. For more information, refer to [Handling Sessions](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640).
{% endhint %}

***

### **Reject**

If the connection is rejected, Solflare responds with the following query parameters:

| **Parameter**      | **Description**                                                                                                                                                   |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`errorCode`**    | A code identifying the error. _Refer to the_ [_Errors_](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640) _section for a list of possible error codes._ |
| **`errorMessage`** | A description of the error.                                                                                                                                       |

***

### **Example**

{% hint style="info" %}
For a working implementation of the connect method, refer to the [demo application](https://chatgpt.com/c/679da458-d818-8013-89ea-60bc8e83a640).
{% endhint %}



***
