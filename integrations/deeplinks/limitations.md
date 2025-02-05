# Limitations

#### **Solflare Error Codes**

When interacting with Solflare for tasks like establishing a connection, sending a transaction, or signing a message, you might encounter errors.&#x20;

Below is a list of possible error codes and their explanations, inspired by Ethereum's EIP-1474 and EIP-1193.

#### **Error Codes and Descriptions**

* **4900 - Disconnected**\
  **Description**: Solflare could not connect to the network.
* **4100 - Unauthorized**\
  **Description**: The requested method and/or account have not been authorized by the user.
* **4001 - User Rejected Request**\
  **Description**: The user rejected the request through Solflare.
* **-32000 - Invalid Input**\
  **Description**: Missing or invalid parameters.
* **-32002 - Requested Resource Not Available**\
  **Description**: This error occurs when an app attempts to submit a new transaction while Solflare’s approval dialog is already open for a previous transaction. Only one approval window can be open at a time. Users should approve or reject their transactions before initiating a new one.
* **-32003 - Transaction Rejected**\
  **Description**: Solflare does not recognize a valid transaction.
* **-32601 - Method Not Found**\
  **Description**: Solflare does not recognize the requested method.
* **-32603 - Internal Error**\
  **Description**: Something went wrong within Solflare.

***

#### **Example Usage**

Here’s an example of how you might handle errors in your code:

```javascript
try {
  await window.solana.signMessage();
} catch (err) {
  // Example output: {code: 4100, message: 'The requested method and/or account has not been authorized by the user.'}
}
```

