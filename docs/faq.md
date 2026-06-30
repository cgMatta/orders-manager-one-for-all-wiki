# FAQ — Frequently Asked Questions

---

## General

### Does the EA place trades automatically?

No. The EA is a **trading panel**, not an automated strategy. It helps you place,
manage and close orders manually with greater speed and precision. All trading
decisions are yours.

---

### Does it work on live accounts?

Yes. The EA has been tested on both demo and live accounts across multiple brokers.
Always test on a demo account first before using it on a live or funded account.

---

### Is it compatible with prop firm accounts?

Yes, it has been tested on prop firm environments. However, always verify that
your prop firm allows the use of trading panels and EAs before using it on a
funded account. The EA does not use any forbidden techniques (no martingale,
no grid, no tick scalping).

---

### Does it work on all instruments?

Yes. The EA auto-detects the instrument type (Forex, indices, metals, crypto, CFDs)
and adjusts lot size calculations accordingly. It works on any symbol available
in your broker.

---

### Can I run multiple instances on the same account?

Yes, but each instance must have a **different Magic Number** (`InpMagicNumber`).
If two instances share the same magic number, they will interfere with each other's
order tracking.

---

## Installation & Setup

### The panel does not appear after loading the EA

Check the following:

1. **AutoTrading is enabled** — the AutoTrading button in the MT5 toolbar must be green
2. **Algo Trading is allowed** — right-click the chart → Expert Advisors → Properties →
   Common tab → check "Allow Algo Trading"
3. **The `.ex5` file is in the correct folder** — it must be placed in `MQL5/Experts/`
   and MT5 must be refreshed (right-click the Navigator panel → Refresh)
4. **The chart has enough space** — try widening the chart window if the panel appears cut off

---

### Orders are rejected with "Invalid stops" error

This means your SL or TP is too close to the current price for the broker's
minimum stop distance. Solutions:

- Increase `InpSLTPBufferPts` (try `3` or `5`) in the EA properties
- Enable `InpShowStopsZone` to see the broker's minimum distance visually on the chart
- Move your SL or TP further from the entry price

---

### The lot size shown is `0.00`

This can happen on instruments with a very small volume step (e.g. BTCUSD with
step `0.001`). Make sure you are using **v1.81 or later**, which fixes this display issue.

---

### The EA settings reset after restarting MT5

All panel settings are saved automatically and restored on restart. If settings
are not persisting, check that:

- MT5 has write permissions to its data folder
- The EA is not being removed and re-added (which triggers a clean state)
- You are loading the EA on the **same chart** (settings are saved per chart ID)

---

## Easy Order Panel

### What is the difference between Manual and One-Click mode?

- **Manual mode** — you drag SL, TP and Entry lines on the chart to define your trade,
  then click Place Order. Best for precise setups with specific price levels.
- **One-Click mode** — you set a fixed volume, SL and TP distance, then click BUY or
  SELL for an instant market order. Best for fast entries.

---

### The draggable lines are not showing

Click the **Activate lines** button at the bottom of the Easy Order panel.
Lines only appear when activated to avoid cluttering the chart when you are
not actively placing an order.

---

### Can I use multi-TP on a Netting account?

Yes. On Netting accounts, multi-TP is handled via the **Synthetic Netting Ladder**:
the EA places a single order with the farthest TP as the real broker TP, then
automatically executes partial closes at each intermediate rung. The result is
the same as multi-TP from the user's perspective.

---

### What does the "runner" TP leg mean?

When you activate multiple TP legs but leave one without a TP price (0%), that
leg becomes a **runner** — a position that stays open indefinitely until you
close it manually. This is useful for letting part of your position run with
the trend while taking profit on the other legs.

---

## Order List Panel

### The Order List shows orders from other symbols

By default the Order List shows all positions across your account. Use the
**symbol dropdown** (top left of the panel) to filter by a specific instrument.
The filter is saved and restored across restarts.

---

### Bulk actions are not working

Check that:

- The **view tab** matches what you want to close (Open / Pending / All)
- The **symbol filter** is set correctly (it may be filtering to a symbol with no orders)
- **AutoTrading** is enabled in MT5

---

### What does the proximity highlight mean in the Order List?

When the current price is within a certain percentage of an SL, TP or Entry level,
that level is highlighted to warn you it may be hit soon. You can adjust the
threshold with `InpNearPct` in the EA properties.

---

## Trade Badges

### The badges are not visible on the chart

Make sure `InpShowBadges` is set to `true` in the EA properties.
Also check that the EA is active (not paused) in the Main Panel.

---

### The badge colors do not match my positions

Badge colors are fully customizable in the `[TB]` section of the EA properties.
Separate colors are available for BUY vs SELL and for open positions vs pending orders.
