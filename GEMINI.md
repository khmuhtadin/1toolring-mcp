# 1ToolRing

Use the 1toolring MCP server when you need live data: Google search results, keyword and SEO data, Google Maps places, e-commerce product prices or exchange rates.

Flow: call `discover_tools` with the job in plain words, then `inspect_tool` on the id you want (read the input schema and price), then `run_tool`. Runs are paid from the user's prepaid balance, so tell the user the price before running anything costly. Failed runs are not charged.
