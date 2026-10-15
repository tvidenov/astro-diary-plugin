# Reviewer guide — 0.1.1

Documentation updated October 15, 2026. This guide reconciles the recorded October 12 host checks and subsequent backend fixes; it does not claim a new package installation, a fresh authenticated Grok test, or marketplace approval.

## Connection

- MCP: `https://theastrodiary.com/mcp` (Streamable HTTP).
- OAuth authorization-code flow with PKCE, public client; no client secret.
- Public client ID and four explicit read scopes are included in `mcp.json`.
- Callbacks: `https://www.cursor.com/agents/mcp/oauth/callback` and `http://localhost:8787/callback` only.
- Personal tests require a reviewer-controlled account with a fictional saved profile. Do not use the developer's real profile or share credentials in a repository.
- Some advanced tools require an eligible service plan. Review access must be arranged privately if needed; no review account is provisioned by this package.

## Core walkthrough

1. Before connecting an Astro Diary account, ask: “Using The Astro Diary, show the Moon forecast from October 20, 2026 for three days in Europe/Sofia.” Expect dates, signs, degrees, and phases, not just “calculated.”
2. Connect through the host, sign in at theastrodiary.com, and verify recipient branding and the four read-only permissions. Do not approve diary-write permission.
3. Ask “Which saved profiles do I have?” Select the fictional test profile by its returned ID. Expect only authorized profile names/IDs and summary fields, not birth details.
4. Ask for the selected profile's natal chart. With a known birth time, expect calculated placements and aspects. With an unknown birth time, expect `moonSign: null`, no Moon placement or Moon-dependent chart aspects, and no Rising sign, houses, angles, or calculated points. Expect a precision note explaining these omissions and that retained slower-body positions and contacts are approximate.
5. Ask for its transits on October 12, 2026. Expect the requested date, transit positions, and aspects to the selected natal chart.

Public Moon, OAuth, profile listing, natal-chart, and dated-transit flows passed native Grok acceptance on October 12 through the manually configured connector, not installation of the marketplace package. The stricter unknown-time natal Moon omission shipped later that day and was validated through protocol tests and Claude; repeat step 4 during Grok package acceptance. No private test outputs are shipped here.

## Recorded host checks and backend fixes — October 12

- Public Moon forecast across the Europe/Sofia clock-change/date boundary: three daily values and UTC/local event timestamps matched an independent live MCP read.
- Two explicitly fictional saved profiles were used for wider testing, one with unknown birth time. An ambiguous "QA Alex" request prompted a choice instead of silently choosing a profile.
- Unknown-time natal chart: the initial Grok check omitted Rising, angles, and houses but still returned an approximate Moon. That result is superseded by the later Moon-precision fix: the backend now omits the Moon sign, placement, and Moon-dependent chart aspects entirely, with an explicit precision note. Known-time Moon output is unchanged. This later behavior passed protocol and Claude validation; that is not a claim of installed-package validation in Grok.
- Weekly transit highlights: the eighth-day spill is fixed in the backend. Samples are restricted to the inclusive requested window before ranking and truncation. The post-deployment native Grok check for `forecastDays: 7` returned seven dates, October 12–18. A seven-day request starting October 15 must likewise stay within October 15–21; missing provider samples must not be fabricated.
- Synastry, composite, and dated relationship-weather tools returned calculated results for the two fictional profiles. Composite/weather omit unknown-time Moon and angle-dependent output. Synastry now omits the unknown-time person's Moon sign and contacts involving that person's Moon before summarization. Contacts involving only the known-time person's Moon may remain. Post-deployment native Grok checks passed in both pair directions; ordered, versioned cache keys preserve each person's chart side. The earlier skill-only workaround is no longer the backend's precision boundary.
- Native catalog searches on October 12 by exact product name and public repository URL returned no matching listing. The tested connector's source was "Added manually"; no package installation or current marketplace approval is claimed.
- Removing only the saved Grok connection preserved the manual plugin configuration and removed authenticated tool availability. After user-attended approval of the final reconnect, Grok again showed Connected with all 19 tools enabled. The user also reported denying an earlier attempt and Grok remained unauthenticated, but no explicit denial callback was captured; denial-specific host evidence remains partial.
- Recorded backend regression checks cover inclusive highlight windows, unknown-time Moon omissions, directional pair order, and structured/text output parity. Isolated OAuth lifecycle tests passed consent denial, PKCE, refresh rotation, scope-elevation rejection, and refused diary writes. These are backend checks, not proof of every native host lifecycle behavior.

## Remaining acceptance before general availability

- Install this exact package through the supported host flow and repeat the walkthrough.
- On a controlled test account: capture an explicit consent-denial outcome and verify refresh/expired authorization behavior. Disconnect/reconnect is observed in the native UI; it does not by itself prove token refresh or revocation at the authorization server.
- Re-test the revised weekly/relationship skills after actual package installation; manual tool-flow tests do not prove that packaged skills are loaded.
- Check missing-plan behavior in a controlled non-Plus account without changing an existing user's billing.
- Verify a read-only token cannot save a diary entry. This is a controlled authorization test, not part of normal user workflows; backend scope-denial tests already pass.
- Confirm publisher approval and actual listing/installability. Do not equate the prior application receipt with approval.

The manual connector's core read flows and the backend calculation fixes have recorded passing checks. Exact-package installation and broader host lifecycle checks above remain open. Interactive workspace rendering is intentionally outside the initial promise. A working manual connection or public Git repository is not evidence of marketplace approval or listing availability.
