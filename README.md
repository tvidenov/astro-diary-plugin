# The Astro Diary — Agent Plugin preview

![The Astro Diary](assets/icon.png)

An Agent Plugin containing a remote MCP connection and three guided workflows:

- **Get started:** public sky and Moon data, or a saved profile's natal chart and daily transits.
- **Weekly reflection:** personal transit highlights and upcoming events for a dated week.
- **Relationship reflection:** synastry, composite charts, and dated relationship weather for two saved profiles.

This is a **preview package, not an approved marketplace listing or Grok-verified integration**. It targets the marketplace ecosystem described in [Grok Bot's plugin documentation](https://cursor.com/docs/grok-bot/work) and uses the portable format accepted by [Cursor Marketplace](https://cursor.com/docs/reference/plugins). Marketplace acceptance and visibility inside Grok Bot still need confirmation.

This repository contains only the plugin configuration, skills, documentation, and branding. It does not include The Astro Diary website/backend source, user data, or credentials.

## Connection and permissions

The package connects to `https://theastrodiary.com/mcp` using Streamable HTTP. No local executable, installation hook, password, or API key is included.

Public sky and Moon tools need no Astro Diary account. Personal tools require an Astro Diary account, saved profiles, and authorization. Plan restrictions still apply to the underlying features.

**Personal authentication is not ready for this host:** the current server's dynamic client registration accepts only ChatGPT callback URLs. An exact callback from the intended Grok/Cursor connector flow must be verified and supported before testing personal access. Do not paste tokens into `mcp.json` as a workaround.

The intended first pilot grants only `openid`, `offline_access`, `astro.profiles.read`, and `astro.charts.read`. These skills do not save diary entries or schedule routines. However, the shared endpoint also advertises `save_diary_reflection`; skill instructions are **not an access-control boundary**. Verify that the issued token excludes `astro.diary.write` and that the server rejects writes before describing the connection as read-only.

Treat charts as calculations and interpretations as reflection, not predictions or professional advice. The package does not retrieve private diary history, the full website Family Guide, or every website report.

## Try after connection is validated

- “Using The Astro Diary, show the Moon forecast for the next three days in Europe/Sofia.”
- “Which saved profiles do I have? Explain the natal chart for the one I select.”
- “Using my selected profile, help me reflect on the week starting 2026-10-12.”
- “Compare the two saved profiles I select, focusing on communication rather than a compatibility score.”

The workflows use structured tool results. ChatGPT's interactive workspace, profile mentions, and navigation are not promised in Grok Bot.

## Before marketplace release

1. Confirm the signed-in publisher account and Grok Bot eligibility at [the publisher portal](https://cursor.com/marketplace/publish).
2. Verify the host's OAuth flow, allow only its confirmed callback, and update consent copy to identify the actual client.
3. Complete public-tool and personal-account tests inside Grok Bot, including denial, reconnect, unknown birth time, and write-scope rejection.
4. Finalize the package's approved open-source license and confirm compatibility of existing paid service plans with the marketplace's terms.
5. Add approved branding, submit the wrapper repository for review, and verify actual installability in Grok Bot after approval.

## Privacy, terms, and support

- [Privacy policy](https://theastrodiary.com/en/privacy)
- [Service terms](https://theastrodiary.com/en/terms)
- [Plugin issues](https://github.com/tvidenov/astro-diary-plugin/issues) — do not post birth details, account tokens, or private profile data.

## License

No open-source license has been granted for this preview yet. The license will be finalized before marketplace release. Existing ChatGPT packaging and the website/backend remain separate.
