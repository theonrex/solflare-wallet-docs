---
description: SPP
---

# Profile Picture Protocol

### **Solana Profile Picture Protocol (SPP) - A New Way to Personalize Your Solana Experience**

The **Solana Profile Picture Protocol (SPP)** is an exciting feature that allows users to set a **Metaplex-standard NFT** as a universal **Profile Picture (PFP)** across the Solana blockchain. This protocol adds a layer of personalization to your Solana identity, helping users make their mark in the ecosystem.

#### **Why We Created the Solana Profile Picture Protocol**

We designed the SPP with three main goals in mind:

1. **Enhanced Personalization & Identity**: Users can now create a more personalized experience within Solana applications by having a unique profile picture tied to their identity.
2. **Improved User Experience for Transactions**: When sending transactions, users will see a visual representation of the recipient's PFP, helping them quickly confirm they're sending assets to the correct person or address.
3. **Security Layer for Address Book**: The PFP also serves as an extra layer of security, ensuring that users can visually identify the correct recipient from their address book before sending any transactions.

***

### **How It Works**

With the Solana Profile Picture Protocol, a single **Token-standard NFT** can be chosen as the user's universal PFP. This makes it easy for users to have a consistent, recognizable identity across Solana apps.

Solana protocols can integrate SPP to show these PFPs on their front end and offer users the option to update their PFP by setting a new one.

***

### **Integration Guide**

If you are a Solana developer looking to integrate the SPP into your app, here's how you can get started.

1.  **Install the NPM package**\
    You can install the official SPP NPM package to integrate PFP functionality into your dApp:

    ```bash
    npm install @solflare-wallet/pfp
    ```
2.  **Fetch the Profile Picture**\
    Once the package is installed, use the following code to fetch the PFP for a specific Solana wallet address.

    ```javascript
    import { Connection, PublicKey } from '@solana/web3.js';
    import { getProfilePicture } from '@solflare-wallet/pfp';

    const connection = new Connection('https://api.mainnet-beta.solana.com');
    const walletPubkey = new PublicKey('ES8rZr16f5eAc9PkUcAbafwg5JjEJANbpwu92CF2Cbox'); // Replace with the wallet address

    // Get the PFP for the wallet
    const { isAvailable, url } = await getProfilePicture(connection, walletPubkey);

    if (isAvailable) {
      console.log('Profile Picture URL:', url);
    } else {
      console.log('No PFP set for this wallet.');
    }
    ```

    * `isAvailable`: A boolean that indicates whether the wallet has a PFP set.
    * `url`: The URL of the PFP image if it exists.

***

#### **Need Help?**

If you encounter any issues or have questions, the **Solflare team** is here to help! Feel free to reach out to us via:

* **Twitter**: [@solflare\_wallet](https://twitter.com/solflare_wallet)
* **Discord**: Join our community
