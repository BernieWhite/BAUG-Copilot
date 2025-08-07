---
description: |
  Describes the secure storage of secrets in Azure Key Vault.
  It includes requirements and security guidelines for configuration and an example Bicep template.
---

# Secure storage of secrets

When storing secrets are required, they must be stored in Key Vault.
When configuring Key Vault, the following guidelines should be followed:

- Access to the Key Vault should be limited to specific identities.
- Any application using the Key Vault should use a user-assigned managed identity if possible, otherwise a system-assigned managed identity.
- Access must be granted using RBAC assignments, not using access policies.

This is an Bicep example of a Key Vault using the approved configuration:

```bicep
resource vault 'Microsoft.KeyVault/vaults@2023-07-01' = {
  name: name
  location: location
  properties: {
    sku: {
      family: 'A'
      name: 'premium'
    }
    tenantId: tenant().tenantId
    softDeleteRetentionInDays: 90
    enableSoftDelete: true
    enablePurgeProtection: true
    enableRbacAuthorization: true
    networkAcls: {
      defaultAction: 'Deny'
      bypass: 'None'
    }
  }
}
```
