# Browse

#### **Solflare Deeplinks: Open Web Apps in In-App Browser**

Solflare provides deeplinks that allow users to open web apps directly within its in-app browser. Users can scan a QR code or be prompted by a mobile web app to open a page within the Solflare app.

***

#### **Key Features**

* **Scan QR Code**: Users can scan a QR code with their phone's camera to open a page directly within Solflare’s in-app browser.
* **Device Detection**: Web apps can detect if a user is on a mobile device and prompt them to open the page in Solflare's in-app browser.
* **No Session Param Needed**: The `browse` deeplink can be used before a Connect event since it does not require a session parameter.

> **Note**: These deeplinks are not intended to be pasted directly into mobile web browsers. They must be handled by an app or clicked by the end user.

***

#### **Base URL**

```plaintext
 https://solflare.com/ul/v1/browse/<url>?ref=<ref>
```

***

#### **Query String Parameters**

| **Parameter** | **Required** | **Description**                                                         |
| ------------- | ------------ | ----------------------------------------------------------------------- |
| **`url`**     | Yes          | The URL that should open within Solflare's in-app browser, URL-encoded. |
| **`ref`**     | Yes          | The URL of the requesting app, URL-encoded.                             |

***

#### **Example**

For a working implementation, refer to the demo application
