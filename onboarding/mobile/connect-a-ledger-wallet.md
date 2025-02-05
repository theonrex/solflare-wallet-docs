---
description: Mobile Guide
---

# Connect a Ledger Wallet

This guide shows you how to connect a funded Ledger account to your Solflare wallet. It assumes you already have a wallet setup on a Ledger device and there is a SOL balance on at least one account.

If you haven’t done that yet, you can set up a new wallet using the Ledger Live app by following the steps in [this guide](https://academy.solflare.com/guides/how-to-generate-a-wallet-with-a-ledger-device-using-the-ledger-live-app-mobile/). For this guide, you’ll need to have downloaded Solflare to your mobile device. You can do so at the links below.

{% hint style="info" %}
**Note:** Ensure the Solflare app is downloaded on your mobile device:\
Solflare for [iOS](https://apps.apple.com/us/app/solflare/id1580902717) | Solflare for [Android](https://play.google.com/store/apps/details?id=com.solflare.mobile)
{% endhint %}

### Step 1: Connect Ledger to Solflare Mobile

<figure><img src="../../.gitbook/assets/solfalre ledger.png" alt=""><figcaption></figcaption></figure>

* Open the Solflare mobile app and click the **Ledger button** on the home screen.
* **Allow** Solflare to use your mobile device’s Bluetooth.

<figure><img src="../../.gitbook/assets/solfare ledger 2.png" alt=""><figcaption></figcaption></figure>

* Click **I Paired My Device** once you have done so.
* Then click on the device that you are trying to connect.

### Step 2: Import Accounts from Ledger

<figure><img src="../../.gitbook/assets/solflare ledger 3.png" alt=""><figcaption></figcaption></figure>

As long as you have a funded account on your device, Solflare will automatically detect it.

* Once your accounts appear on the screen, click **Import All**.

Clicking **Import All** will create a new Ledger-controlled account within Solflare.

{% hint style="success" %}
If you wish to utilize the full security advantages that a hardware wallet provides, please be sure to transfer your assets from the mnemonic-based account (the one you have been using up until this point) to the newly created, Ledger-controlled account.
{% endhint %}

### Step 3: Enable Blind Signing on Ledger

In order to interact with SPL tokens and smart contracts, **enable blind signing** by following these quick steps on your device (as per Ledger’s support [article](https://support.ledger.com/hc/en-us/articles/4499092909085-Allowing-blind-signing-in-the-Solana-SOL-app?docs=true)).

1. Connect and unlock your Ledger device.
2. Open the **Solana** application. Your device displays **Application is ready**.
3. Press the right button to navigate to **Settings**. Then press both buttons to validate. Your Ledger device displays **Allow blind sign**.
4. Select **Yes** then press both buttons. Your device displays **Application is ready** again. You’re done.

***

### **Important:**

{% hint style="warning" %}
Blind signing is an advanced feature required for using Solana; it’s recommended to disable it after each use, stay mindful of when it’s enabled, and note that any firmware or Solana app update will automatically turn it off.
{% endhint %}

#### You’re All Set!

If you encounter issues while following this guide:

* Refer to this [guide](https://academy.solflare.com/guides/how-to-generate-a-wallet-with-a-ledger-device-using-the-ledger-live-app-mobile/) to check if your device is configured correctly.
* Still stuck? Contact our **24/7 Support Team** [here](https://solflare.com/support).
