# SignAndSendTransaction

#### **Sending Transactions via Solflare**

Once an application is connected to Solflare, it can request permission to send transactions on behalf of the user.

To send a transaction, the following steps must be completed:

1. **Create an unsigned transaction.**
2. **Request the user to sign and submit the transaction via Solflare.**
3. **Optionally, await network confirmation** using a Solana JSON RPC connection.

For detailed information about Solana transactions, refer to the solana-web3.js documentation and the [Solana Cookbook](https://solanacookbook.com/).

***

#### **Base URL**

```plaintext
https://solflare.com/ul/v1/signAndSendTransaction  
```

***

#### **Query String Parameters**

| **Parameter**                    | **Required** | **Description**                                                                                                                                |
| -------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **`dapp_encryption_public_key`** | Yes          | The app's original encryption public key from the existing Connect session.                                                                    |
| **`nonce`**                      | Yes          | A base58-encoded nonce used to encrypt the request.                                                                                            |
| **`redirect_link`**              | Yes          | The URI where Solflare should redirect the user after the transaction is processed. Must be URL-encoded. See Specifying Redirects for details. |
| **`payload`**                    | Yes          | An encrypted JSON string containing transaction details and the session token. Refer to the example below.                                     |

***

#### **Payload Structure**

```json
{
  "transaction": "...", // serialized transaction, base58-encoded
  "sendOptions": "...", // optional Solana web3.js sendOptions object
  "session": "..." // token received from the connect method
}
```

| **Field**         | **Type** | **Required** | **Description**                                                                                |
| ----------------- | -------- | ------------ | ---------------------------------------------------------------------------------------------- |
| **`transaction`** | String   | Yes          | The transaction Solflare will sign and submit. Must be serialized and base58-encoded.          |
| **`sendOptions`** | Object   | No           | Optional options for how Solflare should submit the transaction, as defined in Solana web3.js. |
| **`session`**     | String   | Yes          | The session token received from the Connect method. Refer to Handling Sessions for details.    |

***

#### **Returns**

**Approve**

| **Parameter** | **Description**                                                                                                                             |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **`nonce`**   | A base58-encoded nonce used to encrypt the response.                                                                                        |
| **`data`**    | An encrypted JSON string containing the transaction signature. Apps can decrypt the data using a shared secret. See Encryption for details. |

**Decrypted `data` Parameter Example**

```json
{  
  "signature": "..." // transaction signature, used as the transaction ID
}
```

| **Field**       | **Type** | **Description**                                                             |
| --------------- | -------- | --------------------------------------------------------------------------- |
| **`signature`** | String   | The transaction's first signature, which can be used as the transaction ID. |

**Reject**

If the transaction is rejected, the following query parameters are returned:

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

For a practical implementation of the `signAndSendTransaction` method, refer to the demo application.
