<h1 align="left"><img src="extension/favicon/favicon.svg" width="32" valign="middle" /> Swoosh</h1>

**Your tabs, organized.**

Swoosh replaces your Chrome new tab page with a tab dashboard that groups open tabs by site, surfaces stale ones, and helps you clear the clutter — with a satisfying swoosh.

---

## Install

### Option 1: Download Release (Recommended)
1. Download the latest `Swoosh.zip` from the [Releases page](https://github.com/akshatagrawal22/Swoosh/releases)
2. Unzip the file
3. Go to `chrome://extensions` in Chrome
4. Enable **Developer mode** (top-right toggle)
5. Click **Load unpacked**
6. Select the `extension/` folder from the unzipped directory

### Option 2: From Source
1. Clone this repository
2. Go to `chrome://extensions` in Chrome
3. Enable **Developer mode** (top-right toggle)
4. Click **Load unpacked**
5. Select the `extension/` folder from this repo

Open a new tab — you'll see Swoosh.

---

## Features

- **Tab grouping** — Open tabs grouped by domain on a clean grid
- **Universal search** — Press `/` or `Cmd+K` to search tabs and Google
- **Landing pages** — Gmail, YouTube, X, LinkedIn grouped together
- **Duplicate cleanup** — One-click to close duplicate tabs
- **Stale tabs** — Tabs you haven't touched in a while, configurable from 1 hour to 2 weeks
- **Save for later** — Bookmark tabs to a checklist, reopen when ready
- **Archive** — Search through saved tabs
- **Focus time** — See how many tabs you have open and track your focus
- **Themes** — Light/dark mode with warm and cool color palettes

---

## Tech stack

| What | How |
|------|-----|
| Extension | Chrome Manifest V3 |
| Storage | chrome.storage.local |
| Sound | Web Audio API (synthesized, no files) |
| Animations | CSS transitions + JS confetti particles |

---

## License

MIT
