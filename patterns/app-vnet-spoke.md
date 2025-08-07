---
description: |
  Describes the network configuration for subnets used by applications.
---

# Application network spoke

Applications are placed in a landing zone to based on their requirements isolate them from other applications and services.
For security, each application is deployed into a separate subnet.

The guidelines apply to any new applications:

- Applications should start with a `/25` subnet that are allocated centrally before use in the `10.100.0.0/16` range.
- Network security groups (NSGs) should be used to restrict access to the application, and must be applied to the subnet.
- The NSG should be configured to allow only the minimal required inbound traffic to the application.

## Management traffic

The following management traffic must be allowed for any application NSGs:

- Allow inbound traffic from the Azure Bastion subnet to the application subnet on port `22` for SSH and `3389` for RDP.
- The Azure Bastion subnet is `10.55.0.0/24`.
