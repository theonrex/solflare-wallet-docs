# Encryption

Deeplinks are encrypted using symmetric key encryption generated from a [Diffie-Hellman key exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange). While deeplink sessions will be created in plaintext, an encrypted channel will be created to prevent session tokens from getting hijacked.

### Encryption & Decryption Workflow <a href="#encryption-and-decryption-workflow" id="encryption-and-decryption-workflow"></a>

Solflare deeplinks are encrypted with the following workflows:

**Connect**

1. \[dapp]: On the initial `connect` deeplink, apps should include a `dapp_encryption_public_key` query parameter. It's recommended to create a new x25519 keypair for every session started with `connect`. In all methods, the public key for this keypair is referred to as `dapp_encryption_public_key`.
2. \[solflare]: Upon handling a `connect` deeplink, Solflare will also generate a new x25519 keypair.
   * Solflare will return this public key as `solflare_encryption_public_key` in the `connect` response.
   * Solflare will create a secret key using Diffie-Hellman with `dapp_encryption_public_key` and the _**private key**_ associated with `solflare_encryption_public_key`.
   * Solflare will locally store a mapping of `dapp_encryption_public_key` to shared secrets for use with decryption in subsequent deeplinks.
3. \[dapp]: Upon receiving the `connect` response, the dapp should create a shared secret by using Diffie-Hellman with `solflare_encryption_public_key` and the _**private key**_ associated with `dapp_encryption_public_key`. This shared secret should then be used to decrypt the `data` field in the response. If done correctly, the user's public key will be available to share with the dapp inside the `data` JSON object.

**Subsequent Deeplinks**

1. \[dapp]: For any subsequent methods (such as [SignAndSendTransaction](https://docs.solflare.com/solflare/technical/deeplinks/provider-methods/signandsendtransaction) and [SignMessage](https://docs.solflare.com/solflare/technical/deeplinks/provider-methods/signmessage)), apps should send a `dapp_encryption_public_key` (the public key side of the shared secret) used with Solflare along with an encrypted `payload` object.
2. \[solflare]: Upon approval, Solflare will encrypt the signed response as a JSON object with the encryption sent as a `data=` query param.
3. \[dapp]: Upon receiving the deeplink response, apps should decrypt the object in the `data=` query param to view the signature.

#### Encryption Resources <a href="#encryption-resources" id="encryption-resources"></a>

To learn more about encryption and decryption, please refer to the following libraries:

**JavaScript:** [TweetNaCl.js](https://github.com/dchest/tweetnacl-js)

**iOS:** [TweetNaCl SwiftWrap](https://github.com/bitmark-inc/tweetnacl-swiftwrap)

**Android:**

* [Tink](https://github.com/google/tink)
* [TweetNaCl Java](https://github.com/InstantWebP2P/tweetnacl-java)
