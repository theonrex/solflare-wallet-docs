# Other Methods

#### **Solflare Deeplinks: Opening Web Apps in In-App Browser**

Solflare supports deeplinks that allow users to open web apps within Solflare's in-app browser, providing a seamless user experience. These deeplinks can be accessed before a Connect event occurs, as they don't require a session parameter.

***

#### **How It Works**

* **Deeplinks** allow users to easily open web apps directly within Solflare's in-app browser.
* Users can scan a QR code with their mobile device to open a specific page.
* If the web app detects a mobile device, it can prompt users to open the page directly in the Solflare in-app browser.

> **Note:** The browse deeplink is not meant to be pasted into a mobile web browser. It should either be handled by an app or clicked by an end user.

***

#### **Base URL**

```http
https://solflare.com/ul/browse/?ref=
```

***

#### **Query String Parameters**

| **Parameter** | **Required** | **Description**                                                          |
| ------------- | ------------ | ------------------------------------------------------------------------ |
| **`url`**     | Yes          | The URL that should be opened in Solflare's in-app browser, URL-encoded. |
| **`ref`**     | Yes          | The URL of the requesting app, URL-encoded.                              |

***

#### **Example**

For a practical implementation of the `browse` method, refer to the demo application.
