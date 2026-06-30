# Easy Order Panel

The Easy Order panel handles order placement. It has two modes:
**Manual** (draggable lines on the chart) and **One-Click** (instant market orders).
Toggle between modes using the button in the panel header.

---

## Manual Mode

### Step 1 — Configure your order

**Direction:** Select **BUY** or **SELL**.

**Order type:** Select **Market**, **Limit** or **Stop**.

**Risk mode:** Choose how the lot size is calculated:

| Mode | Description |
|------|-------------|
| **%** | Percentage of your account balance / equity / free margin |
| **LOT** | Fixed lot size entered manually |
| **USD** | Fixed monetary amount |

**Risk Basis:** Applies when using **%** mode — choose whether to calculate
from **Balance**, **Equity** or **Free Margin**.

---

### Step 2 — Activate lines

Click **Activate lines** to draw the SL, TP and Entry lines on the chart.
Drag each line to your desired price level. The panel updates in real time
showing estimated lots, risk amount and R:R.

!!! tip
    You can also drag the SL and TP directly from the **Trade Badges** on
    the chart after a position is open.

---

### Step 3 — Set Take Profits

Up to **4 Take Profit levels** are available. Each TP can be assigned a
percentage of the total volume.

- Click a **TP button** (TP1–TP4) to enable or disable that leg
- Enter the **percentage** for each active leg in the field next to the button
- The **Total active TPs** line shows the sum — it cannot exceed 100%
- Leave one leg at 0% to create a **runner** (position with no TP)

!!! note
    On **Netting accounts**, multi-TP is handled automatically via partial closes.
    The setup is identical from the user's perspective.

---

### Step 4 — Place the order

Click **Place Order**. A green ✓ or red ✗ confirmation appears briefly.
If the order is rejected, check the MT5 Journal for details.

---

## One-Click Mode

One-Click mode places instant **market orders** with a single button press.

1. Set your **volume** using the `[−]` / `[+]` buttons or the volume step selector
2. Configure **SL** and **TP** distance in points in the ACTIVATE section
3. Click **BUY** or **SELL** — the order executes immediately

!!! tip
    One-Click mode is ideal for fast entries during volatile moments when
    you don't have time to drag lines on the chart.

---

## Closing the panel

Click the **✕** button in the panel header to close Easy Order.
All your settings (mode, risk, direction, TP configuration) are saved
and restored the next time you open the panel.
