# Set NFT as Profile Picture

### **Allow Users to Change Their Profile Picture (PFP)**

To let users change their profile picture (PFP) on your protocol’s front-end, you can use the functionality below, which helps create a transaction to update the user’s PFP to a new NFT.

### **Function: `createSetProfilePictureTransaction`**

The `createSetProfilePictureTransaction` function creates a transaction that will allow users to set their new profile picture by selecting an NFT from their wallet.

### **Function Signature**

{% code overflow="wrap" %}
```typescript
function createSetProfilePictureTransaction(ownerPublicKey: PublicKey, mintPublicKey: PublicKey, tokenAccountPublicKey: PublicKey): Promise<Transaction>;
```
{% endcode %}

### **Parameters**

* **ownerPublicKey** (`PublicKey`):\
  The public key of the wallet that will own the NFT being set as the profile picture. This is the user’s wallet address.
* **mintPublicKey** (`PublicKey`):\
  The public key of the NFT's mint that the user wants to set as their profile picture.
* **tokenAccountPublicKey** (`PublicKey`):\
  The public key of the token account that holds the NFT. This is where the NFT resides.

### **Return Value**

* The function returns a **Web3 Transaction object**. This transaction can be signed and sent by the user to update their profile picture.

### **Example Usage in React**

Below is an example of how you can integrate this functionality in a React app. The user can click a button to create and send the transaction to set their PFP.

```javascript
import React, { useState } from 'react';
import { Connection, PublicKey, Transaction } from '@solana/web3.js';
import { createSetProfilePictureTransaction } from '@solflare-wallet/pfp'; // Import the function

const connection = new Connection('https://api.mainnet-beta.solana.com');

function ChangeProfilePicture() {
  const [loading, setLoading] = useState(false);
  const [transactionStatus, setTransactionStatus] = useState('');
  
  const handleSetPFP = async () => {
    setLoading(true);
    setTransactionStatus('Creating transaction...');

    try {
      // Replace these with actual PublicKeys from your app's wallet and the NFT to be used as PFP
      const ownerPublicKey = new PublicKey('YOUR_WALLET_PUBLIC_KEY'); // User's wallet address
      const mintPublicKey = new PublicKey('NFT_MINT_PUBLIC_KEY'); // The NFT's mint address
      const tokenAccountPublicKey = new PublicKey('NFT_TOKEN_ACCOUNT_PUBLIC_KEY'); // Token account holding the NFT

      // Create the transaction
      const transaction = await createSetProfilePictureTransaction(ownerPublicKey, mintPublicKey, tokenAccountPublicKey);
      
      // Now send the transaction (this will need to be signed and sent by the user's wallet)
      // You can use a Solana wallet adapter for signing and sending the transaction
      // e.g., Solflare, Phantom, etc.
      
      setTransactionStatus('Transaction created. Please sign the transaction to change your PFP.');

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
      <button onClick={handleSetPFP} disabled={loading}>
        {loading ? 'Creating Transaction...' : 'Change Profile Picture'}
      </button>
      {transactionStatus && <p>{transactionStatus}</p>}
    </div>
  );
}

export default ChangeProfilePicture;
```

### **Steps:**

1. **User Clicks the Button:**\
   The user clicks the "Change Profile Picture" button to trigger the transaction creation.
2. **Create the Transaction:**\
   The function `createSetProfilePictureTransaction` is called with the necessary wallet and NFT information to create a transaction.
3. **Send the Transaction:**\
   After the transaction is created, you can use a Solana wallet (like Solflare or Phantom) to sign and send it. This part of the process requires the wallet connection, which will prompt the user to approve the transaction.
4. **Handle the Status:**\
   The status of the transaction is shown to the user, letting them know whether the transaction is being created or if there was an error.

***

### **Summary**

* **`createSetProfilePictureTransaction`** helps create a transaction for setting an NFT as the user's profile picture.
* This transaction can be signed and sent by the user through their wallet.
* By using this function in your React app, you allow users to seamlessly change their profile pictures using Solana NFTs.
