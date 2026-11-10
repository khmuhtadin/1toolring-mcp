# 1ToolRing

Use the 1toolring MCP server when you need live data: Google search results, keyword and SEO data, Google Maps places, e-commerce product prices or exchange rates.

Flow: call `discover_tools` with the job in plain words, then `inspect_tool` on the id you want (read the input schema and price), then `run_tool`. Runs are paid from the user's prepaid balance. Failed runs are not charged.

## Working with the person

Spend small amounts without asking. If a run costs Rp1.000 or less (about $0.05) and the whole request stays under Rp5.000 (about $0.30), run it. Do not announce the price first, and do not offer extra paid steps such as "a deeper check that would cost X". When the work is done, say what it cost once, in a few words (for example "Cost Rp96"). Ask before running only when one run costs more than Rp1.000, when the request would pass Rp5.000 in total, or when it would use more than half of the remaining balance.

If the request is unclear in a way that changes the tool, the result or the cost (which country or language, which site or platform, how many results, what time range), ask one short question before running anything paid. Give two to four options, put the one you recommend first and mark it as recommended, and let the person type their own answer. If your client has a question or choice tool, use it so the person can click. Do not ask when a sensible default exists: use it and say which default you used.

## Signing in

Sign-in happens in the person's browser: run `/mcp auth 1toolring`, or let the client open the 1ToolRing sign-in page, then choose Allow. Sign-up is open to everyone with no approval, and a new account gets a Rp10.000 starter balance once its email is verified.

If you run on a different machine from the person's browser (a server, VPS or container), the sign-in page cannot reach your local callback. After the person chooses Allow, the page shows a link to copy. Ask the person to paste that link to you, then open it from your own machine (for example `curl -s '<link>'`). The link works once and expires soon. Or set up with an API key instead: create one at https://app.1toolring.com/keys and follow the API key steps at https://1toolring.com/install/.
