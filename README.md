# The Astro Diary — Cursor / Grok plugin

For Claude chat, Cowork, and Claude Code, see the separate [Claude package](claude/README.md). Its source distribution is independent of Anthropic directory review. The Cursor/Grok package below is unchanged.

![The Astro Diary](assets/icon.png)

A Cursor Plugin containing a remote MCP connection and three guided workflows:

- **Get started:** public sky and Moon data, or a saved profile's natal chart and daily transits.
- **Weekly reflection:** personal transit highlights and upcoming events for a dated week.
- **Relationship reflection:** synastry, composite charts, and dated relationship weather for two saved profiles.

This is a **review candidate, not an approved marketplace listing**. Public Moon data, login, profile listing, and selected-profile natal/transit reads have been tested in Grok; broader host acceptance remains incomplete. The marketplace team confirmed that approval makes the plugin discoverable in Grok Bot and that existing paid service plans are permitted. Approval has not been verified. This package uses the [Cursor Plugin format](https://cursor.com/docs/reference/plugins) so `mcp.json` can explicitly request read-only `auth.scopes`; that host-specific field is not part of the portable Agent Plugins MCP schema.

This repository contains only the plugin configuration, skills, documentation, and branding. It does not include The Astro Diary website/backend source, user data, or credentials.

## Connection and permissions

The package connects to `https://theastrodiary.com/mcp` using Streamable HTTP. No local executable, installation hook, password, or API key is included.

Public sky and Moon tools need no Astro Diary account. Personal tools require an Astro Diary account, saved profiles, and authorization. Plan restrictions still apply to the underlying features.

**Compatibility updates:** deployed on October 12, 2026. The server supports Cursor's documented web and desktop callbacks, requires PKCE, and caps new Cursor/Grok registrations at read-only scopes. Backend checks and user-attended Grok login pass. A follow-up result-format fix retains structured output and also supplies JSON text without private UI metadata; fresh native Grok tests return complete Moon calculations, usable saved profile names/IDs, and natal-chart and dated-transit values for the explicitly selected profile. No writes or saved readings were requested. Wider host acceptance remains outstanding. Do not paste tokens into `mcp.json` as a workaround.

Cursor's documented `auth` configuration requires `CLIENT_ID` when specifying `scopes`. The package includes the tested **public** client ID `EFAYWhmvCbFuqxTJPeCzBYFqWIRFiuyA`, registered with the exact Cursor callbacks and four read scopes. This is an identifier, not a credential: no client secret, API key, or local environment variable is required. Use the same configuration in `mcp.json` for a custom connection. Do not fall back to unscoped discovery, because the shared server also supports ChatGPT's optional diary-write permission. Sign in only on theastrodiary.com, and stop if diary-write permission appears.

The intended first pilot grants only `openid`, `offline_access`, `astro.profiles.read`, and `astro.charts.read`. These skills do not save diary entries or schedule routines. However, the shared endpoint also advertises `save_diary_reflection`; skill instructions are **not an access-control boundary**. Verify that the issued token excludes `astro.diary.write` and that the server rejects writes before describing the connection as read-only.

Treat charts as calculations and interpretations as reflection, not predictions or professional advice. The package does not retrieve private diary history, the full website Family Guide, or every website report.

## Try it

- “Using The Astro Diary, show the Moon forecast for the next three days in Europe/Sofia.”
- “Which saved profiles do I have? Explain the natal chart for the one I select.”
- “Using my selected profile, help me reflect on the week starting 2026-10-12.”
- “Compare the two saved profiles I select, focusing on communication rather than a compatibility score.”

Results contain both structured data and JSON text for text-only hosts. Manual-connector checks also exercised weekly event/highlight reads, unknown-time charts, profile ambiguity, synastry, composite charts, and dated relationship weather using fictional profiles. Two calculation-contract caveats remain: weekly highlights may include an extra boundary date, and unknown-time synastry can include approximate Moon contacts with exact-looking orbs. The included skills restrict the requested week and qualify uncertain Moon data; they do not change or repair the backend response. See [REVIEW.md](REVIEW.md) for the exact acceptance boundary. ChatGPT's interactive workspace, profile mentions, and navigation are not promised in Grok Bot.

## Before marketplace release

1. Confirm the prior application's status at [the publisher portal](https://cursor.com/marketplace/publish). The October 9 receipt was verified then; on October 12 the portal displays an application form rather than approval/status. Do not infer rejection or submit a duplicate.
2. The OAuth and text-result compatibility updates are deployed. Test installation of this exact package; the native acceptance so far used a manually configured connector.
3. Complete the remaining controlled-account checks in [REVIEW.md](REVIEW.md), including calculation-contract caveats, native authorization lifecycle, and missing-plan behavior. Backend authorization tests are not a substitute for host acceptance.
4. Keep the plugin wrapper free; underlying service-plan restrictions remain separate. This plugin package is MIT-licensed.
5. Verify actual installability in Grok Bot after approval.

## Privacy, terms, and support

- [Privacy policy](https://theastrodiary.com/en/privacy)
- [Service terms](https://theastrodiary.com/en/terms)
- [Plugin issues](https://github.com/tvidenov/astro-diary-plugin/issues) — do not post birth details, account tokens, or private profile data.

## License

This plugin package is licensed under the [MIT License](LICENSE).

The license applies only to the files in this plugin repository. It does not license or expose The Astro Diary website/backend source, hosted service, user data, or credentials. Existing ChatGPT packaging remains separate. Access to the hosted service is governed by its own terms and permissions.
