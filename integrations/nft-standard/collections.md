# Collections

### **Marking NFTs with a Collection Field in Solflare**

If your NFT belongs to a group or series of unique NFTs, you can associate it with a **collection** using the following structure:

**Example JSON for Collection Field:**

```json
"collection": {   
  "name": "Pigs on Solana Season #1",
  "family": "Pigs on Solana"
}
```

#### **Explanation:**

* **`collection.name`**: Specifies the name of the collection or series to which the NFT belongs.
* **`collection.family`**: Represents the broader set or family the NFT belongs to, especially if you have multiple variations within a theme or project. It must be a unique identifier for your entire project (e.g., "Pigs on Solana" rather than general terms like "art" or "cars").

**Impact:**

Solflare will use this field to group NFTs that belong to the same family and display the collection name when viewing a single NFT.
