# Lock Harbor — public pages

Support guide, FAQ, privacy policy, terms and marketing page for the Lock Harbor
password manager. Static HTML, no build step, no dependencies — matching
`prospere-pages`, `fishermens-buddy-pages` and `repvault-pages`.

## Status: not live yet

This repository is **private** and **GitHub Pages is deliberately not enabled**.
Everything is ready; publishing is a separate, deliberate step.

| File | Purpose |
|---|---|
| `index.html` | Support & User's Guide — the page the store listing's support link should point at |
| `marketing.html` | Landing page |
| `faq.html` | Frequently asked questions |
| `privacy-policy.html` | **Required by both app stores**, and must be a live URL before submission |
| `terms-of-service.html` | Terms of service |
| `images/app-icon.png` | Favicon (256px, 77 KB) |

## Going live

The site serves from **`lockharbor.dubayaapps.com`**, not from the `github.io`
address — matching `liftsense.dubayaapps.com`, which is how the other live app
does it. Confirmed with the user 2026-09-10, no hyphen.

Pages for a private repository needs a paid GitHub plan, so publishing means
making the repository public first. In order:

```bash
gh repo edit joeldubey/lock-harbor-pages --visibility public --accept-visibility-change-consequences
gh api -X POST repos/joeldubey/lock-harbor-pages/pages \
  -f 'source[branch]=master' -f 'source[path]=/'
gh api -X PUT repos/joeldubey/lock-harbor-pages/pages -f cname=lockharbor.dubayaapps.com
```

**And one step that is not GitHub's:** a DNS `CNAME` record at the registrar for
`dubayaapps.com`, pointing `lockharbor` at `joeldubey.github.io`. Neither
`lockharbor.dubayaapps.com` nor the hyphenated form resolved when this was
written, so that record does not exist yet — **the `CNAME` file in this repo is
only half of it**, and GitHub will not serve the domain until DNS does. Worth
stating because a missing DNS record and a missing `CNAME` file fail identically
from the outside.

Once DNS resolves, turn on **Enforce HTTPS** in the repository's Pages settings.
It is greyed out until the certificate is issued, which takes a few minutes.

Check in this order, because each failure looks like the one before it:

```bash
nslookup lockharbor.dubayaapps.com                                        # answers via joeldubey.github.io
curl -sI https://lockharbor.dubayaapps.com/privacy-policy.html | head -1   # 200
```

**After going live, two things are owed:**

1. Put the privacy-policy URL in the store listing — `store/play-listing.md` in
   the app repo already carries every URL in its final form.
2. Link the privacy policy and support guide from inside the app.

## Editing

Open the files directly — there is no toolchain. Two conventions worth keeping:

- **Write with explicit UTF-8.** Reading these files with PowerShell's
  `Get-Content` and writing them back mangles every em dash into `â€”`. It
  happened once already.
- **No overclaiming.** These pages state plainly that Lock Harbor has had no
  external security audit, does not sync, is Android-only for now, and cannot
  recover anyone's vault. Keep it that way — the app's own guide is held to the
  same standard.
