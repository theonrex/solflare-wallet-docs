# NFT Standard

### **Solflare NFT Standard and General Metadata Recommendations v1**

Solflare fully supports displaying metadata associated with **SPL tokens** by adhering to the **Metaplex Token Metadata contract** standards. The wallet pulls both on-chain data and the external **JSON** provided by the **`uri`** field to display all relevant data about the asset. Solflare encourages following the **Metaplex standards** and the additional guidelines outlined here to ensure proper display and full functionality for NFTs within the wallet.

### **Key Fields in the Token Metadata Program**

The following fields are part of the **Token Metadata Program** as described in the Metaplex standards. These fields are used by Solflare to display NFT information and are crucial for ensuring correct functionality.

| **Field**                      | **Type** | **Description**                                                                                    | **Displayed**                                                                                       |
| ------------------------------ | -------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **name**                       | string   | Name of the asset                                                                                  | Grid view and single NFT view.                                                                      |
| **symbol**                     | string   | Symbol representing the asset                                                                      | Not shown currently.                                                                                |
| **uri**                        | string   | URI to the external JSON representing the asset. This is linked to display the off-chain metadata. | Linked in the single NFT view.                                                                      |
| **creators**                   | array    | Public key of each creator associated with the NFT.                                                | Shown in the single NFT view, resolved to Twitter handles if connected via **Solana Name Service**. |
| **update\_authority**          | string   | Public key of the metadata owner (the update authority).                                           | Shown in the single NFT view, can be updated in the send NFT modal.                                 |
| **primary\_sale\_happened**    | boolean  | A flag that indicates whether the primary sale of the token has occurred.                          | Visible in the send NFT modal, can be updated.                                                      |
| **seller\_fee\_basis\_points** | number   | The royalties percentage that will be awarded to the creators when the token is resold.            | Shown as a percentage received by each co-creator.                                                  |

### **Master Editions and Editions**

In addition to the core fields, the **Metaplex Token Metadata** program includes **optional structs** for creating **Master Editions** and **Editions**. If these accounts exist, Solflare will:

* Display the **Edition number** for unique edition tokens.
* Indicate if the token is a **Master Edition**.

### **Why These Standards Matter**

By adhering to the **Metaplex Token Metadata** contract, creators can ensure that their NFTs are displayed correctly in **Solflare wallets** and can fully utilize Solflare's NFT-related functionalities. This includes proper display of creator information, royalties, and editions, which enhances the user experience and ensures the value of the token is recognized and properly tracked.

**Explore More**

You can explore the **Metaplex project** in more detail through their official developer guide. This guide provides a comprehensive breakdown of the metadata structure, how to implement it, and best practices for ensuring your NFTs conform to the standards.
