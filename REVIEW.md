# Reviewer guide — 0.1.1

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
4. Ask for the selected profile's natal chart. Expect calculated placements and aspects; unknown birth time must omit houses/angles.
5. Ask for its transits on October 12, 2026. Expect the requested date, transit positions, and aspects to the selected natal chart.

These core behaviors passed native Grok acceptance on October 12. That evidence covers the manually configured connector, not installation of the marketplace package. No private test outputs are shipped here.

## Additional host checks — October 12

- Public Moon forecast across the Europe/Sofia clock-change/date boundary: three daily values and UTC/local event timestamps matched an independent live MCP read.
- Two explicitly fictional saved profiles were used for wider testing, one with unknown birth time. An ambiguous "QA Alex" request prompted a choice instead of silently choosing a profile.
- Unknown-time natal chart: no Rising sign, angles, or houses were reported. A returned Moon position remains approximate; the host warned about uncertainty near a sign boundary.
- Weekly event/highlight reads returned useful calculated results for both fixtures. A fresh independent native recheck reproduced eight highlight dates for `forecastDays: 7` (October 12–19), while upcoming events cover October 12–18. The weekly skill excludes the extra boundary date from the requested week's interpretation. Backend date-window normalization remains unresolved.
- Synastry, composite, and dated relationship-weather tools returned calculated results for the two fictional profiles. Composite/weather correctly omitted the unknown-time Moon and angles. Synastry still includes uncertain Moon contacts with precise-looking orbs and lacks a Moon-specific caveat; the relationship skill explicitly qualifies this and avoids basing concrete themes on those contacts. This is a workflow safeguard, not a backend fix.
- Native catalog searches by exact product name and public repository URL returned no matching listing. The current connector's source is "Added manually"; no package installation is claimed.
- Removing only the saved Grok connection preserved the manual plugin configuration and removed authenticated tool availability. After user-attended approval of the final reconnect, Grok again showed Connected with all 19 tools enabled. The user also reported denying an earlier attempt and Grok remained unauthenticated, but no explicit denial callback was captured; denial-specific host evidence remains partial.
- The focused backend OAuth/MCP regression suite passes 97 tests. Earlier isolated OAuth lifecycle tests passed consent denial, PKCE, refresh rotation, scope-elevation rejection, and refused diary writes. These are backend checks, not proof of every native host lifecycle behavior.

## Remaining acceptance before general availability

- Install this exact package through the supported host flow and repeat the walkthrough.
- On a controlled test account: capture an explicit consent-denial outcome and verify refresh/expired authorization behavior. Disconnect/reconnect is observed in the native UI; it does not by itself prove token refresh or revocation at the authorization server.
- Re-test the revised weekly/relationship skills after actual package installation; manual tool-flow tests do not prove that packaged skills are loaded.
- Resolve the weekly highlight date-boundary discrepancy and unknown-time Moon precision caveat in the backend response; check missing-plan behavior in a controlled non-Plus account without changing an existing user's billing.
- Verify a read-only token cannot save a diary entry. This is a controlled authorization test, not part of normal user workflows; backend scope-denial tests already pass.
- Confirm publisher approval and actual listing/installability. Do not equate the prior application receipt with approval.

Public Moon, login, profile listing, natal-chart, dated-transit, ambiguity, and unknown-time omission checks pass. Broader host checks above remain open. Interactive workspace rendering is intentionally outside the initial promise.
