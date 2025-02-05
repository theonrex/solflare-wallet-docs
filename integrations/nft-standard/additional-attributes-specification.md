# Additional Attributes Specification

Solflare integrates new fields that provide more flexibility when describing attributes in assets. These fields are optional but can enhance the visual representation of assets.

**New Fields for Attributes:**

1. **`display_type`:**
   * **Example Value**: `"Date"`
   * **Description**: Displays the attribute value as a date, using a Unix timestamp to specify it.
2. **`max_value`:**
   * **Example Value**: `Number`
   * **Description**: If the value is a number, it will be displayed as a bar chart with the specified maximum value.
3. **`trait_count`:**
   * **Example Value**: `Number`
   * **Description**: Represents the total count of other assets in the collection with the same trait type and value.

**Mandatory Fields:**

* **`trait_type`** and **`trait_value`** are the only required fields to describe an attribute.
