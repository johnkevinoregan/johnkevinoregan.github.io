# Switched the Nivea website over to GitHub Pages

_A record of what was done, 18 July 2026._

## Goal
Replace the old site running on `nivea.psycho.univ-paris5.fr` (a university
machine we want to switch off) with a free, permanent copy hosted on GitHub
Pages, reachable at the proper address **https://kevin-oregan.net**.

## What was done

### 1. Mirrored the old site
Captured the whole `nivea.psycho.univ-paris5.fr` site as static files with:

```bash
wget --mirror --page-requisites --convert-links --adjust-extension \
     --no-parent --no-host-directories \
     -e robots=off --reject-regex '(ga\.js|google-analytics)' \
     http://nivea.psycho.univ-paris5.fr/
```

Result: 45 HTML pages + images (~17 MB), internal links made relative, Google
Analytics dropped, two absolute links repointed to local targets, and a
`.nojekyll` file added so GitHub serves the raw HTML verbatim.

### 2. Published it on GitHub Pages
- Repo: **https://github.com/johnkevinoregan/johnkevinoregan.github.io**
  (public; free hosting; HTTPS).
- Committed and pushed the mirror. Site served at
  `https://johnkevinoregan.github.io/`.
- Added a `CNAME` file so GitHub Pages answers for the custom domain
  `kevin-oregan.net`.

### 3. Pointed kevin-oregan.net at GitHub (DNS at OVH)
The domain `kevin-oregan.net` is registered/DNS-hosted at **OVH**, so no
university involvement was needed. In the OVH DNS zone we:

- **Removed** the old redirection that sent the domain to nivea's IP
  (`http://193.51.84.161`).
- **Apex `kevin-oregan.net`** → four GitHub `A` records:
  `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  and four `AAAA` (IPv6) records: `2606:50c0:8000::153` … `:8003::153`.
- **`www`** → `CNAME` to `johnkevinoregan.github.io.`
- **`whyred.kevin-oregan.net`** → changed to a visible 301 redirect to
  `https://kevin-oregan.net/FeelingSupplements/index.html` (the old "Why Red"
  shortcut, now pointing at the new site instead of nivea).
- **Left untouched**: all email records (MX, SPF, DKIM `_domainkey`) and the
  XMPP/Jabber/SIP/VPN/FTP service records — email etc. keep working.

### 4. HTTPS
GitHub Pages issues a free Let's Encrypt certificate for `kevin-oregan.net`
automatically once the DNS is correct. Then "Enforce HTTPS" is turned on so
`https://kevin-oregan.net` is the secure default.

## Result
- **https://kevin-oregan.net** now serves the site directly from GitHub.
- `johnkevinoregan.github.io` redirects to `kevin-oregan.net`.
- `whyred.kevin-oregan.net` → the Feeling Supplements page.
- **Nivea is no longer needed** and can be switched off. Email and other
  services on `kevin-oregan.net` are unaffected.

## How things work now (mental model)
- **OVH** is only the *phonebook* (DNS) + domain registrar + email. No OVH web
  server hosts the site.
- **GitHub** does all the actual web serving, for free.
- The only ongoing cost is the annual domain-registration fee for
  `kevin-oregan.net` (unavoidable for any domain).

## How to edit the site in future
The local working copy is the machine *incca* (currently in
`/home/kevin/webserver4github`). Edit files there, then:

```bash
git add -A
git commit -m "Describe the change"
git push
```

GitHub rebuilds in ~1 minute. To re-snapshot the original nivea site instead,
re-run the `wget` command above and re-push.
