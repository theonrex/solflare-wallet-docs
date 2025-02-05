# Get a Wallet's Profile Picture

### **Fetching Wallet Profile Picture for Your Protocol**

To enhance your user interface, you can fetch a wallet's profile picture and display it on your protocol's front-end using the functionality provided below.

#### **Function: `getProfilePicture`**

The `getProfilePicture` function allows you to fetch the profile picture associated with a specific wallet. It can return a fallback image if no profile picture exists, and it provides additional metadata about the wallet's NFT profile picture.

#### **Function Signature**

{% code overflow="wrap" %}
```typescript
function getProfilePicture(connection: Connection, publicKey: PublicKey, config?: ProfilePictureConfig): Promise<ProfilePicture>;
```
{% endcode %}

#### **Parameters**

* **connection** (`Connection`):\
  The RPC connection object to the Solana network. This is used to interact with the blockchain.
* **publicKey** (`PublicKey`):\
  The public key of the wallet whose profile picture you want to fetch.
*   **config** (`ProfilePictureConfig`, optional):\
    Configuration options to customize the profile picture retrieval.

    * **fallback** (`boolean`, default `true`):\
      Whether to use a fallback generated image when no profile picture is set.
    * **resize** (`object`, default `{ width: 100 }`):\
      The image resizing parameters, such as the width of the image. You can customize it to adjust the image size.

    **Example**:

    ```javascript
    const config = {
      fallback: true,
      resize: { width: 200 },
    };
    ```

#### **Return Value**

The `getProfilePicture` function returns an object with the following fields:

* **isAvailable** (`boolean`):\
  `true` if a profile picture exists for the given wallet; otherwise, `false`.
* **url** (`string`):\
  The URL of the profile image. This will always be populated, either as a fallback image or an empty-image icon.
  * If `isAvailable` is `false`, you can still use this URL, which will point to the fallback or placeholder image.
* **name** (`string`, optional):\
  The name of the NFT used as the profile picture (only present if `isAvailable` is `true`).
* **metadata** (`object`, optional):\
  Metadata about the NFT used as the profile picture (only present if `isAvailable` is `true`).
* **tokenAccount** (`PublicKey`, optional):\
  The public key of the token account that holds the NFT (only present if `isAvailable` is `true`).
* **mintAccount** (`PublicKey`, optional):\
  The public key of the NFT's mint (only present if `isAvailable` is `true`).

#### **Example Usage**

```javascript
import { Connection, PublicKey } from '@solana/web3.js';
import { getProfilePicture } from '@solflare-wallet/pfp';

const connection = new Connection('https://api.mainnet-beta.solana.com');
const walletPubkey = new PublicKey('ES8rZr16f5eAc9PkUcAbafwg5JjEJANbpwu92CF2Cbox'); // Replace with the wallet address

const config = {
  fallback: true,
  resize: { width: 150 }
};

async function fetchProfilePicture() {
  try {
    const { isAvailable, url, name, metadata, tokenAccount, mintAccount } = await getProfilePicture(connection, walletPubkey, config);

    if (isAvailable) {
      console.log('Profile Picture URL:', url);
      console.log('NFT Name:', name);
      console.log('Metadata:', metadata);
      console.log('Token Account:', tokenAccount.toString());
      console.log('Mint Account:', mintAccount.toString());
    } else {
      console.log('No profile picture available for this wallet.');
    }
  } catch (error) {
    console.error('Error fetching profile picture:', error);
  }
}

fetchProfilePicture();
```

***

### **Summary**

* **`isAvailable`** tells you if the wallet has a profile picture.
* **`url`** gives you the link to the profile image.
* **`name`, `metadata`, `tokenAccount`, and `mintAccount`** provide detailed NFT-related data if the wallet has an NFT set as its profile picture.

This feature allows you to seamlessly integrate user profile pictures into your Solana application, enhancing personalization and user experience.
