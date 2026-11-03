# Milk Run

A night-friendly feed tracker for iPhone: time each breast, log bottle top-ups and nappies, see when the next feed is due, and get a push alert when it is.

**Live app:** https://cybersecdigestdaily.github.io/milkrun/

## Set up a phone

1. Open the link in Safari, tap **Share**, then **Add to Home Screen**. Open Milk Run from the Home Screen.
2. First phone: tap **Start tracking**. Second phone: open the invite from Settings → Partner → **Share invite** on the first phone, or paste the code on the welcome screen.
3. Alerts: install **ntfy** from the App Store, tap **+**, paste the topic from Settings → Phone alerts, and subscribe. Allow notifications, including Time Sensitive. Tap **Send a test alert** to check.

## How it works

- Single-file web app (`index.html`), no build step and no dependencies. Works offline via `sw.js`.
- Entries live in each phone's local storage.
- Phones sync through [ntfy.sh](https://ntfy.sh) as a relay. Each sync message is an AES-GCM-encrypted snapshot of recent entries. The key comes from the family code, which never leaves the phones, so ntfy only sees ciphertext.
- Alerts are scheduled ntfy messages with a sequence ID. Logging a new feed replaces the pending alert; starting a feed cancels it.
- Next feed = start of the last feed + the interval in Settings (default 3 hours). You can switch to counting from the end of the feed.

## Limits

- ntfy.sh's free tier allows 250 messages a day per connection. Normal use is roughly 60–100.
- iPhone notifications follow the ring/silent switch. For a wake-up that rings on silent, use the optional Set alarm button (an iOS Shortcut that creates a Clock alarm).
