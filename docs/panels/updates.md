# Updates & Versioning

## How updates work on MQL5 Marketplace

Orders Manager One For All is distributed through the **MQL5 Marketplace**.
Updates are not applied automatically — here is how the process works for both
sellers and buyers.

---

## For users: how to update

When a new version is available, MetaTrader 5 notifies you directly inside
the terminal with a notification badge.

To apply the update:

1. In MT5, go to **Tools → Market** (or click the **Market** tab)
2. Navigate to **My Purchases**
3. Find **Orders Manager One For All** and click **Update**
4. The new `.ex5` file is downloaded and replaces the previous version automatically

!!! warning "Reload required"
    If the EA is already loaded on a chart when you update, you need to **remove
    and re-add it** to the chart for the new version to take effect. MT5 does not
    hot-reload running EAs.

!!! tip "Stay informed"
    Subscribe to the [Telegram Channel](https://t.me/OrdersManagerOneForAllUpdates)
    for update announcements with a summary of what changed before you update.

---

## Update channels

| Channel | Purpose |
|---------|---------|
| 📢 [Telegram Channel](https://t.me/OrdersManagerOneForAllUpdates) | Announcements for every new version |
| 📖 [Changelog](changelog.md) | Full list of changes per version |
| 💬 [Telegram Group](https://t.me/OrdersManagerOneForAllSupport) | Questions about updates or compatibility |

---

## Version numbering

The EA follows this versioning pattern:

- **v1.x** — current series (incremental improvements and fixes)
- The version is visible in the **Common tab** of the EA Properties window (press `F7`)
  and in the **panel header** tooltip

---

## Checking your current version

Two ways to check which version you have installed:

1. **EA Properties** — right-click the chart → Expert Advisors → Properties (or press `F7`)
   → Common tab. The version appears in the description block.

2. **Diagnostics button** — click **[Diagnostics]** in OPTIONS → the first line of
   the Journal output shows the exact version, build date and magic number.

---

## Compatibility between versions

Settings and panel state are saved automatically via MT5 GlobalVariables. They
persist across version updates — you do not need to reconfigure the EA after
updating.

If a new version changes the input parameters (adds, removes or renames inputs),
MT5 will show the Properties window automatically on first load so you can review
and confirm the new defaults.

---

## Frequently asked questions about updates

### Will an update break my active positions?

No. The EA does not hold positions — it is a trading panel. Updating while
positions are open is safe; the positions remain with the broker regardless
of whether the EA is running.

### What happens to my Netting Ladders after an update?

Netting Ladder state is persisted to disk in `MQL5/Files/EO_netting/`. As long
as the file format has not changed between versions (noted in the changelog when
it does), ladders survive updates and are reloaded automatically.

### Can I roll back to a previous version?

MQL5 Marketplace does not provide rollback through the UI. If you need a previous
version for any reason, contact support via the
[Telegram Group](https://t.me/OrdersManagerOneForAllSupport).
