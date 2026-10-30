# Dr. Shantanu Samanta — Financial Scanners Site

Static showcase page plus a small visitor counter (Netlify Function + Netlify Blobs).

## Folder layout (keep it exactly like this)
```
scanners-site/
├── index.html                    ← the website (photo embedded)
├── netlify.toml                  ← tells Netlify where things are
├── package.json                  ← installs @netlify/blobs for the counter
└── netlify/
    └── functions/
        └── counter.mjs           ← the visitor counter (/api/counter)
```

## Deploy (GitHub → Netlify)
1. GitHub → New repository → name e.g. `scanners-site` → Public or Private → Create.
2. "uploading an existing file" → drag ALL the contents of this folder (including the `netlify` folder) → Commit.
   Check that `netlify/functions/counter.mjs` appears in the repo.
3. Netlify → Add new site → Import an existing project → GitHub → choose `scanners-site`.
4. Build settings: Build command = leave empty, Publish directory = `.` (netlify.toml already sets these) → Deploy.
5. When live, open `https://<your-site>.netlify.app/api/counter` — you should see e.g. `{"total":0,"unique":0}`.
6. Open the home page — the two counter pills appear at the bottom.

## Updating later
Edit/upload files in GitHub → Netlify redeploys automatically. The counts are stored in Netlify Blobs and survive redeploys.

## Notes
- Drag-and-drop on Netlify Drop does NOT run functions — use the GitHub route.
- Opening index.html directly from your computer hides the counter (no function there); that is expected.
- "Unique" = once per browser. Different devices, private windows or cleared browser data count again.
- Common bots/link-preview crawlers (WhatsApp, Telegram, Google etc.) are ignored.
- To reset counts: Netlify → your site → Blobs → store `visitor-counter` → delete key `counts`.
- To start from a number, e.g. 100: change `{ total: 0, unique: 0 }` in counter.mjs before the first visit.
