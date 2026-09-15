# Atlas

_draw · name · collect · combine_

Atlas is a small drawing game that runs entirely in the browser. Everything
lives inside **vaults** — separate, self-contained collections (like Obsidian
vaults). Each vault has its own cards and its own concepts, with nothing
shared between them. When you open Atlas you always land on the vault picker
first and choose which one to enter.

Inside a vault: you sketch on an unlimited canvas, name what you drew, and it
becomes a **card** in a searchable collection. Cards can carry **tags**, and
the search box understands `#tag` syntax — type `#nature` to filter to cards
tagged nature, or mix it with plain text (`#nature sketch`) to filter by tag
and name at once. Switch to the **Concepts** tab to pull existing cards onto
a second canvas, draw between and around them, and save the result as its
own named concept.

Every save keeps the previous version instead of overwriting it, so you can
look back at how a card or concept evolved and jump between versions at any
time. Cards and concepts can also be renamed on the fly from their list, and
the latest version always loads first.

It's a single self-contained HTML file — no build step, no server, no
external dependencies.

## Running it locally

Just open `index.html` in a browser. That's it.

## Hosting on GitHub Pages

1. Create a new **public** GitHub repository.
2. Add all the files in this folder to it (`index.html`, `manifest.json`, the
   `.png` icons, this `README.md`).
3. In the repo, go to **Settings → Pages**, set **Source** to "Deploy from a
   branch," pick `main` and the `/(root)` folder, then save.
4. After a minute or two your site is live at
   `https://your-username.github.io/your-repo-name/`.

Any future edits just need a commit to `index.html` — GitHub Pages redeploys
automatically.

## Installing it as an app (iPad / iPhone / Android / desktop)

Once it's hosted somewhere with HTTPS (GitHub Pages qualifies), open it in
Safari or Chrome and use **Share → Add to Home Screen** (iOS/iPadOS) or the
browser's **Install app** option (Chrome/Edge). It'll launch full-screen with
its own icon, no browser chrome.

## Apple Pencil on iPad

Atlas does its own palm rejection: while the Pencil is actively drawing, any
finger touch (like a resting palm) is ignored outright instead of being
treated as a second input. It also properly handles the case where iPadOS
itself cancels a touch mid-gesture — earlier versions could get stuck and
require a page refresh to draw again; that's fixed now.

## How saving works — please read this part

Atlas has no backend and no login. Vaults, cards, and concepts are saved to
the browser's local storage on whatever device you're using:

- Data stays **on that one device, in that one browser**. It does not sync
  between your iPad and your laptop, or between Safari and Chrome on the same
  device.
- Nobody else who opens your hosted link sees your drawings — everyone gets
  their own empty set of vaults, stored locally on their own device.
- Clearing site data/history for the page, or browsing in a private/incognito
  window, will erase it.
- Deleting a vault deletes every card and concept inside it. There's no
  undo for that one — it asks for confirmation first.

This is fine for a personal beta. If you eventually want your collection to
follow you across devices, or to share it with other people, that requires an
actual backend (something like Supabase or Firebase is the lowest-effort way
to add that later) — GitHub Pages alone can only serve static files, it can't
store data for you.

## Files in this folder

| File | Purpose |
|---|---|
| `index.html` | The entire app — canvas engine, UI, storage logic |
| `manifest.json` | Lets browsers install Atlas as a standalone app |
| `apple-touch-icon.png` | Home Screen icon for iOS/iPadOS |
| `icon-192.png`, `icon-512.png` | App icons for Android/desktop install |
| `favicon-32.png` | Browser tab icon |
