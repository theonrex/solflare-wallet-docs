# URI JSON Schema

### **Displaying Off-Chain Metadata for SPL Tokens**

In Solflare, displaying off-chain metadata for SPL tokens requires including a **`uri`** in the on-chain struct. This **`uri`** points to a JSON file containing the metadata of the NFT or token, which Solflare will use to display the relevant information. This structure follows the **Metaplex Developer Guide** and **OpenSea NFT Standard**, allowing for rich metadata displays for your NFTs.

**JSON Structure for Off-Chain Metadata**

Here is an example of how you can structure the metadata JSON file for your SPL token:

```json
{
  "name": "Solflare X NFT",
  "symbol": "",
  "description": "Celebratory Solflare NFT for the Solflare X launch",
  "seller_fee_basis_points": 0,
  "image": "https://www.arweave.net/abcd5678?ext=png",
  "animation_url": "https://www.arweave.net/efgh1234?ext=mp4",
  "external_url": "https://solflare.com",
  "attributes": [
    {
      "trait_type": "web",
      "value": "yes"
    },
    {
      "trait_type": "mobile",
      "value": "yes"
    },
    {
      "trait_type": "extension",
      "value": "yes"
    }
  ],
  "collection": {
     "name": "Solflare X NFT",
     "family": "Solflare" 
  },
  "properties": {
    "files": [
      {
        "uri": "https://www.arweave.net/abcd5678?ext=png",
        "type": "image/png"
      },
      {
        "uri": "https://watch.videodelivery.net/9876jkl",
        "type": "unknown",
        "cdn": true
      },
      {
        "uri": "https://www.arweave.net/efgh1234?ext=mp4",
        "type": "video/mp4"
      }
    ],
    "category": "video",
    "creators": [
      {
        "address": "SOLFLR15asd9d21325bsadythp547912501b",
        "share": 100
      }
    ]
  }
}
```

**Explanation of Fields:**

* **`name`**: The name of the NFT.
* **`symbol`**: A symbol representing the token, often left empty for individual NFTs.
* **`description`**: A human-readable description of the asset.
* **`image`**: The URL to the image of the NFT. Solflare supports PNG, GIF, and JPG file formats, and you may specify the file type using the `?ext={file_extension}` query.
* **`animation_url`**: URL to a multimedia attachment such as video or audio (e.g., MP4, MOV, MP3, FLAC). This field supports different formats for various types of media, including videos, audio files, and 3D/AR assets.
* **`external_url`**: A link to an external website or application where the asset can also be viewed or interacted with.

**Properties:**

* **`category`**: Defines the category of the asset, such as:
  * `"image"` for PNG, GIF, or JPG files.
  * `"video"` for MP4 or MOV files.
  * `"audio"` for MP3, FLAC, or WAV files.
  * `"vr"` for 3D models (GLB, GLTF).
* **`files`**: An array that includes various files associated with the asset, such as images or videos. The **`type`** field matches the file extension (e.g., `image/png`, `video/mp4`). Additionally, files marked with **`cdn: true`** are given priority for selection, typically for faster loading via a Content Delivery Network (CDN).
* **`attributes`**: This array defines the traits or attributes of the asset. Each object in this array includes a **`trait_type`** and **`value`**, where the value can be either a string or a number. For example:
  * **`"trait_type": "web"**, **`"value": "yes"\`**: Indicates that the NFT is compatible with web browsers.
* **`collection`**: If your NFTs belong to a series or family of assets, you can include a **`collection`** field, which contains:
  * **`name`**: The name of the specific collection.
  * **`family`**: The broader category or theme under which the collection falls, such as `"Solflare"`.

**Priority of On-Chain Metadata:**

For fields that match on-chain metadata, the on-chain information will always take priority over the off-chain metadata. This ensures consistency and ensures that the most accurate data is displayed to the user.

By structuring the metadata this way, Solflare can display rich, interactive content for NFTs and SPL tokens, offering users an engaging and informative experience.
