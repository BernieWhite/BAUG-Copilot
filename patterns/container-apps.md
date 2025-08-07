---
description: |
  Describes the deployment and security best practices for container-based applications using Azure Container Apps.
  It includes architecture guidelines, security best practices, and an example Bicep template.
---

# Container-based applications

When deploying container-based applications, Azure Container Apps is the preferred service.
Additionally, the following services are commonly used in conjunction with Container Apps:

- Azure Container Registry (ACR) for storing container images.
- Azure Key Vault for managing secrets and certificates, **if required**.
- Azure Monitor and Log Analytics for monitoring and logging.
- Front Door for global HTTP load balancing and TLS termination, if needed.

## Architecture guidelines

- To access any other Azure services including Key Vault, use a user-assigned managed identity for the Container App.
- Ingress should always be restricted to internal only.
- Enable HTTPS: Use TLS for all communications. Leverage Azure Front Door for SSL termination.
- Monitor and Audit: Enable diagnostics, logging, and Azure Monitor for auditing and alerting.
- Network Security: Use private endpoints and network security groups (NSGs) to restrict traffic.
- Image Scanning: Use Microsoft Defender for Cloud to scan container images for vulnerabilities.
- Applications should avoid using secret references in the Container App configuration and prefer to call Key Vault from application code instead.
- We use Azure Verified Modules (AVM) for deploying Container Apps and App Environments in our environment.

## Example: Secure Container App Deployment using AVM

```bicep
// An example App Environment configured with a consumption workload profile.
module containerEnv 'br/public:avm/res/app/managed-environment:0.11.2' = {
  params: {
    name: envName
    appLogsConfiguration: {
      destination: 'log-analytics'
      logAnalyticsConfiguration: {
        customerId: workspace.properties.customerId
        sharedKey: workspace.listKeys().primarySharedKey
      }
    }
    managedIdentities: {
      systemAssigned: true
    }
    location: location
    infrastructureSubnetResourceId: subnetId
    internal: true
    zoneRedundant: true
    workloadProfiles: [
      {
        name: 'Consumption'
        workloadProfileType: 'Consumption'
      }
    ]
  }
}

// An example Container App using a minimum of 2 replicas.
module containerApp 'br/public:avm/res/app/container-app:0.18.1' = {
  params: {
    name: appName
    environmentResourceId: containerEnv.outputs.resourceId
    containers: containers
    ipSecurityRestrictions: ipSecurityRestrictions
    scaleSettings: {
      minReplicas: 2
      maxReplicas: 5
      rules: [
        {
          name: 'http-rule'
          type: 'http'
          metadata: {
            concurrentRequests: '50'
          }
        }
      ]
    }
  }
}
```
