---
name: Deposit notification invariants
description: Rules for keeping crypto deposit settlement, fees, notifications, and explorer links consistent.
---

The settlement layer must pass the gross provider USD value to the confirmation renderer; the renderer derives the fee-adjusted credited value from the separate fee field.

**Why:** Passing the net amount as gross causes the fee to be subtracted twice in the user-facing confirmation while accounting totals remain correct.

**How to apply:** Keep gross USD, credited USD, fee USD, coin amount, network, and txid as separate values across provider verification, balance crediting, and notification retry payloads.

The Telegram deposit UX has two distinct user-facing stages: a short button-free processing message before the authoritative credit transaction on every verified payment path, followed by a separate button-free confirmation after crediting succeeds. Processing must not include balance, Txid, or diagnostic details.

**Why:** Combining detection and settlement makes users think funds are confirmed before the blockchain/provider confirmation is complete, while skipping processing on a direct provider path makes the player miss the intended status update.

**How to apply:** Keep the processing and confirmation notification claims separate and preserve premium custom-emoji formatting without falling back to inline keyboards or diagnostic blocks.

Telegram Gift confirmations are non-chain deposits: show the player, gift type, Stars received, USD value, and credited amount with premium emojis, but never show a fake blockchain transaction ID.

**Why:** Gifts settle through Telegram's gift profile rather than a blockchain transaction, so the old generic template exposed internal labels and misleading transaction fields.

**How to apply:** Keep the gift layout separate from crypto confirmation rendering while reusing the same header, quote-block, premium-emoji, and casino closing style.