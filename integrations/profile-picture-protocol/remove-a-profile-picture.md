# Remove a Profile Picture

### **Allow Users to Remove Their Profile Picture (PFP)**

To allow users to remove their profile picture (PFP) from your protocol’s front-end, you can use the functionality below, which creates a transaction to remove the user’s profile picture (SPP).

#### **Function: `createRemoveProfilePictureTransaction`**

The `createRemoveProfilePictureTransaction` function generates a transaction that allows users to remove their existing profile picture.

#### **Function Signature**

{% code overflow="wrap" %}
```typescript
function createRemoveProfilePictureTransaction(ownerPublicKey: PublicKey): Promise<Transaction>;
```
{% endcode %}

### **Parameters**

* **ownerPublicKey** (`PublicKey`):\
  The public key of the wallet that will no longer have the profile picture. This is the user’s wallet address.

#### **Return Value**

* The function returns a **Web3 Transaction object**. This transaction can be signed and sent by the user to remove their profile picture.

### **Example Usage in React**

Below is an example of how you can integrate this functionality in a React app. The user can click a button to create and send the transaction to remove their PFP.

```javascript
import React, { useState } from 'react';
import { Connection, PublicKey, Transaction } from '@solana/web3.js';
import { createRemoveProfilePictureTransaction } from '@solflare-wallet/pfp'; // Import the function

const connection = new Connection('https://api.mainnet-beta.solana.com');

function RemoveProfilePicture() {
  const [loading, setLoading] = useState(false);
  const [transactionStatus, setTransactionStatus] = useState('');
  
  const handleRemovePFP = async () => {
    setLoading(true);
    setTransactionStatus('Creating transaction to remove PFP...');

    try {
      // Replace this with the actual PublicKey of the user's wallet
      const ownerPublicKey = new PublicKey('YOUR_WALLET_PUBLIC_KEY'); // User's wallet address

      // Create the transaction to remove the profile picture
      const transaction = await createRemoveProfilePictureTransaction(ownerPublicKey);
      
      // Now send the transaction (this will need to be signed and sent by the user's wallet)
      // You can use a Solana wallet adapter for signing and sending the transaction
      // e.g., Solflare, Phantom, etc.
      
      setTransactionStatus('Transaction created. Please sign the transaction to remove your PFP.');

      // For this example, we’ll just log the transaction
      console.log(transaction);
    } catch (error) {
      setTransactionStatus('Error creating transaction');
      console.error('Error:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      <button onClick={handleRemovePFP} disabled={loading}>
        {loading ? 'Removing PFP...' : 'Remove Profile Picture'}
      </button>
      {transactionStatus && <p>{transactionStatus}</p>}
    </div>
  );
}

export default RemoveProfilePicture;
```

### **Steps:**

1. **User Clicks the Button:**\
   The user clicks the "Remove Profile Picture" button to trigger the transaction creation.
2. **Create the Transaction:**\
   The function `createRemoveProfilePictureTransaction` is called with the necessary wallet information to create a transaction that removes the user's profile picture.
3. **Send the Transaction:**\
   After the transaction is created, you can use a Solana wallet (like Solflare or Phantom) to sign and send the transaction. This part of the process requires the wallet connection, which will prompt the user to approve the transaction.
4. **Handle the Status:**\
   The status of the transaction is shown to the user, letting them know whether the transaction is being created or if there was an error.

***

### **Summary**

* **`createRemoveProfilePictureTransaction`** helps create a transaction for removing the user's profile picture.
* This transaction can be signed and sent by the user through their wallet.
* By using this function in your React app, you allow users to easily remove their profile picture and revert to the default.
