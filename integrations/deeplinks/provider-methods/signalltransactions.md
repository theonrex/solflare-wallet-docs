# SignAllTransactions

### **Signing Multiple Transactions with Solflare**

Once connected to Solflare, an application can request the user to sign multiple transactions simultaneously. Unlike `SignAndSendTransaction`, Solflare does **not** submit these transactions to the network.\
Applications can use **web3.js**’s `sendRawTransaction` to manually submit the signed transactions to the network.

***

#### **Base URL**

```plaintext
https://solflare.com/ul/v1/signAllTransactions
```

***

#### **Query String Parameters**

| **Parameter**                    | **Required** | **Description**                                                                                                              |
| -------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **`dapp_encryption_public_key`** | Yes          | The app's original encryption public key from the existing Connect session.                                                  |
| **`nonce`**                      | Yes          | A base58-encoded nonce used to encrypt the request.                                                                          |
| **`redirect_link`**              | Yes          | The URI where Solflare should redirect the user after processing. Must be URL-encoded. See Specifying Redirects for details. |
| **`payload`**                    | Yes          | An encrypted JSON string containing the array of transactions and session token. Refer to the example below.                 |

***

#### **Payload Structure**

```json
{
  "transactions": [
    "...", // serialized transaction, bs58-encoded
    "..."  // serialized transaction, bs58-encoded
  ],
  "session": "..." // token received from the connect method
}
```

| **Field**          | **Type**         | **Required** | **Description**                                                                             |
| ------------------ | ---------------- | ------------ | ------------------------------------------------------------------------------------------- |
| **`transactions`** | Array of Strings | Yes          | A serialized array of transactions, each base58-encoded, that Solflare will sign.           |
| **`session`**      | String           | Yes          | The session token received from the Connect method. Refer to Handling Sessions for details. |

***

#### **Returns**

**Approve**

| **Parameter** | **Description**                                                                                                                                                                  |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`nonce`**   | A base58-encoded nonce used to encrypt the response.                                                                                                                             |
| **`data`**    | An encrypted JSON string containing the signed transactions. Refer to Encryption to learn how to decrypt this data using a shared secret. Encrypted bytes are encoded in base58. |

**Decrypted `data` Parameter Example**

```json
{
  "transactions": [
    "...", // signed serialized transaction, bs58-encoded
    "..."  // signed serialized transaction, bs58-encoded
  ] 
}
```

| **Field**          | **Type**         | **Description**                                                   |
| ------------------ | ---------------- | ----------------------------------------------------------------- |
| **`transactions`** | Array of Strings | An array of signed, serialized transactions, each base58-encoded. |

* Solflare will **not** submit these transactions. Applications can use **web3.js**’s `sendRawTransaction` method to submit them manually.

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

For a practical implementation of the `signAllTransactions` method, refer to the demo application.
