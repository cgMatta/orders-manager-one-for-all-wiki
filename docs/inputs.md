# Configuration Reference

All EA settings are accessible via **MT5 → EA Properties** (press `F7` on the chart).
Settings are organized in 6 sections, each identified by a prefix.

---

## [GC] General Configuration

Core settings that affect the overall behavior of the EA.

---

### `InpLanguage` — Panel interface language

**Default:** `LANG_EN`  
**Valid values:** `LANG_EN`, `LANG_ES`, `LANG_PT`, `LANG_RU`

Sets the language used across all three panels (Main Panel, Easy Order, Order List).
You can also change the language at any time directly from the Main Panel under
**OPTIONS → GENERAL** using the `[EN]` `[ES]` `[PT]` `[RU]` toggle buttons —
no restart required. This setting defines the language shown on first launch.

---

### `InpMagicNumber` — EA magic number

**Default:** `202600185`  
**Valid values:** Any positive integer

A unique numeric identifier the EA stamps on every order it places. MT5 uses this
number to distinguish orders from different EAs or manual trades.

!!! warning "Important"
    If you run more than one EA on the same account, each one must have a **different**
    magic number. Duplicate magic numbers cause EAs to interfere with each other's
    orders.

---

### `InpUpdateMs` — Panel refresh interval

**Default:** `250`  
**Valid values:** `100` – `1000` (milliseconds)

Controls how often the panels refresh their data (prices, P&L, positions).
Lower values make the panels feel more responsive but use more CPU.

| Value | Feel |
|-------|------|
| `100` | Very smooth, higher CPU usage |
| `250` | Recommended — good balance |
| `500` | Slightly delayed but very light |

---

## [TB] Trade Badges

Badges are visual overlays drawn directly on the chart next to each SL, TP and
Entry line. They show price level, distance in points, R:R ratio, and quick
action buttons (+SL, +TP, close) for every open position and pending order.

---

### `InpShowBadges` — Enable badges

**Default:** `true`  
**Valid values:** `true`, `false`

Master switch for all chart badges. Set to `false` if you prefer a clean chart
without overlays. You can toggle this at any time by reloading the EA properties.

---

### `InpBadgeSLAtr` — ATR multiplier for +SL button

**Default:** `1.5`  
**Valid values:** Any positive decimal (e.g. `1.0`, `1.5`, `2.0`, `3.0`)

When you click the **+SL** quick-action button on a badge, the EA automatically
places the SL at a distance of `N × ATR(14)` from the current price. ATR(14) is
the Average True Range over the last 14 candles on the current timeframe.

**Example:** If ATR(14) = 20 pts and `InpBadgeSLAtr = 1.5`, the SL is placed
20 × 1.5 = **30 pts** from the current price.

!!! tip
    Use a smaller multiplier (e.g. `1.0`) for tight SLs on low-volatility instruments,
    and a larger one (e.g. `2.5`) for volatile instruments like Gold or indices.

---

### `InpBadgeTPAtr` — ATR multiplier for +TP button

**Default:** `2.5`  
**Valid values:** Any positive decimal (e.g. `1.5`, `2.5`, `3.0`)

Same logic as `InpBadgeSLAtr` but applied to the **+TP** button.
Setting this higher than `InpBadgeSLAtr` ensures a positive R:R by default
(e.g. SL at 1.5× ATR, TP at 2.5× ATR = R:R of ~1:1.67).

---

### Color inputs — `InpTBColor*`

Eight color parameters control the appearance of badge and line colors, split
by direction (BUY/SELL) and order state (open position / pending order).

| Parameter | What it colors |
|-----------|---------------|
| `InpTBColorEntryBuy` | Entry badge and line — BUY open position |
| `InpTBColorEntrySell` | Entry badge and line — SELL open position |
| `InpTBColorEntryBuyPending` | Entry badge and line — BUY pending order |
| `InpTBColorEntrySellPending` | Entry badge and line — SELL pending order |
| `InpTBColorSL` | SL badge and line — open position |
| `InpTBColorSLPending` | SL badge and line — pending order |
| `InpTBColorTP` | TP badge and line — open position |
| `InpTBColorTPPending` | TP badge and line — pending order |

!!! tip
    Separating open position colors from pending order colors lets you distinguish
    at a glance which levels are active and which are still waiting to trigger.

---

## [EO] Easy Order Interface

Settings for the **Easy Order** panel, which handles visual order placement using
draggable SL/TP/Entry lines on the chart.

