
This repository contains Azure infrastructure as code (IaC).
Code is written in Bicep, a domain-specific language (DSL) for deploying Azure resources whenever possible.

# Workspace structure

- Reusable `.bicep` modules should be placed in a subdirectory clearly named and lowercased within the `modules/` directory.
  - The subdirectory should be named after the resource type or functionality, e.g., `storage`, `networking`, etc.
  - Each module should have a descriptive name and include a `README.md` file explaining its purpose and usage.
  - Modules should be a file named `main.bicep`.
  - Tests referencing modules should be placed in a `tests/` subdirectory within the module directory. e.g. `modules/storage/tests/main.test.bicep`.
- Specific deployments for environments or resources should be placed in a subdirectory within the `deployments/` directory.
  - Deployments should be an a file named `deploy.bicep`.

# Bicep code guidelines

When generating or reviewing `.bicep` code use:

- The instructions in `.github/instructions/bicep.instructions.md`.
- Always use internal naming conventions and policies.
- The Bicep linter to ensure code quality and adherence to best practices.
- The tool `get_bicep_boiler_plate` to generate boilerplate code for new Bicep files.
- Use the tool `get_approved_patterns` before suggesting a plan or writing any code, you may need to use more then one pattern.
- The tool `getRecommendation` to get recommendations for Azure resources using Bicep code.
- You can use the command line `bicep list <file>.bicep` to check the file for issues.
- Always correct any syntax errors before completing the task.
