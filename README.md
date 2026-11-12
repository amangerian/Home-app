# The Home App 🏡

A phone-friendly home maintenance tracker that runs in the browser. It keeps track of the recurring jobs that keep a house healthy: testing smoke alarms, changing furnace filters, checking toilet flappers for leaks, cleaning gutters, inspecting the attic, and yard work. The Home screen shows what's overdue and what's coming up.

It is a single `index.html` file with no server, no account and no build step. Data stays on the phone (in the browser's local storage).

## Features

- **161 suggested tasks** in 10 categories: Safety, Heating & Cooling, Plumbing & Water, Electrical, Kitchen & Appliances, Interior, **Attic**, Exterior & Roof, **Yard & Garden**, and Pool & Spa. Each one comes with a short note on why and how to do it.
- **Setup based on your home.** Tick what your home has (lawn, attic, sump pump, septic, furnace, heat pump, pool, freezing winters…) and the app adds only the tasks that apply.
- **Two kinds of schedules, both editable:**
  - *Repeat every N days / weeks / months / years*, optionally limited to certain months. For example, "Mow weekly, Apr–Oct" pauses in winter and starts again in April.
  - *Certain months*: "Clean gutters every April & November", or "Furnace tune-up every September".
- **Multiple items of the same task, each on its own cycle.** Have two furnaces, three toilets, or alarms installed in different years? Add each one as its own item. Each item has its own due date, history, notes (e.g. "filter size 16×25×1") and, if needed, its own schedule. When you add one, a single tap puts it **half a cycle offset** from the first one, so the work is staggered.
- **Custom tasks** with your own name, category, emoji, schedule and notes.
- **One-tap "done"** with undo. You can also record a past date with a note ("replaced flapper"), snooze, or skip a cycle.
- **Year Plan**: a month-by-month view of the next 12 months.
- **Calendar reminders**: export every task (or a single one) as a `.ics` file with repeating events and a 9 AM alert, so the phone's own calendar sends the notifications.
- **Backup & restore** to a JSON file.
- Light and dark mode, a Southern Hemisphere setting (shifts seasonal months by six), and offline use once it's installed.

## Put it on a phone

The easiest way is to host it with **GitHub Pages**:

1. In the repository on GitHub, go to **Settings → Pages**.
2. Under *Build and deployment*, pick **Deploy from a branch**, then choose the branch and the `/ (root)` folder, and save.
3. After a minute it will be live at `https://<your-username>.github.io/Home-app/`.
4. Open that link on the phone, then:
   - **iPhone (Safari):** Share button → **Add to Home Screen**.
   - **Android (Chrome):** ⋮ menu → **Add to Home screen** / **Install app**.

It then opens full-screen like a normal app and works offline.

> **Why install it?** On iPhone, Safari may clear a website's saved data if you don't visit it for several weeks. Apps added to the Home Screen don't have that limit. Either way, use **Settings → Back up to a file** now and then.

You can also just open `index.html` directly. All the main features work from the single file. Installing and offline mode need `manifest.webmanifest`, `sw.js` and `icons/` next to it.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app: UI, styles, the suggested-task library, and logic |
| `manifest.webmanifest` | Lets phones install it as an app |
| `sw.js` | Service worker that adds offline support |
| `icons/` | App icons |

## Editing the suggested tasks

The built-in list is the `LIBRARY` array near the top of the second `<script>` in `index.html`. Each entry looks like this:

```js
{ id:'gutters', cat:'exterior', high:1, name:'Clean gutters & downspouts', s:M(4,11),
  notes:'Clear leaves and debris and flush downspouts…' }
```

- `s:E(1,'m')`: every 1 month (`'d'` days, `'w'` weeks, `'m'` months, `'y'` years)
- `s:E(1,'w',[4,5,6,7,8,9,10])`: weekly, but only April through October
- `s:M(4,11)`: once in April and once in November
- `req:['attic']`: only suggested when the home has that feature
- `high:1`: marked ★ Important

## Sources for the suggested list

The intervals are typical guidance, not hard rules. Always check manufacturer instructions and your local climate.

- [Ramsey Solutions: home maintenance checklist](https://www.ramseysolutions.com/real-estate/home-maintenance)
- [Opendoor: home maintenance checklist](https://www.opendoor.com/w/guides/home-maintenance-checklist)
- [Gardenfrontier: printable home maintenance checklist](https://gardenfrontier.com/home-maintenance-checklist-printable-Gardenfrontier.pdf)
- [HouseLogic: seasonal home maintenance](https://www.houselogic.com/?p=179821)
- [Fannie Mae: homeowner maintenance checklist](https://yourhome.fanniemae.com/media/2131/display)
- [University of Georgia Extension: home maintenance checklist](https://fieldreport.caes.uga.edu/publications/C1082/home-maintenance-checklist/)
- [Bob Vila: month-by-month lawn care calendar](https://www.bobvila.com/articles/month-by-month-lawn-care-calendar/)
- [LawnStarter: lawn care schedule](https://www.lawnstarter.com/blog/lawn-care/lawn-care-schedule/)
- [AAA: home maintenance schedule](https://mwg.aaa.com/via/house-home/home-maintenance-schedule)
- Safety intervals follow NFPA, CPSC and EPA guidance (monthly alarm tests, 10-year smoke alarm replacement, radon retesting every 2 years, annual private-well testing, septic inspection every 3 years).
