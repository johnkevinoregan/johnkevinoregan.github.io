# johnkevinoregan.github.io

Personal website of J. Kevin O'Regan, hosted on GitHub Pages.

- **Live site:** https://johnkevinoregan.github.io/
- **Repository:** https://github.com/johnkevinoregan/johnkevinoregan.github.io
- **Local working copy:** `/home/kevin/webserver4github` (on the machine *incca*)

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

Edit files in `/home/kevin/webserver4github`, then publish:

```bash
cd /home/kevin/webserver4github
git add -A
git commit -m "Describe your change"
git push
```

GitHub Pages rebuilds automatically in about a minute. Reload the live URL
(hard-refresh, Ctrl/Cmd-Shift-R, to bypass the browser cache).

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
- **Nicer domain later:** you can buy a custom domain and point it at this
  GitHub Pages site (free HTTPS). The address is currently tied to the GitHub
  username `johnkevinoregan`; a custom domain is the way to get a chosen name.
