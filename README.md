# Milk Run

A night-friendly feed and nappy tracker for iPhone: log bottle feeds and nappies with exact amounts and times, see when the next feed is due, and get a push alert when it is.

**Live app:** https://cybersecdigestdaily.github.io/milkrun/

## Set up a phone

1. Open the link in Safari, tap **Share**, then **Add to Home Screen**. Open Milk Run from the Home Screen.
2. First phone: tap **Start tracking**. Second phone: open the invite from Settings → Partner → **Share invite** on the first phone, or paste the code on the welcome screen.
3. Alerts: install **ntfy** from the App Store, tap **+**, paste the topic from Settings → Phone alerts, and subscribe. Allow notifications, including Time Sensitive. Tap **Send a test alert** to check.

## What it does

- **Feed:** type the exact amount in ml, or tap a preset. Choose formula or expressed milk, and set the exact date and time. It shows the Kendamil scoop count for multiples of 30 ml.
- **Nappy:** wet, dirty, wet and dirty, or clean and dry (a check with nothing to change), with an exact date and time.
- **Home:** the next feed time (last feed + the interval in Settings, default 3 hours), the nappy check due, and the last 24 hours at a glance.
- **Navigation:** a tab bar for Home, History and Settings. A swipe from the left edge also goes back Home.
- **History:** tap any entry to change or delete it. Every save can be undone.

## Archived: breastfeeding timer

The left/right breastfeeding timer from version 1.0 is removed for now. The full version is preserved at commit [`51b6874`](https://github.com/CyberSecDigestDaily/milkrun/tree/51b68746f66d1a818c391e769501e046ff4eb9ee). Breastfeeds logged with it still show in History, and their side times are kept.

## How it works

- Single-file web app (`index.html`), no build step and no dependencies. Works offline via `sw.js`.
- Entries live in each phone's local storage.
- Phones sync through [ntfy.sh](https://ntfy.sh) as a relay. Each sync message is an AES-GCM-encrypted snapshot of recent entries. The key comes from the family code, which never leaves the phones, so ntfy only sees ciphertext.
- Alerts are scheduled ntfy messages with a sequence ID. Logging a new feed replaces the pending alert.

## Limits

- ntfy.sh's free tier allows 250 messages a day per connection. Normal use is roughly 40–80.
- iPhone notifications follow the ring/silent switch. For a wake-up that rings on silent, use the optional Set alarm button (an iOS Shortcut that creates a Clock alarm).