---

### `InpFeedbackMs` — Confirmation message duration

**Default:** `250`  
**Valid values:** `500` – `5000` (milliseconds)

After placing an order, the EA shows a brief confirmation at the bottom of the
Easy Order panel — a green **✓ Order placed** or red **✗ Error - see log**.
This setting controls how many milliseconds that message stays visible before
returning to the normal placement button.

| Value | Feel |
|-------|------|
| `500` | Quick flash |
| `1500` | Comfortable reading time (recommended) |
| `3000` | Stays visible for 3 seconds |

---

### `InpShowStopsZone` — Show minimum stops zone

**Default:** `false`  
**Valid values:** `true`, `false`

When enabled, the EA draws a shaded zone on the chart showing the broker's
minimum allowed distance for SL and TP from the current price. Any SL or TP
placed inside this zone will be rejected by the broker.

!!! tip
    Enable this when trading instruments with wide minimum stop requirements
    (e.g. some CFDs or exotic pairs) to avoid placement errors.

---

### `InpSLTPBufferPts` — Extra buffer over broker minimum stops

**Default:** `0`  
**Valid values:** `0` – `50` (points)

Adds extra points on top of the broker's minimum SL/TP distance. The EA uses
this buffer when calculating whether your lines are in a valid position.

!!! warning "When to use this"
    If you frequently see **"Invalid stops"** errors when placing orders (MT5
    error 10016), increase this value in small steps (try `3` or `5`). This
    happens when the broker's minimum stop distance changes rapidly during
    high volatility and the EA's calculation becomes slightly outdated.

---

### `InpMaxSlippagePts` — Maximum allowed slippage

**Default:** `0`  
**Valid values:** `0` – `100` (points), `0` = disabled

Protects against price moving significantly between when you click **Place Order**
and when the broker executes it. If the price moves more than this many points
during that window, the order is **aborted** and an error is shown.

| Value | Behavior |
|-------|----------|
| `0` | No check — order always executes regardless of slippage |
| `5` | Aborts if price moves more than 5 pts before execution |
| `10` | More tolerant — suitable for slower connections |

!!! tip
    Leave at `0` for most cases. Enable it (e.g. `5`–`10` pts) when trading
    during high-impact news events where price can spike unpredictably.

---

### `InpEOLabelsRight` — Label position on chart lines

**Default:** `true`  
**Valid values:** `true` (right), `false` (left)

Controls which side of the chart the SL/TP/Entry line labels appear on.

- `true` — labels appear on the **right** side (near the price axis)
- `false` — labels appear on the **left** side

Change this if the labels overlap with your chart indicators or price action
on either side.

---

### `InpEOBadgeFontPt` — Badge font size

**Default:** `0`  
**Valid values:** `0` (auto), or any positive integer (e.g. `8`, `10`, `12`)

Font size in points for the text inside the EO badges on the chart.  
`0` = automatic — the EA picks the best size based on your current chart zoom
level. Set a fixed value if you want consistent badge size regardless of zoom.

---

### `InpEOLineStyle` — Line style

**Default:** `STYLE_DOT`  
**Valid values:** `STYLE_SOLID`, `STYLE_DASH`, `STYLE_DOT`, `STYLE_DASHDOT`, `STYLE_DASHDOTDOT`

Visual style of the draggable SL/TP/Entry lines drawn on the chart.

!!! warning
    Non-solid styles (`STYLE_DASH`, `STYLE_DOT`, etc.) only render correctly
    when `InpEOLineWidth` is set to `1`. With higher widths, MT5 forces all
    lines to appear solid regardless of this setting.

---

### `InpEOLineWidth` — Line width

**Default:** `1`  
**Valid values:** `1` – `5`

Thickness of the SL/TP/Entry lines in pixels. `1` is the thinnest, `5` the
thickest. See the note in `InpEOLineStyle` about non-solid styles.

---

### `InpEOFontScale` — Label font scale

**Default:** `1.2`  
**Valid values:** `0.7` – `2.0`

Scales the font size of the text labels displayed on the SL/TP/Entry lines.
This affects readability when your chart is small or zoomed out.

| Value | Use case |
|-------|----------|
| `0.7` | Compact — fits many labels on a small chart |
| `1.0` | Normal size |
| `1.2` | Slightly larger (default) |
| `1.5` | Large — easier to read on high-resolution monitors |

---

### Color inputs — `InpEOColor*`

