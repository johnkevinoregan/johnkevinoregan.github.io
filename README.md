# johnkevinoregan.github.io

Personal website of J. Kevin O'Regan, hosted on GitHub Pages.

- **Live site:** https://kevin-oregan.net/ (custom domain; `https://johnkevinoregan.github.io/` redirects here)
- **Repository:** https://github.com/johnkevinoregan/johnkevinoregan.github.io
- **Local working copy:** wherever you cloned or copied this repo (originally
  `/home/kevin/webserver4github` on *incca*; now edited from wherever you keep it)

This is a static snapshot of the original site at
`http://nivea.psycho.univ-paris5.fr/`, mirrored and re-hosted on GitHub Pages.

---

## What was done

1. **Mirrored** the original site with:

   ```bash
   wget --mirror --page-requisites --convert-links --adjust-extension \
        --no-parent --no-host-directories \
        -e robots=off --reject-regex '(ga\.js|google-analytics)' \
        http://nivea.psycho.univ-paris5.fr/
   ```

   Result: 45 HTML pages plus images (~17 MB). All internal links were
   rewritten to relative form. Google Analytics (`ga.js`) was dropped.

2. **Fixed** the two absolute links that would have broken once off the old
   server (a citation image and a cross-link) to point at their local targets.
   The only remaining absolute reference is harmless MS-Word editing metadata
   that browsers ignore.

3. **Added `.nojekyll`** so GitHub serves the raw HTML files verbatim
   (important for a hand-authored site — without it, Jekyll can mangle files).

4. **Created the public repo** `johnkevinoregan/johnkevinoregan.github.io`,
   committed and pushed, and enabled GitHub Pages (branch `main`, root, HTTPS).

Verified live: homepage, a deep page with spaces/apostrophes in its path, and
the repointed image all return `HTTP 200`.

---

## How to edit the site

From inside the repo folder (wherever it lives on your machine), edit the
files, then publish:

```bash
git add -A
git commit -m "Describe your change"
git push
```

GitHub Pages rebuilds automatically in about a minute. Reload the live URL
(hard-refresh, Ctrl/Cmd-Shift-R, to bypass the browser cache).

### Working on a new machine (e.g. a laptop)

The commands above are the same on any computer, but two things live *outside*
this folder and must be set up once per machine:

1. **Git must be installed** (and ideally the GitHub CLI, `gh`).
2. **You must be logged in to GitHub** so `git push` is authorized — the login
   is not stored in this folder. Easiest: run `gh auth login` once
   (GitHub.com → HTTPS → log in via browser).

To move the project to another machine, the cleanest way is to **clone** it
rather than copy files:

```bash
git clone https://github.com/johnkevinoregan/johnkevinoregan.github.io.git
```

If you copy the folder manually instead, you **must** include the hidden `.git`
subfolder — that is the repository and the link to GitHub. Copying only the
visible files gives you loose HTML that cannot push anywhere.

### To re-snapshot the original site instead

If the original `nivea` site changes and you want to pull those changes in,
re-run the `wget` command above from a scratch folder, copy the files over the
working copy, then commit and push as above.

---

## Good to know

- **This is a snapshot, not a live proxy.** Changes on the original `nivea`
  server do **not** appear here until you re-mirror.
- **The old site still exists** independently at
  `http://nivea.psycho.univ-paris5.fr/`. To truly retire it you would redirect
  or shut down the Apache server on `nivea` (a separate university machine).
- **`.claude/`** is intentionally excluded from the repo (see `.gitignore`).
- **Custom domain:** the site is served at `https://kevin-oregan.net` via a
  `CNAME` file in this repo plus DNS records at OVH. HTTPS is a free,
  auto-renewing Let's Encrypt certificate managed by GitHub — nothing to renew
  manually. See `README_switched_Nivea_Website_to_Github.md` for the full
  migration details.
