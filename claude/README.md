# The Astro Diary for Claude

Explore calculated astrology data in conversation, with guided workflows for your natal chart, the coming week, and relationships. Interpretations are for reflection, not predictions or professional advice.

This is a Claude directory review candidate. Both the connector and plugin were submitted on October 13, 2026; their last verified statuses were **In review** and **Publish requested** (plugin v0.1.3), respectively. These statuses have not been refreshed for this documentation update on October 15. Public source availability is not directory approval or publication.

## What it adds

- **Get started:** explore public sky and Moon data, or a selected saved profile's natal chart and daily transits.
- **Weekly reflection:** connect a dated week's personal transit highlights and upcoming events to a focus you choose.
- **Relationship reflection:** explore synastry, composite charts, or dated relationship weather for two selected saved profiles.

The skills preserve unknown-birth-time limitations, distinguish calculated data from interpretation, and avoid compatibility scores or fixed labels for children. Unknown-time natal charts omit the Moon sign, placement, and Moon-dependent aspects; synastry omits contacts involving the unknown-time person's Moon. Some transit tools still return approximate natal Moon contacts, so their precision notes remain essential. These workflows do not retrieve the website's full Family Guide or every written report.

## Connect

The source package is available from this repository, independently of Anthropic directory approval. In Claude Code 2.1.275 or later:

```text
/plugin install the-astro-diary --marketplace tvidenov/astro-diary-plugin
```

The plugin uses the dedicated read-only Streamable HTTP MCP server at `https://theastrodiary.com/mcp/claude`. No local program, installation hook, API key, or client secret is bundled.

Public sky and Moon tools require no Astro Diary account. Personal charts require your own Astro Diary account, saved profiles, and OAuth consent. Feature-specific plan restrictions still apply; installing the free plugin does not unlock a paid service plan.

In Claude chat or Cowork, open the plugin's Connectors tab, add The Astro Diary, and connect your account. Until the directory entry is available, add a custom connector with the server URL above, select OAuth/sign in, use public client ID `4fb2f85096ba56a3cc416e53a35cf5e07ce5e0b733f755bf`, and leave the client secret empty. This client ID is a public identifier, not a credential. Sign in only on theastrodiary.com.

Claude Code loads the remote connection from `.mcp.json`; complete its interactive OAuth login when prompted. Its callback is pinned to `http://localhost:8892/callback`; keep that local port available during login. The client uses PKCE and also accepts Claude's exact web callback. The server limits this client's grant to profile/chart reads and staying connected. Stop if diary-write permission appears.

The Claude endpoint exposes 18 read-only tools. It does not register the diary-write tool, and its embedded workspace hides diary-save controls. OAuth tokens are bound to this dedicated resource; tokens for the shared endpoint cannot be used here. The server enforces these boundaries independently of skill instructions. The plugin does not save diary entries, modify profiles, or schedule routines.

The dedicated endpoint was deployed on October 12, 2026. Recorded protocol checks passed all 18 tools, PKCE login, token refresh, resource-audience isolation, and unknown-birth-time Moon handling using a separate fictional account. By October 13, all 17 conversational tools and the interactive workspace had Claude-host evidence; the eighteenth tool, app-only `search_profile_mentions`, was checked with MCP Inspector. This is connector acceptance evidence, not proof that this exact repository package's installed skills have been exercised or that Anthropic has approved it.

## Try it

- “Using The Astro Diary, show the Moon forecast for three days in Europe/Sofia.”
- “Help me understand the natal chart for the saved profile I select.”
- “Help me reflect on the week starting October 12, 2026, using my selected profile.”
- “Compare two profiles I choose, focusing on communication rather than a score.”

## Data and privacy

The package itself stores no data and runs no local code. Tool requests go only to The Astro Diary's declared HTTPS endpoint. Authenticated tools access profiles belonging to the signed-in account; selected profile and chart results are returned to Claude. Do not select another person's profile without the right to use their information. Birth details are personal data even when the resulting interpretation is just for reflection.

Data already saved on the Astro Diary website is governed by its [privacy policy](https://theastrodiary.com/en/privacy) and [service terms](https://theastrodiary.com/en/terms). Disconnecting the connector stops its use in Claude but does not delete your Astro Diary account or previously returned conversation content. Claude handles conversation content under its own terms and settings. No additional analytics, advertising, or third-party destinations are included in this package.

The plugin is intended for adults. Family-related questions are for adult reflection, not developmental, medical, or mental-health assessment.

For support, use the [plugin issue tracker](https://github.com/tvidenov/astro-diary-plugin/issues). Never post credentials, birth details, or private chart data publicly.

## License

This plugin package is MIT-licensed. The license does not cover or expose the hosted backend, website source, account data, or credentials.
