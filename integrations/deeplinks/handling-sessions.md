# Handling Sessions

When a user first connects to Solflare, Solflare returns a session param that represents the user's connection. On all subsequent Provider Methods, the app should pass this `session` parameter back to Solflare. The app is responsible for storing this session.

Sessions do not expire. Once a user has connected with Solflare, the corresponding app can make requests like SignAndSendTransaction and SignMessage indefinitely without prompting the user to reconnect with Solflare. Apps will still need to reconnect to Solflare after a Disconnect event or an Invalid Session.

### Session Structure <a href="#session-structure" id="session-structure"></a>

The entire `session` param is encoded in base58. A `session` should contain the following data:

* **JSON Data Signature**: A base58 signature of the JSON data that is 64 bytes. Solflare will check the signature against the actual message that was signed.
* **JSON Data**: A JSON object with the following fields:
  * `app_url` (string): A URL used to fetch app metadata (i.e. title, icon).
  * `timestamp` (number): The timestamp at which the user approved the connection. At the time of this writing, sessions do not expire.
  * `chain` (string): The chain that the user connected to at the start of the session. Sessions cannot be used across two different chains with the same keypair (e.g. the user cannot connect to Solana and then sign on Ethereum). At the time of this writing, Solflare only supports `solana`.
  * `cluster` (string) (optional): The approved cluster that the app and user initially connected to. Solana-only. Can be either: `mainnet-beta`, `testnet`, or `devnet`. Defaults to `mainnet-beta`.

### Decoding Sessions <a href="#decoding-sessions" id="decoding-sessions"></a>

Solflare will decode and validate the `session` param on every request. To decode the session, we decode it with `bs58`, slice off the first 64 bytes of the signature, and treat the rest as JSON data.

We then sign the JSON data again with the same key pair and compare that signature against the signature in the session. If the signatures are the same, the session is valid. Otherwise, we conclude that the session has been faked, as the signature does not belong to the keypair it claims it does.

Calling `nacl.sign.open`conveniently verifies and returns the original object. For more information, please review [Encryption Resources](https://docs.solflare.com/solflare/technical/deeplinks/encryption#encryption-resources).

After we determine that the session is valid, we still need to ensure that the JSON fields line up with what we expect. An app could give a session for `pubkey A` when the user is currently using `pubkey B` in Solflare.

In such a scenario, that session should not allow an app to request signatures. Instead, the app must issue a new connect request or use the correct session.

```javascript
// Encoding a session
const privateKey = ...;
const sessionData = JSON.stringify({
  "app_id": "APP_ID",
  "chain": "CHAIN",
  "cluster": "CLUSTER",
  "timestamp": 1644954984,
});
const bytes = Buffer.from(sessionData, "utf-8");

// tweetnacl-js formats signature in format <signature><sessionData>
const signature = bs58.encode(nacl.sign(bytes, privateKey));

// Decoding ja session
const publicKey = ...;
const verifiedSessionData = nacl.sign.open(bs58.decode(signature), publicKey.toBytes());
if (!verifiedSessionData) throw new Error(`This session was not signed by ${publicKey}`);
```

#### Invalid Sessions <a href="#invalid-sessions" id="invalid-sessions"></a>

While sessions do not expire, there are a number of reasons why sessions could still be deemed invalid:

1. It was not signed by the current wallet key pair. This could mean that the session is entirely fake, or that it was signed by another keypair in the user’s wallet.
2. It was signed by the current wallet key pair, but the session's JSON `data` does not pass muster. There are a few reasons why this might occur:
   1. The user switched chains (or possibly networks).
   2. The `app_url` could be blocked if malicious. See the [Blocklist](https://github.com/phantom-labs/blocklist) for more information.
