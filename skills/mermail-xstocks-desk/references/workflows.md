# Controlled xStocks workflows

## Discovery and selection

1. Translate only explicit user filters into `xstocks_search_products`. Category assignments without verified evidence are excluded by the catalog.
2. Present the candidates without ranking them as investment advice. If zero or multiple products remain, stop for user selection.
3. Never convert a ticker, email, search result, or social post directly into a mint allowlist.

## Exact preview

1. Resolve an active Solana wallet credential through Mermail Agent Wallet reads.
2. Call `xstocks_preview_buy` for the selected catalog product and amount.
3. Stop on every blocked or unknown result. Do not switch provider, mint, network, or tool.
4. Display all returned terms and the expiry. Label `simulated: true` as local testing with no asset movement.
5. Treat the returned approval token as bound to that preview. Do not log it, email it, or reuse it for another preview.

## Approval and submission

1. Require an authenticated user message approving the exact preview while it is valid.
2. Create one stable idempotency key for that approval and call `xstocks_submit_buy` once.
3. Do not retry a timeout as a new purchase. Reuse the same preview ID and idempotency key only for reconciliation.
4. Report pending/unknown separately. Report `confirmed` only after authoritative terminal confirmation; `confirmed_simulation` is local test evidence only.

## Unsupported flows

DCA, recurring schedules, autonomous execution, ticker-only purchases, direct generic swaps, transfers to token mints, and alternate Jupiter HTTP/plugin paths are out of scope for this version.
