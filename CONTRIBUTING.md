# Contributing to the xrMCP Registry

Thanks for contributing a tool manifest. Here's how to do it correctly.

## Requirements

- The tool must call a **public or self-hosted API** accessible over HTTP/HTTPS.
- The manifest must validate against the [`ToolRegistration`](https://github.com/xrmcp/xrmcp/blob/main/specification/v0.1.0/schema.json#/$defs/ToolRegistration) definition in the xrMCP v0.1.0 schema.
- Credentials must use `{{secrets.*}}` — never hardcode tokens or passwords.
- The tool must be **generic enough** to be useful to others (no personal domains, no org-specific endpoints hardcoded).

## Steps

### 1. Create the manifest

Place your file under `xrmcp-registry/tools/<category>/<tool_name>.xrmcp.json`.

Use an existing tool as a reference, e.g. [`xrmcp-registry/tools/jira/get_jira_ticket.xrmcp.json`](./xrmcp-registry/tools/jira/get_jira_ticket.xrmcp.json).

Naming rules:
- `<category>` — lowercase, matches the service name (e.g. `jira`, `gitlab`, `github`)
- `<tool_name>` — snake_case verb + noun (e.g. `get_issue`, `list_projects`, `create_comment`)

### 2. Update metadata.json

Add an entry to `xrmcp-registry/tools/metadata.json` in the `tools` array:

```json
{
  "name": "your_tool_name",
  "displayName": "Human Readable Name",
  "description": "One sentence describing what the tool does.",
  "tags": ["relevant", "keywords"],
  "path": "<category>/<tool_name>.xrmcp.json"
}
```

### 3. Test locally

Start an xrMCP server and register your tool:

```sh
xrmcp server start -t http
xrmcp tool install xrmcp-registry/tools/<category>/<tool_name>.xrmcp.json
```

Invoke it via the MCP Inspector:

1. Start the MCP Inspector:
   ```sh
   npx @modelcontextprotocol/inspector
   ```
2. Open [http://localhost:6274](http://localhost:6274) in your browser.
3. Set **Transport** to `Streamable HTTP` and **URL** to `http://localhost:7373/mcp`, then click **Connect**.
4. Go to the **Tools** tab — your tool should appear in the list.
5. Select it, fill in the input fields, and click **Run Tool** to verify the response is correct.

### 4. Open a pull request

- Title: `feat(<category>): add <tool_name>`
- Include a short description of the API being wrapped and what the tool returns.

## Checklist

- [ ] `schemaVersion` is `xrmcp.v0.1.0`
- [ ] No hardcoded credentials or personal domains
- [ ] Auth uses `{{secrets.*}}`
- [ ] `permissions.network` lists the correct host(s)
- [ ] `permissions.secrets` lists every secret referenced
- [ ] Entry added to `xrmcp-registry/tools/metadata.json`
- [ ] Tool tested against a running xrMCP server
