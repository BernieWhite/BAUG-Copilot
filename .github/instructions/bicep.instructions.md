---
description: Instructions for working with Bicep files in this repository.
applyTo: '**/*.bicep'
---

When generating or reviewing Bicep code, please adhere to the following guidelines:

- Always include the `targetScope` declaration at the top of the file, specifying the scope of the deployment (e.g., `targetScope = 'subscription'` or `targetScope = 'resourceGroup'`).
- Parameters should be defined at the top of the file, immediately after the `targetScope` declaration. Use clear and descriptive names for parameters.
  - Use the `@description` decorator to provide context for each parameter.
  - Each parameter should have one blank line space before it for readability.
  - Always include common parameters such as `location`, `tags`, and `name` for consistency across modules.
- Always correct any syntax errors before completing the task.
