# Changelog

All notable features and important fixes for **Orders Manager One For All**.

---

## v1.88

**Feature: Diagnostics button**

New **[Diagnostics]** button at the bottom of the OPTIONS section in the Main Panel.
Click it to print a full troubleshooting snapshot to the MT5 Journal/Experts tab,
including EA state, account type, symbol info, MT5 build, all open positions
(with type, lots, entry, SL, TP, P&L), pending orders, and active Netting Ladders.
Sensitive financial data (balance, equity, margin, login) is intentionally excluded
so the output can be shared safely with support.

To save or share the log: in the Experts tab, right-click a row → **Open** to view
the full log file, or select rows and use **Copy** to paste into a support message.

**Improvement: Full English translation of all internal messages**

All internal messages, warnings and feedback strings are now in English across all
modules. Fixes also apply to user-visible UI strings that were not yet going through
the translation system (`TR()`), including order list pagination and runner leg labels.

**Fix: Three panel buttons silently unresponsive**

The hit detection array in the Main Panel had a hard limit of 16 slots. With 19
buttons registered, the last three (`Diagnostics`, `Include Commissions in Risk`,
and the `Reverse Mode` toggle) were silently dropped and never responded to hover
or click. Array increased to 24 slots.

**Fix: Easy Order and Order List sections misaligned in OPTIONS**

When the language toggle row was added to the GENERAL card in a previous version,
the vertical positions of the Easy Order and Order List sub-sections were not
updated to match. This caused both sections to overlap with the GENERAL card.
Layout formulas corrected.

---

## v1.87

**Fix: Wiki help button [?] opens URL in panel**

New `[?]` button in the Main Panel header. Clicking it displays the wiki URL
in an MT5 alert popup and prints it to the Journal for easy copying.

**Fix: NettingLadder file isolation and input validation**

Ladder persistence files moved from `MQL5/Files/` root to `MQL5/Files/EO_netting/`
subdirectory. Added range validation when loading files to reject corrupt or
manually edited data.

**Improvement: EA renamed to "Orders Manager One For All"**

File, EA name constant, and panel header updated to reflect the official product name.

---

## v1.85

**Improvement: Input settings reorganized**

All EA input parameters are now organized into 6 clearly labeled sections
(`[GC]`, `[TB]`, `[EO]`, `[OC]`, `[MP]`, `[LO]`), making the Properties window
easier to navigate. All descriptions rewritten in English.

---

## v1.84

**Feature: Portuguese (PT-BR) and Russian language support**

Added Portuguese (Brazil) and Russian to the multi-language system.
The language toggle in the panel now shows `[EN]` `[ES]` `[PT]` `[RU]`.

---

## v1.83

**Feature: Multi-language interface (EN / ES)**

The full panel UI (Main Panel, Easy Order, Order List) can now be switched
between English and Spanish in real time. Language preference persists across
MT5 restarts. Toggle available in **OPTIONS → GENERAL**.

---

## v1.82

**Fix: Chart objects left behind after removing the EA**

When the EA was removed while the Easy Order panel was open, draggable lines
and input fields could remain visible on the chart. This has been fully resolved
with a three-layer cleanup on EA removal.

---

## v1.81

**Fix: Incorrect lot volume display on instruments with small volume step**

On instruments like BTCUSD where the broker's minimum volume step is `0.001`,
the lot field was showing `0.00` instead of the correct value. The display now
adapts its decimal precision to the instrument's volume step.

---

## v1.80

**Feature: Slippage protection for market orders**

New `InpMaxSlippagePts` input. When set, the EA checks the price movement
between order calculation and execution — if the price moves more than the
allowed threshold, the order is aborted and a warning is shown in the panel.
Set to `0` to disable (default).

---

## v1.72

**Improvement: Netting Ladder stability and persistence**

Intermediate TP rungs now survive MT5 restarts and symbol changes.
Added desync detection: if the user manually edits the broker TP,
the ladder detects the change and resyncs automatically.

---

## v1.70

**Feature: Synthetic Netting Ladder (multi-TP for Netting accounts)**

Netting accounts only allow one position per symbol, so multi-TP is implemented
via automatic partial closes. The EA monitors the position and executes each
rung at the right price. The Order List shows the next active rung in the TP
column. Intermediate rung badges are shown on the chart alongside the main TP badge.

---

## v1.63

**Improvement: R:R moved from Entry badge to TP badge**

The Risk:Reward ratio is now displayed on the TP badge (where it makes more
sense) instead of the Entry badge. The TP badge also shows estimated profit.
R:R updates live while dragging the TP line on the chart.

---

## v1.60

**Feature: Multi-TP support — up to 4 Take Profits per order (Hedging)**

On Hedging accounts, you can now set up to 4 independent Take Profit levels,
each with its own percentage allocation of the total volume. Each TP leg is
sent as a separate position with its own badge on the chart.
The TP % fields auto-redistribute when you toggle legs on or off.

---

## v1.56

**Improvement: Panels auto-scale to chart width**

