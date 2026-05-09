# xrMCP Registry

The official registry of xrMCP tool manifests. Each tool is a single `.xrmcp.json` file that describes an API — its inputs, outputs, authentication, and how to map the response.

## Browse tools

| Category | Tool | Description |
|---|---|---|
| jira | `get_jira_ticket` | Fetch a Jira issue by key |
| jira | `comment_jira_ticket` | Add a plain text comment to a Jira issue |
| jira | `get_jira_ticket_comment` | Fetch the most recent comments for a Jira issue |
| jira | `get_jira_ticket_history` | Fetch the change history of a Jira issue |
| gitlab | `list_project` | List projects in a GitLab group |
| jsonph | `get_post` | Fetch a post from JSONPlaceholder by id |
| jsonph | `list_posts` | List posts from JSONPlaceholder |

## Install a tool

Using the [xrMCP CLI](https://github.com/xrmcp/cli):

```sh
xrmcp tool install jira/get_jira_ticket
```

Or directly with curl:

```sh
curl -X POST http://localhost:7373/tools/register \
  -H 'content-type: application/json' \
  -d @- <<< $(curl -fsSL https://raw.githubusercontent.com/xrmcp/registry/main/xrmcp-registry/tools/jira/get_jira_ticket.xrmcp.json)
```

## Structure

```
xrmcp-registry/tools/
├── metadata.json          # searchable index of all tools
├── jira/
├── gitlab/
└── jsonph/
```

`metadata.json` is used by the CLI for `xrmcp tool search <keyword>` — it is fetched once and searched locally without downloading every manifest.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md).
