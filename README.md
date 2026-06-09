# coolartifacts.github.io

Static site for the **Cool Artifacts Society**, hosted on GitHub Pages at
[https://coolartifacts.io](https://coolartifacts.io).

## Contents

| File | Purpose |
|------|---------|
| `index.html` | Company landing page |
| `privacy.html` | MoveMouse privacy policy (linked from the Play Store listing) |
| `app-ads.txt` | AdMob seller authorization — must be served at the domain root |
| `CNAME` | Custom domain for GitHub Pages (`coolartifacts.io`) |

## One-time setup

### 1. Create the GitHub org + repo
- Create a free GitHub **organization** named `coolartifacts`.
- Inside it, create a repo named **`coolartifacts.github.io`** (the user/org-pages
  repo name — this is what makes the site serve at the domain root, which
  `app-ads.txt` requires).
- Push this folder to that repo.

### 2. Point the OVH domain at GitHub Pages
In the OVH DNS zone for `coolartifacts.io`:

**Apex (`@`) — four A records:**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**`www` — one CNAME record:**
```
www  CNAME  coolartifacts.github.io.
```

(Optionally also add the four AAAA records for IPv6:
`2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.)

### 3. Enable Pages + HTTPS
In the repo on GitHub: **Settings -> Pages**
- Source: `main` branch, `/ (root)`.
- Custom domain: `coolartifacts.io` (the `CNAME` file sets this automatically).
- Tick **Enforce HTTPS** once the certificate is issued (can take an hour).

### 4. Point the Play Store listing at this domain
In Google Play Console, set the app's **developer website / store listing URL**
to `https://coolartifacts.io`. AdMob's crawler reads this URL, strips it to the
root domain, and looks for `https://coolartifacts.io/app-ads.txt`. The domain in
the listing **must** match where `app-ads.txt` is served, or AdMob reports it as
missing.

## Verify

- Site: <https://coolartifacts.io>
- AdMob file: <https://coolartifacts.io/app-ads.txt> (must show the `google.com, pub-...` line)
- Privacy: <https://coolartifacts.io/privacy.html>

AdMob can take **24-48 hours** to re-crawl `app-ads.txt` after it goes live; the
"app-ads.txt not found" warning in the AdMob console clears on its own once found.
