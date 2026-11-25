# ExoDial

A personal calling app built on an Exotel virtual number (ExoPhone). It looks and feels like the iPhone dialer, runs in the browser, and can be added to the iPhone home screen.

**Live app:** https://jatin-savaliya.github.io/exodial/

## What it does

- **Inbound** - calls to your ExoPhone ring your personal number. Telegram tells you who is calling (from your contacts), and sends missed-call alerts and the call recording after the call.
- **Outbound** - tap Call on any contact. The iPhone dialer calls your ExoPhone and Exotel connects the contact, who sees your ExoPhone as the caller ID. On a laptop, Exotel rings your phone first, then the contact.
- **Recents** - all calls with duration, missed-call filter and playable recordings.
- **Favourites, Contacts and Keypad** - iOS-style screens. Contacts are imported from an iPhone `.vcf` export.
- **Multi-user** - each user has their own ExoPhone, contacts, call history and Telegram alerts.

## How it works

| Part | Tool | Role |
|---|---|---|
| App | GitHub Pages | Static web app (`index.html`), no build step |
| Login + database | Supabase | Users, profiles, contacts, call logs, call requests |
| Backend | Supabase Edge Functions | `exodial-incoming` (Exotel flow webhooks + "dial whom"), `exodial-outgoing` (calls, call status, recordings) |
| Telephony | Exotel | ExoPhone, call flow, Connect API, recordings |
| Alerts | Telegram bot | Incoming, missed and ended-call messages with recordings |

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app (UI + logic) |
| `manifest.webmanifest` | Name and icon for Add to Home Screen |
| `icon-180.png`, `icon-512.png` | App icons |

## Updating the app

1. Replace the changed file using **Add file → Upload files → Commit changes**.
2. GitHub Pages publishes it in about a minute.

## Security notes

- The Supabase key in `index.html` is the **publishable** key. It is meant to be public; data is protected by login and row-level security.
- Exotel API credentials, the Telegram bot token and the webhook key live only in **Supabase secrets**. Never commit them to this repo.

## Using it on iPhone

Open the live link in Safari → sign in → Share → **Add to Home Screen** (optional).
