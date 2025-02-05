# Solflare Notifications

### **Solflare Wallet - Notification Center Integration**

Solflare Wallet offers a simple, no-code solution to send notifications directly to your users via the Notification Center within the Solflare Wallet. This allows you to notify users about important updates and events.

#### **Notifications Delivered to Users**

Users will receive the following types of notifications in their Solflare Wallet:

* **App-Specific Notifications**: Notifications that are unique to your application or dApp.
* **Notifications for Protocols Without Applications**: Notifications for projects or protocols like NFT projects that may not have a full app.
* **General Solflare Updates**: Important updates or news from Solflare itself.

#### **Notification Delivery Channels**

Notifications are delivered through multiple channels, including:

* **Solflare Mobile (iOS and Android)**: Push notifications will appear on the user’s mobile device.
* **Solflare Web**: Notifications will appear in the browser.
* **Solflare Extension**: Notifications will be shown on the Solflare extension if the user has it installed.

#### **How It Works**

This is a **no-code** integration, so your app just needs to use a wallet connector, like the **Solana Wallet Adapter**. With this in place, you can start sending notifications to users through Solflare Wallet without writing any complex backend code.

#### **Integration Steps**

Here’s how you can integrate Solflare notifications into your app.

**1. Set Up Wallet Connection**

To send notifications, your app first needs to establish a wallet connection. Solflare supports various wallet connectors, like **Solana Wallet Adapter**.

Below is an example of how to integrate a basic wallet connection using **Solana Wallet Adapter** in your React app:

```javascript
import React, { useState, useEffect } from 'react';
import { useWallet, WalletProvider } from '@solana/wallet-adapter-react';
import { Connection, PublicKey } from '@solana/web3.js';

const WalletConnection = () => {
  const [connected, setConnected] = useState(false);
  const { wallet, connect, disconnect, publicKey } = useWallet();

  useEffect(() => {
    if (wallet && publicKey) {
      setConnected(true);
    }
  }, [wallet, publicKey]);

  return (
    <div>
      <button onClick={() => connect()} disabled={connected}>
        {connected ? 'Wallet Connected' : 'Connect Wallet'}
      </button>
      <button onClick={() => disconnect()} disabled={!connected}>
        Disconnect Wallet
      </button>
    </div>
  );
};

export default function App() {
  return (
    <WalletProvider>
      <WalletConnection />
    </WalletProvider>
  );
}
```

**2. Send a Notification**

Once the wallet connection is set up, you can send notifications. Below is an example of sending a notification to a user.

The notification will be pushed directly to the user’s **Solflare Wallet Notification Center**.

```javascript
import { sendNotification } from '@solflare-wallet/notifications'; // Import the notification function

const sendUserNotification = async () => {
  // Check if the wallet is connected
  if (!wallet || !publicKey) {
    console.log('Please connect your wallet.');
    return;
  }

  // Define the notification parameters
  const notification = {
    title: "Important Update!",
    message: "You have a new message in your account.",
    recipient: publicKey.toString(), // The wallet address of the user
    type: "app_specific", // Can be "app_specific", "protocol_update", or "general"
  };

  try {
    // Send the notification
    await sendNotification(notification);
    console.log("Notification sent successfully.");
  } catch (error) {
    console.error("Error sending notification:", error);
  }
};
```

**3. Example Button to Trigger Notification**

Here’s how you could create a button that triggers a notification to the user:

```javascript
import React from 'react';

function SendNotificationButton() {
  return (
    <div>
      <button onClick={sendUserNotification}>Send Notification</button>
    </div>
  );
}

export default SendNotificationButton;
```

When a user clicks this button, the notification will be sent to their Solflare Wallet Notification Center.

#### **Benefits of Solflare Notification System**

* **No-Code Integration**: You don’t need to worry about complex backend logic or setting up complicated push notification servers.
* **Cross-Platform Support**: Notifications will be sent to all devices where the user has set up Solflare, whether it's mobile, web, or extension.
* **Universal Access**: Users will see the same notifications across different platforms, ensuring they don't miss important updates.

#### **Summary**

1. **Set up a wallet connection**: Using a wallet adapter like **Solana Wallet Adapter**.
2. **Send notifications**: Use the Solflare notification API to send messages directly to the user’s notification center.
3. **Cross-platform delivery**: Solflare supports notifications on mobile (iOS/Android), web, and extension.
4. **No backend required**: The solution is plug-and-play, with no backend setup necessary for sending notifications.
