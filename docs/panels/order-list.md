# Order List Panel

The Order List panel shows all your open positions and pending orders
with live P&L, risk and quick action buttons for each row.

---

## Header Bar

The header shows a real-time account summary split into three sections:

| Section | Contents |
|---------|----------|
| **Account Summary** | Balance, Equity, Margin, Free Margin |
| **Accumulated Risk** | Open positions count, pending orders count, total risk |
| **Positions** | Open count, pending count, total P&L |

---

## Filters

### Symbol filter
The dropdown on the left filters the list by instrument.
Select a specific symbol or **All** to see your entire account.
The selection persists across MT5 restarts.

### Type filter
Filters by order direction: All, Buy, Sell, Buy Limit, Sell Limit, Buy Stop, Sell Stop.
Resets automatically when switching tabs.

### View tabs
| Tab | Shows |
|-----|-------|
| **All** | Open positions and pending orders |
| **Open** | Open positions only |
| **Pending** | Pending orders only |

---

## Columns

| Column | Description |
|--------|-------------|
| **TYPE** | Order type and direction (BUY / SELL / BUY LMT / etc.) |
| **ASSET** | Instrument symbol |
| **LOTS** | Position size |
| **ENTRY** | Entry price |
| **SL** | Stop Loss level |
| **TP** | Take Profit level (or next Netting Ladder rung if active) |
| **R:R** | Risk:Reward ratio |
| **RISK** | Estimated risk in account currency |
| **P&L** | Current unrealized profit or loss |
| **ACTIONS** | Per-row action buttons |

---

## Row Actions

Each row has the following action buttons:

| Button | Action |
|--------|--------|
| **BE** | Move SL to breakeven for this position |
| **REV** | Reverse the position direction |
| **25% / 50% / 75%** | Partial close at the selected ratio |
| **✕** | Close the position or cancel the pending order |

---

## Bulk Actions

The bulk action buttons in the filter row apply to **all visible rows**
matching the active symbol and type filters:

| Button | Action |
|--------|--------|
| **25% / 50% / 75%** | Partial close all open positions |
| **BE** | Move all open position SLs to breakeven |
| **✕** | Close all open positions / cancel all pending orders |

!!! warning "Close All confirmation"
    By default, the **✕** bulk close button requires a **double-click** to execute.
    The first click arms the button (it turns amber), the second click confirms.
    You can disable this in the EA properties with `InpConfirmCloseAll = false`.

---

## Netting Ladder

When a Netting Ladder is active on a position, the **TP column** shows the
**next rung price** instead of the broker TP, with a **▸** indicator.
This lets you track exactly which partial close will execute next.

---

## Closing the panel

Click the **✕** button in the panel header to close the Order List.
Filters, selected symbol and view tab are saved and restored automatically.
