# CDN hosted files

### **Understanding NFT Metadata with Multimedia Files**

When creating NFTs that include multimedia files (such as videos, images, or audio), the metadata can include a **`files`** field within the **`properties`** section. This allows you to store links to the media associated with the NFT. Here’s an example:

```json
"properties": {
  "files": [
    {
      "uri": "https://watch.videodelivery.net/52a52c4a261c88f19d267931426c9be6",
      "type": "unknown",
      "cdn": true
    }
  ]
}
```

Let’s break this down:

1. **`properties`**: This field is used for storing additional attributes and metadata related to the NFT that are not essential for identification but improve the overall experience. It can include multimedia content, among other things.
2. **`files`**: This is an array where you can store one or more multimedia files linked to the NFT. Each file has its own set of attributes, such as the **`uri`**, **`type`**, and **`cdn`** flag.
3. **File Object**:
   * **`uri`**: The URL that points directly to the file. In this case, it's a video hosted on a video delivery network.
   * **`type`**: Specifies the type of the file. Although marked as `"unknown"` in this example, it typically defines the file type (video, audio, 3D model, etc.).
   * **`cdn`**: A boolean flag indicating whether the file is hosted on a **Content Delivery Network (CDN)**. When set to `true`, it prioritizes this file as the main option for display or playback. The use of a CDN ensures faster loading times as content is served from multiple locations worldwide.

### **Why Use CDN Hosting?**

By marking the multimedia file with the `cdn: true` flag, the app ensures that the file will load quickly from a CDN, improving the user's experience with faster load times.

* **Primary Option for Multimedia**: If this flag exists, the CDN-hosted file is selected as the **primary option** for multimedia attachments (video, audio, or 3D) to be displayed to the NFT owners. This ensures a seamless viewing experience.
* **Fallback if Unavailable**: If the CDN-hosted file is no longer available, Solflare will default to using the URL specified in the **`animation_url`** field as a backup. This ensures that the multimedia content remains accessible, even if the primary CDN file becomes unavailable.

This setup allows NFT creators to offer a seamless and high-performance multimedia experience for users, ensuring the content is delivered efficiently and reliably.
