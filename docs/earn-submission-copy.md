# Spout Finance Product Feedback — submission copy ($1K USDC, deadline Sep 24 06:00 IST)

## Title
Spout Finance beta: deep review — the LTV model is the flagship and the flashpoint

## Review summary (~200 words)
Spout's pitch is compelling: **0% interest borrowing against tokenized equities at 50%
LTV** — "Aave, but for stocks." The beta UX is genuinely clean (Phantom connect, vault
deposit of tokenized AAPL, borrow against it). But the review surfaced systemic issues a
production launch can't carry:

1. **Beta-mode ambiguity.** Nothing on beta.spout.finance signals you're on a test/limited
   deployment — no banner or badge. Users deposit real assets without knowing the surface
   is a beta. Fix: mandatory warning banner + deposit confirmation acknowledging partial
   functionality.
2. **Single-source oracle, no staleness check.** The tokenized-equity price feed looks like
   one oracle source with no staleness detection. A stale print on a 50% LTV product is a
   liquidation-event driver. Fix: multi-oracle aggregation (Pyth + Chainlink + on-chain
   TWAP), staleness rejection, conservative deviation bands on equities.
3. **Liquidation buffer invisible.** 50% LTV with no visible liquidation-buffer policy means
   borrowers can't price their own liquidation risk. Fix: show configurable liquidation
   buffer (e.g., 52% trigger) + health factor in the vault UI.
4. **No portfolio-level view.** Power users can't see equity exposure vs. debt across
   vaults — the one view whales use to size position. Fix: aggregated portfolio dashboard.

Full findings + severity log in repo. Bottom line: the mechanism is differentiated; the
risk layer needs hardening before it deserves the "Aave of equities" title.

## Link to include
https://github.com/sidsri14/spout-finance-review