# Solflare Wallet SDK

### **Tutorial: Integrating Solflare Wallet SDK in a React App**

In this tutorial, we'll walk you through how to integrate the **Solflare Wallet SDK** into your React app. We'll cover everything from setting up the wallet to sending transactions and signing messages.

***

### **Step 1: Install the Solflare Wallet SDK**

First, we need to install the **Solflare Wallet SDK** package, which allows us to integrate Solflare into our React app.

Run the following command in your project directory:

```bash
npm install @solflare-wallet/sdk@latest
```

***

### **Step 2: Initialize the Wallet**

The first step is to initialize the Solflare wallet. This involves creating a wallet instance and setting up event listeners to detect when the wallet connects or disconnects.

**Create a file named `InitializeWallet.js`**

```jsx
// InitializeWallet.js
import React, { useState, useEffect } from 'react';
import Solflare from '@solflare-wallet/sdk';

const InitializeWallet = () => {
  const [wallet, setWallet] = useState(null);
  const [publicKey, setPublicKey] = useState(null);

  // Initialize the wallet and set up event listeners
  useEffect(() => {
    const walletInstance = new Solflare();
    setWallet(walletInstance);

    walletInstance.on('connect', () => {
      console.log('Wallet connected:', walletInstance.publicKey.toString());
      setPublicKey(walletInstance.publicKey.toString());
    });

    walletInstance.on('disconnect', () => {
      console.log('Wallet disconnected');
      setPublicKey(null);
    });

    return () => {
      walletInstance.removeAllListeners(); // Clean up listeners
    };
  }, []);

  return (
    <div>
      <h2>Initialize Solflare Wallet</h2>
      {wallet ? (
        <p>Wallet initialized. Public Key: {publicKey || 'Not connected'}</p>
      ) : (
        <p>Loading wallet...</p>
      )}
    </div>
  );
};

export default InitializeWallet;
```

***

### **Step 3: Connect to the Wallet**

Now that we’ve initialized the wallet, let’s set up a button to **connect** the wallet to your dApp. When the user clicks the button, we’ll trigger the `connect` function.

**Create a file named `ConnectWallet.js`**

```jsx
// ConnectWallet.js
import React from 'react';

const ConnectWallet = ({ wallet, setPublicKey }) => {
  const connectToWallet = async () => {
    try {
      await wallet.connect(); // This will connect the wallet
      setPublicKey(wallet.publicKey.toString()); // Store the public key after connection
      console.log('Connected wallet:', wallet.publicKey.toString());
    } catch (error) {
      console.error('Failed to connect wallet:', error);
    }
  };

  return (
    <div>
      <h2>Connect Solflare Wallet</h2>
      <button onClick={connectToWallet}>Connect Wallet</button>
    </div>
  );
};

export default ConnectWallet;
```

***

### **Step 4: Disconnect the Wallet**

We also want to provide an option to **disconnect** the wallet. When the user clicks the "Disconnect" button, we’ll trigger the `disconnect` function.

**Create a file named `DisconnectWallet.js`**

```jsx
// DisconnectWallet.js
import React from 'react';

const DisconnectWallet = ({ wallet, setPublicKey }) => {
  const disconnectWallet = () => {
    wallet.disconnect(); // Disconnect the wallet
    setPublicKey(null); // Clear the public key
    console.log('Wallet disconnected');
  };

  return (
    <div>
      <h2>Disconnect Solflare Wallet</h2>
      <button onClick={disconnectWallet}>Disconnect Wallet</button>
    </div>
  );
};

export default DisconnectWallet;
```

***

### **Step 5: Send a Solana Transaction**

After connecting the wallet, we can send **Solana transactions**. In this example, we’ll create a basic transaction and send it using the wallet.

**Create a file named `SendTransaction.js`**

```jsx
// SendTransaction.js
import React from 'react';
import { Transaction } from '@solana/web3.js';

const SendTransaction = ({ wallet }) => {
  const sendTransaction = async () => {
    try {
      const transaction = new Transaction();
      // Add transaction instructions here (e.g., transfer, stake, etc.)

      const signature = await wallet.signAndSendTransaction(transaction);
      console.log('Transaction sent! Signature:', signature);
    } catch (error) {
      console.error('Transaction failed:', error);
    }
  };

  return (
    <div>
      <h2>Send Solana Transaction</h2>
      <button onClick={sendTransaction}>Send Transaction</button>
    </div>
  );
};

export default SendTransaction;
```

***

### **Step 6: Sign a Message**

In this step, we’ll show you how to **sign a custom message** using the wallet. This can be useful for verifying ownership of a wallet or other use cases.

**Create a file named `SignMessage.js`**

```jsx
// SignMessage.js
import React, { useState } from 'react';

const SignMessage = ({ wallet }) => {
  const [messageSignature, setMessageSignature] = useState(null);

  const signMessage = async () => {
    try {
      const message = 'To verify your wallet on https://example.com';
      const messageBytes = new TextEncoder().encode(message);

      const signature = await wallet.signMessage(messageBytes, 'utf8');
      setMessageSignature(signature);

      console.log('Message signed successfully:', signature);
    } catch (error) {
      console.error('Message signing failed:', error);
    }
  };

  return (
    <div>
      <h2>Sign Message</h2>
      <button onClick={signMessage}>Sign Message</button>
      {messageSignature && (
        <div>
          <h3>Message Signature</h3>
          <pre>{JSON.stringify(messageSignature, null, 2)}</pre>
        </div>
      )}
    </div>
  );
};

export default SignMessage;
```

***

### **Step 7: Bring It All Together in `App.js`**

Finally, we’ll bring everything together into a single React component that integrates the wallet and exposes all the functionality.

**Create or update your `App.js` file:**

```jsx
// App.js
import React, { useState } from 'react';
import InitializeWallet from './InitializeWallet';
import ConnectWallet from './ConnectWallet';
import DisconnectWallet from './DisconnectWallet';
import SendTransaction from './SendTransaction';
import SignMessage from './SignMessage';

const App = () => {
  const [wallet, setWallet] = useState(null);
  const [publicKey, setPublicKey] = useState(null);

  return (
    <div className="App">
      <h1>Solflare Wallet SDK Integration</h1>

      {/* Initialize Wallet */}
      <InitializeWallet />

      {/* Conditionally render Connect, Disconnect, Send Transaction, and Sign Message components */}
      {wallet && !publicKey && (
        <ConnectWallet wallet={wallet} setPublicKey={setPublicKey} />
      )}
      {wallet && publicKey && (
        <>
          <p>Connected Wallet: {publicKey}</p>
          <SendTransaction wallet={wallet} />
          <SignMessage wallet={wallet} />
          <DisconnectWallet wallet={wallet} setPublicKey={setPublicKey} />
        </>
      )}
    </div>
  );
};

export default App;
```

***

### **Summary of What You’ve Built**

* **InitializeWallet.js**: Initializes the Solflare wallet and sets up event listeners.
* **ConnectWallet.js**: Handles wallet connection through a button.
* **DisconnectWallet.js**: Handles wallet disconnection and clears the public key.
* **SendTransaction.js**: Allows users to send a Solana transaction.
* **SignMessage.js**: Allows users to sign a custom message.
* **App.js**: The main component that integrates all of the above functionalities.

***

### **How to Run**

1. Follow the steps to install the SDK.
2. Copy each of the code snippets into their respective files.
3. Import each component into `App.js` as shown.
4. Run your React app with:

```bash
npm start
```

Now you should have a working Solflare Wallet integration in your React app!
