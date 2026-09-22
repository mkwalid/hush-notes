# Hush

**Private notes that are encrypted before they ever touch your disk.**

Hush is a single-file notes app with folders, Markdown, attachments, and a built-in space to think out loud about each note. No account, no server, no tracking, no build step. Open the page, set a passphrase, write.

**Try it:** https://mkwalid.github.io/hush-notes/

## Why use it

- **Your notes are yours.** Everything is encrypted in your browser with a key made from your passphrase. Nothing is uploaded, because there is nowhere to upload it to.
- **Nothing to sign up for.** No email, no login, no subscription. Free forever, because it's just a web page.
- **Organized like real docs.** Nested folders, search across every note, and Markdown for headings, lists, code, links, and tick-able tasks.
- **Room for more than text.** Attach images, videos, audio, or any other file to a note, encrypted the same way as everything else.
- **Built for ideas, not just storage.** Every note has a **Thoughts** panel: a running thread where you question the idea, list your doubts, and write down what to try next, without cluttering the note itself.
- **Feels good on any screen.** Responsive layout for phone and desktop, light and dark themes, keyboard friendly.
- **One file.** The whole app is `index.html`. Read it, fork it, host it anywhere, or run it offline from your desktop.

## How it works

1. On first visit you choose a passphrase (8 characters or more).
2. Your notes are stored as a single encrypted blob in your browser's local storage. Attachments are encrypted the same way and stored separately in the browser's file database.
3. When you unlock, everything is decrypted in memory only. When you lock (or after 10 minutes of inactivity), the key is dropped.
4. **Backup and vault** gives you an encrypted text backup of your notes, or a full backup file that also includes attachments, either of which restores on any device.

## Features

- Nested folders and subfolders
- Markdown: headings, bold, italic, lists, tasks, code blocks, quotes, links
- Attach images, videos, and files to any note, encrypted with the rest of your vault
- Write and Read modes
- Full-text search across all notes
- Thoughts thread on every note
- Encrypted backup and restore, with a full backup option for attachments
- Auto-lock after 10 minutes idle, plus a manual lock button
- Light and dark themes

## Security, honestly

**What it does**

- Encrypts with AES-256-GCM using the browser's built-in Web Crypto API.
- Derives the key from your passphrase with PBKDF2 (SHA-256, 250,000 iterations) and a random salt.
- Uses a fresh random IV every time it saves.
- Keeps decrypted notes, attachments, and the key in memory only while unlocked.
- Sends your notes nowhere. The only outside request is to Google Fonts, for typography.

**What you should know**

- **This code has not been independently audited.** It uses standard, well-tested primitives, but the app itself is young. Don't make it the only copy of anything critical.
- **There is no passphrase recovery.** Lose it and the notes are gone, for you and for everyone else. That is the point, and also the risk.
- **A weak passphrase is the weakest link.** Use several random words.
- **Local only.** Your vault lives in one browser on one device. Clearing site data deletes it unless you have a backup. There is no sync.
- **It can't protect a compromised device.** Malware, a hostile browser extension, or someone watching you type can still read your notes while the vault is unlocked.
- **Notes are stored in the browser, not in this repo.** Publishing the code exposes nothing about anyone's notes.

## Moving your notes between devices

1. On the old device: **Backup and vault**, then either **Copy text backup** (notes and folders only) or **Download full backup file** (also includes attachments).
2. On the new device: on the lock screen choose **Restore from backup**, paste the text or choose the file, then unlock with the same passphrase.

## Run it yourself

**Offline:** download `index.html` and double-click it. Keep it in the same place afterward, since some browsers tie stored data to the file's location.

**Host it:** put `index.html` in any static host (GitHub Pages, Netlify, Cloudflare Pages). No build needed.

**Local server:**

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Encryption needs a secure context, so use `https://`, `http://localhost`, or a local file in a current browser.

## Roadmap ideas

- Change passphrase
- Drag and drop to move notes between folders
- Tags
- Optional end-to-end encrypted sync
- Export notes as Markdown files

Pull requests and ideas are welcome.

## License

MIT. See [LICENSE](LICENSE).
