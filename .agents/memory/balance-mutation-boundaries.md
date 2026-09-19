---
name: Balance mutation boundaries
description: Durable rules for protecting user and house balances during transfers and external payouts.
---

External payouts must reserve the user's balance and the house's asset balance before calling the provider; if the provider rejects or errors, refund both reservations exactly once.

**Why:** A legacy withdrawal path could call missing house helpers, ignore a failed user debit, and leave either a free payout or a permanently deducted user balance.

**How to apply:** Use the shared balance lock for multi-account moves and house-to-user transfers. Keep provider calls outside the lock, with explicit reservation and refund state.