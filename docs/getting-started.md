# Getting Started

## Requirements

Before installing, make sure you have:

- MetaTrader 5 (build 3000 or higher)
- A demo or live account at any broker
- AutoTrading and Algo Trading enabled in MT5

---

## Enabling AutoTrading & Algo Trading

The EA requires both AutoTrading and Algo Trading to be active before placing orders.

**AutoTrading** (toolbar button):

1. In MT5, look at the top toolbar
2. Click the **AutoTrading** button — it turns green when active
3. If it stays grey, check that your broker allows automated trading

**Algo Trading** (per-chart permission):

1. Right-click the chart where the EA is loaded
2. Go to **Expert Advisors → Properties** (or press `F7`)
3. In the **Common** tab, check **Allow Algo Trading**
4. Click OK

!!! warning
    Orders will be rejected if either AutoTrading or Algo Trading is disabled.

---

## Installation

1. Download the compiled EA (`.ex5` file) from the [MQL5 Marketplace](#)
2. Copy it to your MT5 `Experts` folder:
    - In MT5, go to **File → Open Data Folder**
    - Navigate to `MQL5 → Experts`
    - Paste the `.ex5` file there
3. Restart MT5 or right-click the **Navigator** panel and select **Refresh**
4. The EA will appear under **Navigator → Expert Advisors**

---

## Adding the EA to a Chart

1. Open any chart in MT5
2. In the **Navigator** panel, expand **Expert Advisors**
3. Double-click **OrdersManager_All_In_One** or drag it onto the chart
4. The **Properties** window will open — configure your settings and click **OK**
5. The panel will appear on the left side of the chart

!!! tip "Recommended first steps"
    1. Set your preferred language in **OPTIONS → GENERAL** (`[EN]` `[ES]` `[PT]` `[RU]`)
    2. Set your Magic Number in the EA properties (`[GC]` section)
    3. Make sure AutoTrading and Algo Trading are both enabled

---

## Account Types

The EA works on both Hedging and Netting accounts. Multi-TP is supported on both,
adapting automatically to the account type.

| Account Type | Multi-TP | How it works |
|---|---|---|
| Hedging | ✅ Up to 4 TPs | Each TP closes an independent position |
| Netting | ✅ Up to 4 TPs | Intermediate TPs via automatic partial closes |

---

## Compatibility

The EA has been tested on both **Hedging** and **Netting** account types across
multiple brokers and prop firm environments.

!!! warning "Prop firm rules"
    Always verify that your prop firm allows EAs before using this tool
    on a funded account.