All three panels now adapt their font and layout scale to the actual chart
window size at startup, preventing overflow or truncation on narrow charts.

---

## v1.54

**Feature: Order type filter in the Order List**

A new dropdown next to the view tabs lets you filter by order type:
All, Buy, Sell, Buy Limit, Sell Limit, Buy Stop, Sell Stop.
The filter resets automatically when switching between Open / Pending / All tabs.
Bulk actions (close, partial close, breakeven) respect the active filter.

---

## v1.43

**Feature: Multi-symbol filter in the Order List**

A symbol dropdown in the Order List lets you view and manage positions and
orders across all symbols from a single panel, not just the chart's symbol.
Bulk actions apply only to the selected symbol (or all symbols if "All" is chosen).
The selected symbol is saved and restored across MT5 restarts.

---

## v1.27

**Feature: One-Click mode in Easy Order**

A new mode that lets you place instant market orders with a single click using
predefined volume, SL and TP. Includes `[−]` / `[+]` volume buttons, Volume Step
selector, and the same feedback flash as Manual mode.

---

## v1.22

**Feature: Reverse Mode for Breakeven (SL placement option)**

When using the Breakeven action, you can now choose between two behaviors:
- **SL at original distance** — mirrors the SL symmetrically past entry
- **SL at original entry** — moves SL exactly to the entry price

Toggle available in **OPTIONS → ORDER LIST**.

---

## v1.20

**Feature: Trade Badges — chart overlays for every position**

Visual badges appear on the right side of the chart for each open position
and pending order, showing Entry price, SL and TP with estimated P&L,
lot size and R:R. Quick action buttons (+SL, +TP) place levels automatically
using ATR-based distance. Badge colors and sizes are fully configurable.

---

## v1.18

**Feature: Bulk actions in the Order List**

New action buttons in the Order List header: close all (with optional double-click
confirmation), partial close at 25% / 50% / 75%, and breakeven all — applied to
all visible positions in the active filter.

---

## v1.14

**Feature: Mini menu when the panel is minimized**

When the Main Panel is minimized to its FAB button, a compact mini menu appears
with quick access to the Easy Order and Order List panels — no need to expand
the panel first.

---

## v1.12

**Feature: Account type display (Hedging / Netting)**

The account card in the Main Panel now shows the account margin mode
(Hedging or Netting), making it easy to confirm which mode is active
before placing orders.

---

## v1.07

**Feature: OPTIONS section collapse / expand with animation**

The OPTIONS section in the Main Panel can now be collapsed to save screen space,
with a smooth animated transition. The collapsed/expanded state persists across
MT5 restarts.

---

## v1.06

**Feature: Full session persistence**

All panel settings (language, toggles, EasyOrder configuration, selected tabs,
panel positions, collapsed sections) are now saved and restored automatically
across MT5 restarts, timeframe changes and EA reloads.

---

## v1.01

**Improvement: Order List Panel rewritten with CCanvas**

The Order List was rebuilt from scratch using a single CCanvas bitmap, replacing
dozens of individual MT5 objects. Result: zero flickering, instant drag, lower
CPU usage and support for hover effects and pixel-precise layouts.

---

## v0.17

**Feature: Animated minimize button (FAB)**

The minimize button animates between its header position (expanded) and a
floating action button position (minimized), with a smooth easing transition.

---

## v0.16

**Feature: Minimize / maximize with curtain animation**

The Main Panel can be minimized to a single floating button with a smooth
curtain animation (ease-out cubic). Expand is faster than minimize for
snappier UX.

---

## v0.14

**Feature: UIPanel and EasyOrder migrated to CCanvas**

Both panels rebuilt using CCanvas bitmaps — eliminating flickering caused by
individual MT5 objects. DPI-aware scaling, smooth hover effects and
pixel-precise layout are now possible. EasyOrder lines are also badged
with CCanvas overlays showing lot size, R:R and risk amount.

---

## v0.7

**Feature: Easy Order panel with draggable SL / TP / Entry lines**

The Easy Order panel lets you place orders by dragging SL, TP and Entry lines
directly on the chart. Risk is calculated automatically based on your chosen
mode (% of balance, fixed amount, or manual lots). Orders can be placed as
Market, Limit or Stop.

---

## v0.6

**Feature: Individual position management**

Each open position now has its own row in the Main Panel with close buttons
(25% / 50% / 75% / full close), entry price, SL, TP and individual P&L.

---

## v0.5

**Feature: Quick actions — Close All, Breakeven, Partial Close**

Added **Close All** (with optional include pending orders toggle),
**BE All** (move all SLs to breakeven, with optional commission offset),
and **25% / 50% / 75%** partial close buttons.

---

## v0.2

**Feature: Risk-based lot size calculation**

The EA automatically calculates the correct lot size from a percentage of
balance (or equity / free margin), SL distance and instrument type.
Supports Forex, indices, metals, crypto and all account types including cent accounts.

---

## v0.1

**Initial release**

Core EA structure with Main Panel (account info, position summary, quick actions),
dark theme UI, OnTimer-based refresh and OnTradeTransaction for instant updates.
