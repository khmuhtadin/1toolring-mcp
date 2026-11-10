# 1ToolRing MCP server

One key and one prepaid balance for the live data AI agents need: Google search results, keyword and SEO data, Google Maps places, e-commerce product prices and exchange rates.

Your agent finds a tool by describing the job, sees the price before it runs anything, and pays per call from your 1ToolRing balance. Failed calls are not charged. There is no subscription.

- Website: https://1toolring.com
- Docs: https://docs.1toolring.com/overview/
- Setup guide for agents: https://1toolring.com/llms.txt
- Status: open. Anyone can sign up, and a new account gets a Rp10.000 starter balance once its email is verified.

This repository holds the public connection details and client configs. The server itself is hosted; there is nothing to run locally.

## Endpoint

| | |
|---|---|
| URL | `https://mcp.1toolring.com/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 (dynamic client registration, PKCE). An API key sent as `Authorization: Bearer <key>` also works. |
| Registry name | `com.1toolring/mcp` ([official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.1toolring)) |

## Tools

| Tool | What it does | Cost |
|---|---|---|
| `discover_tools` | Search the catalog by describing the job in plain words. Returns tool ids, a short description and the price as {usd, idr}. | Free |
| `inspect_tool` | Read one tool's input schema, price model and health before running it. | Free |
| `run_tool` | Run a tool, paid from your prepaid balance. The price is held up front and settled to the real cost; failed runs are not charged. | Per call |
| `get_tool_run` | Fetch the status and output of a slow run started by `run_tool`. | Free |

What the catalog covers today: thousands of tools from third-party providers, across search and SEO, maps and places, e-commerce, market data, web pages, images, video and voice, and more. The full list with prices is at https://1toolring.com/tools/

## Set up

The quickest way: paste this line into your agent's chat (Claude Code, Codex, Cursor, ChatGPT, claude.ai).

```
set up 1ToolRing - https://1toolring.com/llms.txt
```

Or add it by hand:

**Claude Code (plugin, includes the skill)**

```bash
/plugin install 1toolring --marketplace khmuhtadin/1toolring-mcp
```

**Claude Code (MCP server only)**

```bash
claude mcp add --transport http 1toolring https://mcp.1toolring.com/mcp
```

Then run `/mcp`, choose Authenticate and select Allow in your browser.

**Codex**

```bash
codex mcp add 1toolring --url https://mcp.1toolring.com/mcp
codex mcp login 1toolring
```

**Cursor**

[Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=1toolring&config=eyJ1cmwiOiJodHRwczovL21jcC4xdG9vbHJpbmcuY29tL21jcCJ9), or add this to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "1toolring": { "url": "https://mcp.1toolring.com/mcp" } } }
```

**VS Code / GitHub Copilot**

```bash
code --add-mcp '{"name":"1toolring","type":"http","url":"https://mcp.1toolring.com/mcp"}'
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/khmuhtadin/1toolring-mcp
```

Or `gemini mcp add --transport http 1toolring https://mcp.1toolring.com/mcp`, then `/mcp auth 1toolring`.

**claude.ai and ChatGPT**

Add a custom connector with the URL `https://mcp.1toolring.com/mcp` (no client ID needed), then choose Allow.

**Hermes Agent**

```sh
hermes plugins install https://github.com/khmuhtadin/1toolring-mcp
hermes plugins enable 1toolring
```

Then add your key (from https://app.1toolring.com/keys) as `ONETOOLRING_API_KEY` in your Hermes profile `.env`, or paste it in the plugin's settings form in Hermes Desktop. Portable packages stay disabled until you enable them. Start a new session (or run `/reload-mcp`) and the `1toolring` MCP tools are available, along with the `1toolring:1toolring` skill.

Disclosure for the Hermes package:

- Every tool call, with its arguments, goes to 1ToolRing's hosted server (`mcp.1toolring.com`). The tool list is served by that server at runtime.
- `run_tool` spends money from the prepaid balance of the account that owns the key, at the price shown by `inspect_tool`. Failed runs are not charged. The other three tools are free and read-only.
- The server is marked `untrusted` in the package, so Hermes asks before every `run_tool` call; the free read-only tools run without a prompt.
- The key is read from `ONETOOLRING_API_KEY` and sent as an `Authorization: Bearer` header. The package has no local code, runs no shell commands and stores nothing.

**Every agent on this machine at once**

```bash
npx add-mcp https://mcp.1toolring.com/mcp -g
```

## Agent on a server or VPS

Sign-in opens in a browser on your own computer. When your agent runs on another machine, that browser cannot reach the agent, so the Allow click leaves it waiting for a callback it will never get. After you choose Allow, the 1ToolRing page shows a link and a ready curl command. Paste the link to your agent, or run the command on the server. The link works once and expires soon.

You can also skip the sign-in flow and use an API key: create one at https://app.1toolring.com/keys, then follow the API key steps at https://1toolring.com/install/ (they include a one-line installer for servers).

## How your agent handles cost and questions

- It runs small jobs without asking (a run of Rp1.000 or less, about $0.05, while the whole request stays under Rp5.000) and tells you the cost once at the end.
- It asks first for anything above that, or above half your balance.
- When a request could mean different things it asks one short question with a few options, its recommendation first.

## Pricing and payment

Pay per call, no plan. A Google search costs about Rp48 (roughly $0.003). Top up any amount from Rp10.000 by Indonesian bank virtual account or minimarket, or from $1 by card. Prices are always shown before a run. See https://1toolring.com/pricing/.

## Privacy and support

- Privacy policy: https://1toolring.com/privacy/
- Terms: https://1toolring.com/terms/
- Support: hello@1toolring.com

1ToolRing is built by Khaisa Studio, Indonesia.

## License

The contents of this repository (docs and config files) are MIT licensed. The hosted service is covered by the terms above.
