# Jupiter and PayBox boundary

Jupiter DCA and direct PayBox swap/plugin execution are intentionally out of scope for this controlled single-purchase version.

Do not call `paybox_request_swap`, `paybox_use_plugin`, `jupiter_place_solana_order`, a host Jupiter API, transfers, or x402 payments to purchase an xStock. Use `xstocks_preview_buy`, authenticated browser approval, `xstocks_submit_buy`, and `xstocks_get_buy_status`.

If the controlled backend reports that quote, route, simulation, eligibility, or execution capability is unavailable, return `blocked`. Do not invent fields, choose another mint, or fall back to another payment path.
