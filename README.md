# Accelerating Infrastructure as Code development with MCP and Bicep

This is a source sample repository for a MCP Presentation presented at the Brisbane Azure User Group on 2025-08-06.

> [!NOTE]
> The command `ps-rule-azure` is the result of personal experimentation, and is not available publicly at the time of writing.
> For more information on PSRule for Azure, please refer to the [aka.ms/ps-rule-azure](https://aka.ms/ps-rule-azure) documentation.

## 1 - Copilot orientation

- Getting chat up.
- Choosing modes and model.
- Showing tools.

## 2 - MCP

See the list of published MCP servers from Visual Studio Code documentation here: https://code.visualstudio.com/mcp

Showing request/ response from stdout:

```json-rpc
{  "jsonrpc": "2.0",  "id": 1,  "method": "tools/list",  "params": {  }}
```

## 3 - Creating a storage account

```prompt
Can you create a module for a storage account.
```

## 4 - Creating a container app

```prompt
create an application deployment for a container app that uses a storage account. the application is called shopfront.
```

```prompt
can you please create a bicep deployment for a new web application called storefront that will use containers.
```

## Patterns

Patterns are stored in the `patterns/` directory.

Publishing new patterns to the registry:

```shell
ps-rule-azure pattern publish --registry nnn.azurecr.io --name patterns/container-app --version 1.0.0 -f patterns/container-apps.md

ps-rule-azure pattern publish --registry nnn.azurecr.io --name patterns/container-app --version 1.0.0 -f patterns/container-apps.md

ps-rule-azure pattern publish --registry nnn.azurecr.io --name patterns/container-app --version 1.0.0 -f patterns/container-apps.md

ps-rule-azure pattern publish --registry nnn.azurecr.io --name patterns/container-app --version 1.0.0 -f patterns/container-apps.md
```

Listing and importing patterns from the registry:

```shell
ps-rule-azure pattern list --registry nnn.azurecr.io --prefix patterns/
```

```shell
ps-rule-azure pattern import --registry nnn.azurecr.io --prefix patterns/
```

## References

- https://modelcontextprotocol.io/clients
- https://code.visualstudio.com/docs/copilot/copilot-customization#_custom-instructions
- https://code.visualstudio.com/docs/setup/enterprise#_centrally-manage-vs-code-settings
