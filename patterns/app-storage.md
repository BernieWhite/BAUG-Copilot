---
description: |
    Describes deployment and security best practices for deploying blob or general-purpose storage for applications.
    The pattern is applicable for applications that need to store files or blobs.
---

# Application storage

When deploying storage for applications, the following guidelines should be followed:

- Storage accounts must never be publicly accessible, any access to a storage account must be done through a private endpoint.
- An existing Bicep module for storage accounts in the `nnn.azurecr.io` container registry should be used.

## Bicep example

```bicep
module app_storage 'br:nnn.azurecr.io/modules/storage:v2' = {
  params: {
    name: name
    location: location
    blobSoftDeleteDays: 30
    containerSoftDeleteDays: 30
    containers: [
      {
        name: 'backups'
        publicAccess: 'None'
        metadata: {}
      }
      {
        name: 'logs'
      }
    ]
  }
}
```
