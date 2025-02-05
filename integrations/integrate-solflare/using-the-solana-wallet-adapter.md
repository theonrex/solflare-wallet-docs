# Using the Solana Wallet Adapter

This tutorial explains how to integrate the **Solflare Wallet** into your Solana dApp using the **Solana Wallet Adapter**. We’ll guide you through installing dependencies, configuring adapters, and modularizing your code for a clean setup.



### **1. Prerequisites**

Ensure you have the following:

* A React or Next.js project set up.
* Basic knowledge of Solana and dApp development.
* Installed packages: `@solana/wallet-adapter-react`, `@solana/wallet-adapter-wallets`, and `@solana/web3.js`.

### **2. Install Necessary Packages**



{% tabs %}
{% tab title="Install all required wallet adapter packages:" %}
{% code overflow="wrap" %}
```bash
npm install @solana/wallet-adapter-wallets @solana/wallet-adapter-react @solana/web3.js
```
{% endcode %}
{% endtab %}

{% tab title="To include only Solflare:" %}
```bash
npm install @solana/wallet-adapter-solflare
```


{% endtab %}
{% endtabs %}

### **3. Configure Wallet Adapters**

In your `App.js` or `App.tsx`, add the **Solflare Wallet Adapter** to your list of wallets.

**Code Example:**

```javascript
import { useMemo } from 'react';
import { ConnectionProvider, WalletProvider } from '@solana/wallet-adapter-react';
import { SolflareWalletAdapter } from '@solana/wallet-adapter-wallets';

const App = () => {
  const RPC_URL = process.env.NEXT_PUBLIC_RPC_URL || 'https://api.mainnet-beta.solana.com';

  const wallets = useMemo(
    () => [
      new SolflareWalletAdapter(),
      // Add other adapters like Phantom or Torus here
    ],
    []
  );

  return (
    <ConnectionProvider endpoint={RPC_URL}>
      <WalletProvider autoConnect wallets={wallets}>
        <h1>Solana dApp</h1>
        {/* Add your app components here */}
      </WalletProvider>
    </ConnectionProvider>
  );
};

export default App;
```

***

### **4. Modularize the Wallet Button**

For clean code and reusability, move the wallet button logic into a separate component.

**Create a `WalletButton.js` file:**

```javascript
import { useWallet } from '@solana/wallet-adapter-react';

const WalletButton = () => {
  const { connect, disconnect, connected, publicKey } = useWallet();

  const walletAddress = publicKey ? publicKey.toBase58() : null;

  return (
    <div>
      {connected ? (
        <>
          <p>Wallet: {walletAddress}</p>
          <button onClick={disconnect} style={styles.disconnectButton}>
            Disconnect Wallet
          </button>
        </>
      ) : (
        <button onClick={connect} style={styles.connectButton}>
          Connect Wallet
        </button>
      )}
    </div>
  );
};

const styles = {
  connectButton: {
    padding: '10px 20px',
    backgroundColor: '#4CAF50',
    color: 'white',
    borderRadius: '8px',
    border: 'none',
    cursor: 'pointer',
  },
  disconnectButton: {
    padding: '10px 20px',
    backgroundColor: '#FF6F61',
    color: 'white',
    borderRadius: '8px',
    border: 'none',
    cursor: 'pointer',
  },
};

export default WalletButton;
```

***

### **5. Use the Wallet Button in Your App**

Update your main `App.js` to use the `WalletButton` component.

```javascript
import WalletButton from './components/WalletButton';

const App = () => {
  return (
    <ConnectionProvider endpoint="https://api.mainnet-beta.solana.com">
      <WalletProvider autoConnect wallets={wallets}>
        <div style={{ textAlign: 'center' }}>
          <h1>Welcome to My Solana dApp</h1>
          <WalletButton />
        </div>
      </WalletProvider>
    </ConnectionProvider>
  );
};
```

***

### **6. Environment Variables**

Store your RPC endpoint in a `.env` file for better environment management:

```arduino
NEXT_PUBLIC_RPC_URL=https://api.mainnet-beta.solana.com
```

***

### **Best Practices**

1. **Error Handling**: Use `try/catch` around wallet connections for better user feedback.
2. **Custom Styling**: Adjust button styles to match your app's design.
3. **Test in Different Environments**: Ensure compatibility with both Mainnet and Devnet.
