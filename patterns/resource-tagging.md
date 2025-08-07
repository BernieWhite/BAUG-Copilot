---
description: |
  Describes the tagging and naming strategy for all resource groups and resources/ infrastructure/ applications in Azure.
  It includes requirements and Bicep examples.
---

# Naming and tagging

## Resource group tagging

Resource groups in Azure must be tagged, other resource types are not tagged.
The following tags are required for all resource groups:

- `env`: The environment the resource group is deployed into, such as `dev`, `test`, or `prod`.
- `costCenter`: The cost center or department responsible for the resource group. This is a six digit number, such as `123456`.

Resource groups that relate to applications must also be tagged with the following tags:

- `app`: The name of the application or service the resource group supports.

Resource groups that relate to infrastructure must also be tagged with the following tags:

- `serviceGroup`: The name of the service group the resource group supports, such as `networking`, `identity`, or `storage`.

## Resource naming

All resources and resource groups in Azure must be named with lowercase using the following standard formats:

- Resource groups: `rg-{environment}-{app}-{suffix}-{number}`
- Storage Account: `st-{environment}-{app}-{suffix}-{number}`
- Virtual Network: `vnet-{environment}-{zone}-{suffix}-{number}`
- Virtual Network Subnet: `snet-{environment}-{zone}-{suffix}-{number}`
- Container Apps: `ca-{environment}-{app}-{suffix}-{number}`
- Key Vault: `v-{environment}-{app}-{suffix}-{number}`

Where:

- {environment} is the environment identifier (e.g., `dev`, `test`, `prod`).
- {zone} is the security zone (e.g. `public`, `private`, `restricted`).
