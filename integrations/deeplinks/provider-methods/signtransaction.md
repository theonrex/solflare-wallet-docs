# SignTransaction

### **Sign and Send Transaction with Solflare**

The **SignAndSendTransaction** method is the simplest and most recommended way to send a transaction.\
By letting Solflare sign and immediately submit the transaction, this method ensures enhanced safety for users and provides a simpler API for developers.

However, applications can also request only the **signature** from Solflare, allowing them to submit the transaction independently using **web3.js**’s `sendRawTransaction` method.

***

#### **Base URL**

```plaintext
https://solflare.com/ul/v1/signTransaction
```

***

#### **Query String Parameters**

| **Parameter**                    | **Required** | **Description**                                                                                                              |
| -------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **`dapp_encryption_public_key`** | Yes          | The app's original encryption public key from the existing Connect session.                                                  |
| **`nonce`**                      | Yes          | A base58-encoded nonce used to encrypt the request.                                                                          |
| **`redirect_link`**              | Yes          | The URI where Solflare should redirect the user after processing. Must be URL-encoded. See Specifying Redirects for details. |
| **`payload`**                    | Yes          | An encrypted JSON string containing the transaction and session token. Refer to the example below.                           |

***

#### **Payload Structure**

```json
{
  "transaction": "...", // serialized transaction, base58-encoded
  "session": "..." // token received from the connect method
}
```

| **Field**         | **Type** | **Required** | **Description**                                                                             |
| ----------------- | -------- | ------------ | ------------------------------------------------------------------------------------------- |
| **`transaction`** | String   | Yes          | A serialized transaction that Solflare will sign. It must be base58-encoded.                |
| **`session`**     | String   | Yes          | The session token received from the Connect method. Refer to Handling Sessions for details. |

***

#### **Returns**

**Approve**

| **Parameter** | **Description**                                                                                                                                   |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`nonce`**   | A base58-encoded nonce used to encrypt the response.                                                                                              |
| **`data`**    | An encrypted JSON string containing the signed transaction. Refer to Encryption for details on decryption. Encrypted bytes are encoded in base58. |

**Decrypted `data` Parameter Example**

```json
{
  "transaction": "..." // signed serialized transaction, base58-encoded
}
```

| **Field**         | **Type** | **Description**                                                                                                                                                                   |
| ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`transaction`** | String   | The signed and serialized transaction, base58-encoded. Solflare will **not** submit this transaction. Developers can manually submit it using **web3.js**’s `sendRawTransaction`. |

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

For a practical implementation of the `signTransaction` method, refer to the demo application.
