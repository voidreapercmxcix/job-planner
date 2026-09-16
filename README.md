# job-planner

A daily job planner and money tracker for vehicle delivery drivers. Built for trade-plate and driven-delivery work, where every job has a collection window, a delivery window, a long drive in between, and a train home afterwards.

It runs on your phone, works with no signal, and keeps everything on the phone. There is no account, no server and no subscription.

## What it does

**Plans your day.** Jobs sit on a board in three columns: To collect, On board, Delivered. A strip along the top shows which days have work, so you can see tomorrow at a glance.

**Reads jobs from your jobs app.** Copy a job, tap Paste job, and the reg, vehicle, both addresses, both windows, mileage, drive time, job ref and pay are filled in for you to check.

**Keeps your plan separate from the window.** The collection and delivery windows are what you're allowed. Your planned times are what you'll actually do. The app warns you if a plan falls outside its window, if you've left less drive time than the job needs, or if you're cutting it fine before a window closes.

**Puts reminders in your calendar.** One tap adds your planned collection, planned delivery and window-closing reminders to the phone's calendar, with the address on the alert.

**Tracks the money.** Log expenses against each job as you go (train, bus, taxi, fuel, tolls, parking, food). The Money view shows earned, spent, net, miles and jobs for this week, last week, this month, the tax year or all time, with charts of earnings over time and where the expenses go. Export the period to CSV for self-assessment.

**Handles jobs that go wrong.** Cancel or abort a job with a reason and any partial payment. It leaves the board but stays in the money, with its expenses.

## Installing it on your phone

You need the app served from an HTTPS address once. After that it's cached on the phone and works offline.

1. Create a free GitHub account if you don't have one.
2. Create a new public repository and upload these files: `index.html`, `sw.js`, `manifest.json`, `icon.svg`.
3. In the repository's Settings, open Pages, set Source to "Deploy from a branch", choose `main` and `/ (root)`, and save.
4. After a minute or two your app is at `https://YOUR-USERNAME.github.io/REPO-NAME/`.
5. Open that address on your phone and choose Add to Home Screen from the browser menu.

Android works fully. iPhone can install it too, but iOS is stricter about web apps, so calendar import and offline behaviour may need a little more patience.

## Using it

**Add a job** with the + button, or Paste job to read one from your jobs app. Set your planned collection and delivery times; the day view and reminders are based on those, not the windows.

**Move a job along** with the big button on its card: Collected, then Delivered.

**Calendar** on a card creates a calendar file with the reminders. Open it and your calendar app adds the events. If you change a planned time later and add it again, the calendar will create a second entry, because phones don't let web apps edit calendar events; delete the old one by hand.

**Edit** opens the full job, including expenses and the Cancel / Abort buttons.

**Money** in the header switches to the money view. Tap a period, tap a row to open the job, or export the period to CSV.

**⋯ menu** has backup and restore. Everything lives on this phone only, so take a backup file now and then and keep it somewhere safe. Restoring on a new phone brings it all back.

## Paste format

The parser is tolerant, but it was tuned on this layout:

```
NV73OCL
Driven Insured
IVECO DAILY 35S14B
Flex-E-Rent Edinburgh, 1 Drovers Road, Broxburn, 0, Edinburgh, EH52 5ND
 Mon, 14th Sep 11:00 - Wed, 16th Sep 15:00
7 hrs 1 min   330 miles
Hudson Kapel Worcester, Church Lane, Norton, -, Worcester, WR5 2PR
 Tue, 15th Sep 08:00 - Thu, 17th Sep 12:00
J-A945-98DF
£181.43 Total
```

It looks for a UK reg, lines containing a postcode (first is collection, second is delivery), date-times in order (collection open, collection close, delivery open, delivery close), a miles figure, an hours figure, a `J-` style reference and a `£` amount. Placeholder fields like `0` and `-` are dropped. If your jobs app lays things out differently, the fields it misses can be typed in.

## Privacy

Your jobs, addresses, earnings and expenses are stored in the phone's browser storage and never leave the phone. The GitHub repository only holds the app's code, which contains no personal data. Nobody can see your jobs by finding the address of the app.

The flip side: if you clear the browser's site data or uninstall without a backup, the jobs are gone. Use the backup button.

## Updating

When a new `index.html` (and usually `sw.js`) is released, upload them to the repository over the old ones and commit. On the phone, close the app fully and open it twice with signal. The first open fetches the new version, the second runs it.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app: layout, logic, parser, charts |
| `sw.js` | Service worker that caches the app for offline use |
| `manifest.json` | Tells the phone how to install it as an app |
| `icon.svg` | Home-screen icon |

## Roadmap

- Native Android build with real alarms, so reminders don't depend on the calendar
- Better handling of other jobs apps' paste layouts
- Optional mileage rate for drivers using their own vehicle between jobs

## Licence

MIT. Use it, change it, share it with the people you work with.
