# MetaMask

The Solflare MetaMask Adapter is included with the Solflare Wallet Adapter and is automatically injected when the Solflare Adapter is added to the list of supported wallets.

To learn how to add the Solflare Wallet Adapter to your dApp, click [here](https://docs.solflare.com/solflare/technical/integrate-solflare/using-the-solana-wallet-adapter).

### Step 1: Visit the MetaMask Snaps Documentation

Head over to the MetaMask Snaps Documentation to get an overview of how to install and configure MetaMask Snaps.

1. Click the **"Get Started"** button on the page.
2. Follow the initial instructions to set up MetaMask with Snaps compatibility if you haven't already.

### Step 2: Install Required Dependencies

In your React project, install the required Solana wallet adapter libraries and dependencies by running the following command:

{% code overflow="wrap" %}
```
npm install @solana/wallet-adapter-react @solana/wallet-adapter-react-ui @solana/wallet-adapter-wallets @solana/web3.js @solana/wallet-adapter-base
```
{% endcode %}



### Step 3: Integrate Solflare with MetaMask Snaps

The **Solflare Wallet Adapter** automatically includes the **MetaMask Solflare Snaps** integration. Follow these steps to implement it in your dApp:

#### Create a Wallet Context Provider

1. In your `src` directory, create a file called `WalletContextProvider.js`.
2. Add the following code to initialize the Solflare adapter with MetaMask Snaps:

```javascript
import React, { useMemo } from "react";
import {
  ConnectionProvider,
  WalletProvider,
} from "@solana/wallet-adapter-react";
import { WalletModalProvider } from "@solana/wallet-adapter-react-ui";
import { SolflareWalletAdapter } from "@solana/wallet-adapter-wallets";
import { clusterApiUrl } from "@solana/web3.js";
import { WalletAdapterNetwork } from "@solana/wallet-adapter-base";

const WalletContextProvider = ({ children }) => {
  // Define the Solana network (Devnet, Testnet, or Mainnet)
  const network = WalletAdapterNetwork.Devnet;

  // Set up the Solana RPC endpoint
  const endpoint = useMemo(() => clusterApiUrl(network), [network]);

  // Add Solflare Wallet Adapter (with MetaMask Snaps integration)
  const wallets = useMemo(() => [new SolflareWalletAdapter()], []);

  return (
    <ConnectionProvider endpoint={endpoint}>
      <WalletProvider wallets={wallets}>
        <WalletModalProvider>{children}</WalletModalProvider>
      </WalletProvider>
    </ConnectionProvider>
  );
};

export default WalletContextProvider;

```

### Step 4: Wrap Your App with the Provider

To enable wallet functionality, wrap your app with the `WalletContextProvider`.

#### Example: `App.js`

```javascript
import React from "react";
import WalletContextProvider from "./WalletContextProvider";
import "@solana/wallet-adapter-react-ui/styles.css"; // Import UI styles

function App() {
  return (
    <WalletContextProvider>
      <div>
        <h1>Welcome to Solflare with MetaMask Snaps</h1>
        {/* Add wallet interaction components here */}
      </div>
    </WalletContextProvider>
  );
}

export default App;

```



### Step 5: Add Wallet Modal and Connection Button

Use the `WalletMultiButton` component from `@solana/wallet-adapter-react-ui` to allow users to connect their wallets:

#### Example: `Home.js`

```javascript
import React from "react";
import { WalletMultiButton } from "@solana/wallet-adapter-react-ui";

const Home = () => {
  return (
    <div>
      <h1>Connect Your Solflare Wallet</h1>
      <WalletMultiButton />
    </div>
  );
};

export default Home;

```

### Step 6: Test MetaMask Snaps with Solflare

<figure><img src="../../.gitbook/assets/mm solfare code (1).png" alt=""><figcaption></figcaption></figure>

1.  Start your development server:

    ```javascript
    npm run dev
    ```
2. Open your application in a browser.
3. Click the **Connect Wallet** button, and select **Solflare**. If MetaMask is installed and Snaps are set up, the integration will prompt you to authorize access.

