# StockDesk

**Farm inventory management for farmOS — Android app, offline-first**

StockDesk is a single-file Android app for tracking farm supply inventory and syncing adjustments to a [farmOS](https://farmos.org) instance. Log what comes in, what goes out, and what's on hand — from the barn, the feed room, or wherever you are — then push to farmOS when you're ready.

Part of the [FarmDesk suite](https://github.com/ltlfarm).

---

## Features

- Dashboard view of all inventory items with current quantities
- Category tabs for quick filtering (feed, medical, supplies, etc.)
- Log increments (restock), decrements (use), and absolute resets
- Optional restock fields: seller, lot number
- Adjustment history with sync status indicators
- Edit existing local adjustments before they're pushed
- Syncs to farmOS JSON:API — quantity and log records posted in the correct sequence
- Categories and units auto-detected from your farmOS taxonomy on first fetch
- Offline-first: adjustments queue locally, pushed only when you tap Sync
- Cross-module bridge: GoatDesk medication logs automatically deduct from StockDesk inventory when both are in use (via FarmDesk unified app)
- No hardcoded farm data — works with any farmOS instance

---

## Requirements

- farmOS 2.x with JSON:API and inventory module enabled
- OAuth2 credentials with `farm_manager` scope
- Android 6+ (tested on Samsung Galaxy devices)

---

## Installation

Download the latest APK from [Releases](https://github.com/ltlfarm/stockdesk/releases) and sideload it onto your device.

---

## Setup

1. Open the app and tap the **⚙️** settings icon
2. Enter your farmOS URL, username, and password
3. Tap **Fetch Inventory** to import your material assets
4. Start logging adjustments

---

## farmOS Integration Notes

The inventory write sequence follows the farmOS JSON:API spec exactly:

1. POST `quantity--standard` with `inventory_adjustment` and asset relationship
2. POST `log--activity` (or `log--input` / `log--output`) linking the quantity with `meta.target_revision_id`
3. Log `status` must be `done` for inventory to count in farmOS

The asset `inventory` field is computed/read-only in farmOS — StockDesk never writes to it directly.

---

## Repository

`github.com/ltlfarm/stockdesk`

APK builds automatically via GitHub Actions on every push to `main`.
