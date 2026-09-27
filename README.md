# Mon Cahier

A single-page app for learning French at A1–A2, working through English: spaced-repetition
flashcards, grammar lessons with exercises, dictation practice, a progress dashboard, and
import of your own word lists from Google Sheets.

Everything runs in the browser. There is no server, no account and no database — your
progress lives in the browser's `localStorage`, and the Settings panel can export it as a
JSON backup or restore one.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app: markup, CSS and JavaScript in one file. Nothing is fetched from a CDN. |
| `manifest.webmanifest` | Lets the site be installed as an app on a phone or desktop. |
| `sw.js` | Service worker. Caches the app so it keeps working offline. |
| `icon.svg`, `icon-192.png`, `icon-512.png` | App icons. |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is. |

## Putting it on GitHub Pages

1. Create a new repository on GitHub — for example `mon-cahier`. Public is fine; the app
   holds no secrets.
2. On the repository page choose **Add file → Upload files**, drag in everything from this
   folder (including the hidden `.nojekyll`), and commit.
3. Go to **Settings → Pages**. Under *Build and deployment* set **Source** to
   *Deploy from a branch*, **Branch** to `main` and the folder to `/ (root)`. Save.
4. Wait a minute or two. The site appears at
   `https://<your-username>.github.io/mon-cahier/`.

With git on the command line instead:

```bash
cd path/to/this/folder
git init
git add -A
git commit -m "Mon Cahier"
git branch -M main
git remote add origin https://github.com/<your-username>/mon-cahier.git
git push -u origin main
```

Then do step 3 above.

### Updating later

Replace `index.html` and commit again. The service worker fetches from the network first,
so the next online visit picks up the new version. If a phone still shows an old copy,
close the tab and reopen it, or bump the `CACHE` name at the top of `sw.js`.

### A custom domain

In **Settings → Pages → Custom domain**, enter the domain and add the DNS records GitHub
shows you (a `CNAME` for a subdomain such as `french.example.com`, or four `A` records for
a bare domain). Leave **Enforce HTTPS** ticked.

## The AI helpers

Inside claude.ai the app can ask Claude to build exercises from a word list, turn your own
grammar notes into a lesson, and write example sentences for words that lack one. On a
plain website that runtime does not exist, so those buttons stay hidden until you paste an
Anthropic API key into **Settings → AI helpers**.

The key is stored only in that browser under `moncahier.key`. It is never included in the
JSON backup and never sent anywhere except `api.anthropic.com`. Usage is billed to your own
key, so keep in mind that anyone using that browser profile can spend it — this is meant
for your own machine, not a shared computer. You can clear it by emptying the field.

Never commit an API key to the repository.

## Browser support

Chrome, Edge, Safari and Firefox, on desktop and mobile. Dictation uses the browser's
built-in French speech synthesis; if a browser has no French voice the app says so and the
rest keeps working.
