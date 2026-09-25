# Controlled xStocks tool contracts

These tools require the full Mermail MCP OAuth profile. They are not available through an API key or the restricted agent-inbox profile.

| Tool | Purpose | Effect |
| --- | --- | --- |
| `xstocks_search_products` | Search active, non-halted products with a matched Solana deployment and evidence-backed categories | Read-only discovery |
| `xstocks_preview_buy` | Verify the selected product and mint, check eligibility/wallet/provider capabilities, and store a 30-second exact preview | Internal reversible write; never trades |
| `xstocks_submit_buy` | Submit the stored preview after exact user approval; the backend ignores caller-supplied trade terms because none are accepted | Financial effect when live execution is enabled |
| `xstocks_get_buy_status` | Read or reconcile the durable state of one existing purchase session | Read-only status |

## Inputs

- Search accepts optional `q`, `assetType`, `sector`, `theme`, `page`, and `pageSize`.
- Preview accepts `productId`, `amountUsdc`, optional `credentialId`, and optional `slippageBps` up to 50. Omit the credential when the backend can select one eligible/default Solana wallet.
- Preview returns a first-party `reviewUrl`. Approval happens only in its authenticated Mermail Agent Wallet browser session.
- Submit and status accept only `previewId`. They do not accept approval tokens, idempotency keys, mint, amount, network, wallet, or slippage overrides.

The mint fields returned by search or preview are token identifiers, not wallet deposit destinations. Never send USDC directly to one.

Generic PayBox swap/plugin tools are not an xStocks execution surface. The backend rejects direct execution for recognized xStocks mints and requires the controlled workflow.