Eight color parameters for the Easy Order lines and badges on the chart,
organized by line type and trade direction.

| Parameter | What it colors |
|-----------|---------------|
| `InpEOColorSlBuy` | SL line and badge for BUY orders |
| `InpEOColorSlSell` | SL line and badge for SELL orders |
| `InpEOColorTpBuy` | TP line and badge for BUY orders |
| `InpEOColorTpSell` | TP line and badge for SELL orders |
| `InpEOColorEntBuy` | Entry line and badge for BUY orders |
| `InpEOColorEntSell` | Entry line and badge for SELL orders |
| `InpEOColorInvalid` | Any line dragged to an invalid position (e.g. SL above price on a BUY) |
| `InpEODirBtnColor` | The BUY ↔ SELL direction toggle button in the panel |

---

## [OC] One-Click Mode

Settings for the **One-Click** sub-mode of Easy Order, which lets you place
instant market orders with a single click using pre-configured volume and stops.

---

### `InpOCDefaultVolume` — Default lot size

**Default:** `0.01`  
**Valid values:** Any valid lot size for your broker (e.g. `0.01`, `0.1`, `1.0`)

The lot size pre-filled when you open One-Click mode. You can change it
directly in the panel before clicking BUY or SELL — this setting only
controls the initial value shown.

---

### `InpOCDefaultSL` — Default Stop Loss distance

**Default:** `10.0`  
**Valid values:** Any positive number in points

Distance of the Stop Loss from the entry price in points, pre-filled when
opening One-Click mode.

**Example:** On EURUSD with 5-digit pricing, `10` points = 1 pip.

---

### `InpOCDefaultTP` — Default Take Profit distance

**Default:** `20.0`  
**Valid values:** Any positive number in points

Distance of the Take Profit from the entry price in points, pre-filled when
opening One-Click mode. The default `20.0` with `InpOCDefaultSL = 10.0`
gives an initial R:R of 1:2.

---

## [MP] Main Panel Interface

---

### `InpPanelFontScale` — Main panel font scale

**Default:** `1.05`  
**Valid values:** `0.8` – `2.0`

Scales the font size of all text in the Main Panel. Increase this on
high-resolution or large monitors; decrease it if the panel feels too large
on a small screen.

| Value | Use case |
|-------|----------|
| `1.0` | Normal size |
| `1.05` | Slightly larger (default) |
| `1.3` | Comfortable for 2K monitors |
| `1.5` | Large — for 4K or accessibility |

---

## [LO] Order List Interface

Settings for the **Order List** panel, which shows all open positions and
pending orders with live P&L, risk and quick action buttons.

---

### `InpListFontScale` — Order List font scale

**Default:** `1.2`  
**Valid values:** `0.8` – `2.0`

Scales the font size of the Order List panel independently from the Main Panel.
Useful if you want the list to be more readable without making the main panel larger.

---

### `InpNearPct` — Price proximity threshold

**Default:** `0.0015`  
**Valid values:** `0.0005` – `0.01` (as a decimal percentage)

Controls when an SL, TP or Entry badge is highlighted as **"near price"** in
the Order List. When the current price is within this percentage distance of
a level, that level is visually highlighted to warn you it may be hit soon.

| Value | Meaning |
|-------|---------|
| `0.0005` | Alert when price is within 0.05% of the level |
| `0.0015` | Alert when price is within 0.15% (default) |
| `0.003` | Alert when price is within 0.30% |

!!! tip
    Use a smaller value for tight scalping strategies and a larger value for
    swing trading where price typically has more room to move.

---

### `InpConfirmCloseAll` — Double-click confirmation for Close All

**Default:** `true`  
**Valid values:** `true`, `false`

When `true`, the **Close All** button requires two clicks to execute —
the first click arms it, the second confirms. This prevents accidentally
closing all your positions with a single misclick.

!!! warning
    Setting this to `false` means a single click immediately closes **all**
    open positions and pending orders. Use with caution.

---

### `InpSoundBulkClose` — Sound on Close All

**Default:** `true`  
**Valid values:** `true`, `false`

Plays an audio alert when the **Close All** action is executed. Useful as
an audible confirmation that all positions have been closed, especially
when monitoring multiple charts.

---

### `InpSoundClose` — Sound on individual order close

**Default:** `true`  
**Valid values:** `true`, `false`

Plays an audio alert each time a single position or pending order is closed
via the Order List action buttons (the × close button on each row).
