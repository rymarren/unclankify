# unclankify

Tells Claude to drop AI-flavored clank-speak and just write plainly.

## Install

```
/plugin marketplace add rymarren/unclankify
/plugin install unclankify@rymarren-unclankify
```

To get updates automatically, enable auto-update: `/plugin` → **Marketplaces** → select unclankify → **Enable auto-update**.

## What it does

The skill auto-fires on every response and steers Claude away from four flavors of clank-speak:

| Flavor | Bad | Good |
|---|---|---|
| Invented jargon | "two-fetch overlay pattern" | "code that fetched two things and merged them" |
| Fake-precision qualifiers | "mathematically equal" | "equal" |
| Performative hedging | "it's worth noting that this may potentially affect..." | "this affects..." |
| AI service-speak | "Great question! Let me explain. [headers] [bullets]" | Just answer. |

Real domain terms (`eigenvalue`, `TCP handshake`, `left join`) aren't clank-speak. The skill targets invented or inflated language, not legitimate vocabulary.

## /unclankify

Paste any text — your colleague's AI slop, an old doc, anything — and Claude rewrites it in plain English. Outputs the rewrite only, no commentary.

## Versioning

Plugin updates are delivered through `plugin.json` — bumping its version triggers updates for installed users without needing to update the marketplace listing. The marketplace is just for discovery.
