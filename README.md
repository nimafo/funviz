# Chat Heatmap for Telegram & WhatsApp

![Heatmaps made](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fabacus.jasoncameron.dev%2Fget%2Fnimafo.github.io%2Ffunviz-heatmaps&query=%24.value&label=heatmaps%20made&color=2da44e)
![Downloads](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fabacus.jasoncameron.dev%2Fget%2Fnimafo.github.io%2Ffunviz-downloads&query=%24.value&label=downloads&color=2f81f7)
![Visits](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fabacus.jasoncameron.dev%2Fget%2Fnimafo.github.io%2Ffunviz-visits&query=%24.value&label=visits&color=6e7781)

Turn a Telegram or WhatsApp chat export into a GitHub-style contribution heatmap: one square per day, coloured by how many messages you exchanged.

**Live:** https://nimafo.github.io/funviz/

**Everything runs in your browser.** Your chat file is never uploaded anywhere.

![Screenshot](docs/screenshot.png)

## Use it

### Telegram
1. Install [Telegram Desktop](https://desktop.telegram.org/). The phone apps can't export.
2. Open a chat → **⋮** (top right) → **Export chat history**.
3. Untick all media, set **Format → Machine-readable JSON**, and set the date range to start from the oldest message.
4. Open [the page](https://nimafo.github.io/funviz/) and drag in `result.json` from `Downloads/Telegram Desktop/ChatExport_…`.

Full-account exports (Settings → Advanced → Export Telegram data) also work, even multi-GB ones. You'll get a dropdown with all your chats.

### WhatsApp
1. Open the chat on your phone.
   - **iPhone:** tap the contact or group name → **Export Chat**
   - **Android:** **⋮** → **More** → **Export chat**
2. Choose **Without media**.
3. Open [the page](https://nimafo.github.io/funviz/) and pick the `.txt` (Android) or `.zip` (iPhone). No need to unzip.

Then pick a colour and a light or dark background, and click **Download PNG**.

## Features

- Telegram JSON (single chat or full-account export) and WhatsApp `.txt` / `.zip`
- **Handles huge files:** the file is streamed in chunks and only dates are extracted, so memory stays around 100 MB even for multi-GB exports (tested with a 1.45 GB, 3.4M-message file in about 7 s)
- WhatsApp date formats are detected automatically (day/month vs month/day, 12h/24h, iPhone and Android, different locales)
- Drag & drop or file picker, plus a demo-data button
- Colour presets and a custom colour picker
- Light / dark background
- Hide empty years, show/hide yearly totals, optionally show the chat name
- Hover a day to see its message count
- Stats: total messages, active days, busiest day, longest streak
- High-resolution PNG export, ready for Twitter/X
- A single static `index.html` with no dependencies and no build step

![Dark mode](docs/screenshot-dark.png)

## Host it on GitHub Pages

1. Create a new repository and push these files.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, then pick `main` and `/ (root)`.
3. Your page will be live at `https://<username>.github.io/<repo>/`.

## How counting works

**Telegram:** only entries with `"type": "message"` are counted, so service events like calls, pins and joins are skipped. **WhatsApp:** only lines with a sender (`Name: text`) are counted. System notices and the encryption notice are skipped, and messages spanning several lines count once. The day comes from the timestamp in the export, which is in your local time. Colour levels are the quartiles of your active days, like GitHub.

## Usage counter

The page keeps three anonymous counts using the free [Abacus](https://abacus.jasoncameron.dev) API: **visits**, **heatmaps made** (a real file loaded, at most once per visit; the demo doesn't count) and **PNG downloads**. Only the counter is incremented. No chat data, names or numbers from your file are ever sent.

The totals are shown at the bottom of the page, and you can also check them directly:

```
https://abacus.jasoncameron.dev/get/nimafo.github.io/funviz-heatmaps
https://abacus.jasoncameron.dev/get/nimafo.github.io/funviz-downloads
https://abacus.jasoncameron.dev/get/nimafo.github.io/funviz-visits
```

The counter is off when the page is opened locally (`file://` or `localhost`), so testing doesn't inflate it.

## License

MIT
