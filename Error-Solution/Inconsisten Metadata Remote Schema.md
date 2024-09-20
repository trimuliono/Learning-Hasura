# Inconsistent Metadata in Remote Schema - Documentation

### Introduction
This documentation addresses the issue of inconsistent metadata when integrating remote schemas in Hasura. Conflicting or inconsistent metadata typically arises when there are naming conflicts between the fields, types, or queries in the remote schema and the Hasura’s native schema. This document also provides a solution to resolve these issues using custom root field namespaces.

## Problem Overview
When integrating remote GraphQL schemas with Hasura, you may encounter `metadata inconsistency` due to:
-  **Naming conflicts** between fields in the remote schema and the native Hasura schema.
-  Conflicts between **multiple remote schemas** that have overlapping or identical root field names.
-  **Type conflicts** where the same type names are present in both local and remote schemas, causing errors in metadata synchronization.

## Solution: Using Custom Root Field Namespace

The recommended solution to resolve metadata inconsistency when dealing with remote schemas is to apply a custom root field namespace. This allows you to avoid naming collisions by isolating the root fields of remote schemas under a unique namespace.

### Steps to Add a Custom Namespace for a Remote Schema

**1. Add or Edit a Remote Schema:**
- Go to Remote Schemas from the sidebar.
- Click Add to create a new remote schema, or select an existing schema to edit.

**2. Configure the Remote Schema:**

- In the configuration form, provide:
  - **Name:** A unique identifier for the remote schema (e.g., cloudhasuratri).
  - **GraphQL** Server URL: The URL of the remote GraphQL API.
  - **Headers:** Any necessary headers (e.g., authorization headers) required by the remote API.

  ![image](https://github.com/user-attachments/assets/6dd63fb1-e2b0-498e-bf4f-9b53bf0603fc)

**3. Apply a Custom Root Field Namespace:**
- In the field labeled Custom Root Field Namespace, enter a unique namespace (e.g., externalAPI).
- This namespace will prefix all root fields from the remote schema, preventing any name collisions with the native Hasura schema or other remote schemas.
- For example, if the remote schema has a field employees, it will now be accessed as cloudhasuratri_employees in Hasura.

![image](https://github.com/user-attachments/assets/d3711c00-07d0-4284-a30a-89bf5bd230f5)

**4. Save the Remote Schema:**
- After configuring the namespace, click Save to apply the changes.
- Hasura will now isolate the remote schema under the custom namespace, preventing any metadata inconsistency issues.

**Example:**

![image](https://github.com/user-attachments/assets/f9f8b375-6724-4f44-8eed-854a73647b57)
