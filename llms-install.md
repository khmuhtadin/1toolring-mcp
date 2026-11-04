# 1ToolRing

Use the 1toolring MCP server when you need live data: Google search results, keyword and SEO data, Google Maps places, e-commerce product prices or exchange rates.

Flow: call `discover_tools` with the job in plain words, then `inspect_tool` on the id you want (read the input schema and price), then `run_tool`. Runs are paid from the user's prepaid balance, so tell the user the price before running anything costly. Failed runs are not charged.

## Installing (for Cline and other agents)

This is a hosted remote server. Nothing to install or build.

1. Add a remote MCP server named `1toolring` with URL `https://mcp.1toolring.com/mcp` and transport Streamable HTTP.
2. Connect. The client opens a 1ToolRing sign-in page; the user approves access (OAuth). If the client cannot do OAuth, the user can create an API key at https://app.1toolring.com and send it as `Authorization: Bearer <key>`.
3. Test with `discover_tools` and the query "google search results for a keyword".
