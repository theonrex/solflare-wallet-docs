# Deeplinks

### **What Are Deeplinks?**

Deeplinks are URLs designed to take users directly to specific features or sections within an app. Instead of simply opening the app's homepage, a deeplink can, for instance, navigate directly to a wallet connection screen or initiate a transaction signing process.

Deeplinks are widely used in mobile applications to improve user experience and enable seamless app-to-app communication. They are essential for integrating third-party apps, such as wallets or payment services, into broader workflows.

### **Solflare Deeplink Integration**

Solflare now enables iOS and Android apps to interact natively with Solflare via **deeplinks**.

In Solflare's case, these deeplinks enable developers to integrate Solflare functionality, such as wallet connection, transaction signing, or account management into their apps, improving the user experience.

***

### **Deeplink Protocol Format**

All Solflare provider methods follow a standardized protocol format:

```http
https://solflare.com/ul/<version>/<method>
```

* **`<version>`**: The API version being used (e.g., `v1`).
* **`<method>`**: The specific action or functionality to invoke, such as connecting a wallet or signing a transaction.

### **Examples**

{% tabs %}
{% tab title="Wallet Connection:" %}
```http
https://solflare.com/ul/v1/connect
```

_**This deeplink initiates a wallet connection workflow.**_
{% endtab %}

{% tab title="Transaction Signing:" %}
```http
https://solflare.com/ul/v1/signTransaction
```

_**This deeplink directs users to sign a transaction within the Solflare app.**_
{% endtab %}
{% endtabs %}

***

### **Why Use Solflare Deeplinks?**

By using the defined protocol format, developers can ensure compatibility and easily extend their app's functionality with Solflare's wallet capabilities.
