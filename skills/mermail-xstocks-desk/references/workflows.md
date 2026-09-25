# Controlled xStocks workflows

## Discovery and selection

1. Translate only explicit user filters into `xstocks_search_products`. Category assignments without verified evidence are excluded by the catalog.
2. Present the candidates without ranking them as investment advice. If zero or multiple products remain, stop for user selection.
3. Never convert a ticker, email, search result, or social post directly into a mint allowlist.

## Exact preview

1. Call `xstocks_preview_buy` for the selected catalog product and amount, omitting a wallet unless the user already selected one.
3. Stop on every blocked or unknown result. Do not switch provider, mint, network, or tool.
4. Present one `reviewUrl` as **Open Mermail Agent Wallet**. Label `simulated: true` as local testing with no asset movement.
5. The purchase session lasts up to 15 minutes. Its browser page may refresh a 30-second quote while preserving product, amount, and wallet.

## Approval and submission

1. Require approval recorded by the authenticated Mermail Agent Wallet browser page for the current quote terms.
2. Call `xstocks_submit_buy` once with only the preview ID; the server owns approval and idempotency state.
3. Do not retry a timeout as a new purchase. Use `xstocks_get_buy_status` with the same preview ID for one reconciliation when the user asks.
4. Report pending/unknown separately. Report `confirmed` only after authoritative terminal confirmation; `confirmed_simulation` is local test evidence only.

## Unsupported flows

DCA, recurring schedules, autonomous execution, ticker-only purchases, direct generic swaps, transfers to token mints, and alternate Jupiter HTTP/plugin paths are out of scope for this version.
