# Spotify Playlist Builder

A single-file web app that turns a list of song names into a Spotify playlist. Paste a list, upload a CSV, or import from an existing playlist — review the matches Spotify finds, swap in alternatives where needed, then create a new playlist or append to an existing one.

**Live demo:** https://studio6networks.github.io/playlist-builder/

No backend, no database, no analytics. The whole app is one `index.html` file. Auth tokens live in your browser's localStorage and never leave it.

## Features

- **PKCE OAuth** — secure browser-only auth with persistent sign-in via refresh token. Stay logged in across sessions until you disconnect.
- **Flexible input** — paste lines as `Artist - Title`, `Title - Artist`, or plain `Title`. Upload a CSV with auto-detected `title` / `artist` columns. Or import every track from an existing Spotify playlist URL.
- **Top-5 match picker** — for each line, the app shows Spotify's best guess plus 4 alternatives in a dropdown. Swap in a different match in one click.
- **30-second previews** — every matched track has a play button using Spotify's preview clip.
- **Duplicate detection** — same track appearing twice gets flagged with a yellow highlight.
- **Retry misses** — re-search unmatched lines with simpler queries to recover more tracks.
- **Drag-to-reorder** — set the final play order before creating.
- **CSV export** — download a timestamped CSV of all matches with artist, title, album, Spotify URL.
- **Create new or append** — make a fresh playlist, or pick one of your existing playlists and add tracks to it.
- **Draft persistence** — song list, playlist name, and client ID all auto-save to localStorage. Refresh-safe.

## Using the live app

1. Open https://studio6networks.github.io/playlist-builder/
2. Click **Connect Spotify** and authorize.
3. Paste songs, upload a CSV, or import from a playlist URL.
4. Click **Search tracks**. Review matches, swap alternatives or remove rows as needed.
5. Pick **Create new** (name it) or **Add to existing** (pick from your playlists).
6. Hit **Create playlist** / **Add to playlist**. You'll get a direct "Open in Spotify" link.

Note: while the connected Spotify app is in Development Mode, only Spotify accounts the app owner has whitelisted under **User Management** can sign in.

## Host your own

The app is one HTML file — any static host works (GitHub Pages, Netlify, Vercel, S3, your own server).

### 1. Create a Spotify app

1. Go to https://developer.spotify.com/dashboard and log in.
2. Click **Create app**. Pick any name and description.
3. Set **Redirect URI** to the exact URL where your `index.html` will be served. The trailing slash matters. Examples:
   - GitHub Pages: `https://yourname.github.io/your-repo/`
   - Local: `http://localhost:8000/`
4. Check **Web API**, accept terms, save.
5. Copy the **Client ID** from the app settings.

### 2. Deploy the file

Clone or download this repo, then either:

**GitHub Pages**
- Push to a public repo, then in **Settings → Pages** set source to `main` / root.
- Your site goes live at `https://<username>.github.io/<repo>/`.

**Local**
```bash
python -m http.server 8000
# open http://localhost:8000/
```

### 3. Prefill your Client ID (optional)

Edit `index.html` and replace the `value="..."` in the Client ID input with your own. Otherwise users can paste theirs.

### 4. Authorize Spotify accounts

While in Development Mode, add Spotify emails under **User Management** in your Spotify app settings. To go fully public, request **Extended Quota** from the same dashboard — Spotify reviews and approves apps for public use at no cost.

## Tech

- Vanilla HTML / CSS / JavaScript. No build step, no dependencies.
- Spotify Web API + PKCE auth flow.
- ~700 lines, single file.

## License

MIT
