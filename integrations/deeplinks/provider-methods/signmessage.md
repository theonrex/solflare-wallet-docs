# SignMessage

#### **Sign a Message with Solflare**

After establishing a connection to Solflare, an application can request the user to sign a message.\
Message signing is a convenient way to verify address ownership without incurring any network fees.

Applications can create custom messages that are displayed to users via Solflare's signature prompt.

***

#### **How It Works**

To send a message for signing:

1. Provide the message as a **hex** or **UTF-8** encoded string.
2. Convert the string into a `Uint8Array` and encode it in **base58**.
3. Request Solflare to sign the encoded message via the user's wallet.

For signature verification details, refer to the Encryption Resources.

***

#### **Base URL**

```plaintext
https://solflare.com/ul/v1/signMessage
```

***

#### **Query String Parameters**

| **Parameter**                    | **Required** | **Description**                                                                                                              |
| -------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **`dapp_encryption_public_key`** | Yes          | The app's original encryption public key from the existing Connect session.                                                  |
| **`nonce`**                      | Yes          | A base58-encoded nonce used to encrypt the request.                                                                          |
| **`redirect_link`**              | Yes          | The URI where Solflare should redirect the user after processing. Must be URL-encoded. See Specifying Redirects for details. |
| **`payload`**                    | Yes          | An encrypted JSON string containing the message, session token, and display settings. Refer to the example below.            |

***

#### **Payload Structure**

```json
{
  "message": "...", // the message, base58-encoded
  "session": "...", // token received from the connect method
  "display": "utf8" | "hex" // optional, defaults to utf8
}
```

| **Field**     | **Type** | **Required** | **Description**                                                                                            |
| ------------- | -------- | ------------ | ---------------------------------------------------------------------------------------------------------- |
| **`message`** | String   | Yes          | The message to be signed by the user, encoded in base58. Solflare will display this message in the prompt. |
| **`session`** | String   | Yes          | The session token received from the Connect method. Refer to Handling Sessions for details.                |
| **`display`** | String   | No           | Specifies how the message should be displayed (`utf8` or `hex`). Defaults to `utf8`.                       |

***

#### **Returns**

**Approve**

| **Parameter** | **Description**                                                                                                                               |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **`nonce`**   | A base58-encoded nonce used to encrypt the response.                                                                                          |
| **`data`**    | An encrypted JSON string containing the signed message. Refer to Encryption for details on decryption. Encrypted bytes are encoded in base58. |

**Decrypted `data` Parameter Example**

```json
{
  "signature": "..." // the message signature, base58-encoded
}
```

| **Field**       | **Type** | **Description**                                                                               |
| --------------- | -------- | --------------------------------------------------------------------------------------------- |
| **`signature`** | String   | The signed message, encoded in base58. Developers can use this signature to verify ownership. |

***

**Reject**

If the request is rejected, the following query parameters are returned:

| **Parameter**      | **Description**                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| **`errorCode`**    | A code identifying the error. Refer to the Errors section for a complete list of possible error codes. |
| **`errorMessage`** | A description of the error.                                                                            |

**Reject Example**

```json
{
  "errorCode": "...",
  "errorMessage": "..."
}
```

***

#### **Example**

For a practical implementation of the `signMessage` method, refer to the demo application.
