# Keycloak MCP Server (TypeScript)

A Model Context Protocol (MCP) server built with TypeScript that enables AI assistants (such as Claude Desktop, Cursor, and Goose) to interact with and manage a **Keycloak** instance using natural language.

Built on the official `@modelcontextprotocol/server` SDK and `@keycloak/keycloak-admin-client`.

## ✨ Features
- **User Management:** Search, list, and create users in your target realm.
- **Least-Privilege Security:** Authenticates via OAuth2 `client_credentials` using a dedicated Keycloak service account rather than master admin credentials.
- **Type-Safe Validation:** Strict input validation powered by `zod`.

## 📋 Prerequisites
- **Node.js** v20 or higher
- A running **Keycloak** server
- A dedicated **Keycloak Service Account Client** with `realm-management` roles (e.g., `view-users`, `manage-users`)

## 🚀 Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd keycloak-mcp
   ```

2. **Install dependencies and build:**
   ```bash
   npm install
   npm run build
   ```

## ⚙️ Configuration

### 1. Keycloak Client Setup
1. Open the **Keycloak Admin Console** and select your target realm.
2. Navigate to **Clients** > **Create client** (e.g., `mcp-admin-bot`).
3. Enable **Client authentication** and **Service accounts roles**, then save.
4. Copy the secret from the **Credentials** tab.
5. Assign the required roles under the **Service accounts roles** tab (`Filter by clients` -> `realm-management`).

### 2. MCP Client Configuration
Add the server to your MCP client configuration (e.g., `claude_desktop_config.json` or `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "keycloak": {
      "command": "node",
      "args": ["/absolute/path/to/keycloak-mcp/build/index.js"],
      "env": {
        "KEYCLOAK_URL": "http://localhost:8080",
        "KEYCLOAK_REALM": "your-realm",
        "KEYCLOAK_CLIENT_ID": "mcp-admin-bot",
        "KEYCLOAK_CLIENT_SECRET": "your-client-secret"
      }
    }
  }
}
```

## 🛠️ Available Tools

| Tool Name | Description |
| :--- | :--- |
| `list-users` | Search and list users by username, email, or name. |
| `create-user` | Create a new user in the configured Keycloak realm. |

## 📄 License
MIT
