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

Pages for a private repository needs a paid GitHub plan, so publishing means
making the repository public first. Both steps, in order:

```bash
gh repo edit joeldubey/lock-harbor-pages --visibility public --accept-visibility-change-consequences
gh api -X POST repos/joeldubey/lock-harbor-pages/pages \
  -f 'source[branch]=master' -f 'source[path]=/'
```

It then serves at `https://joeldubey.github.io/lock-harbor-pages/`, matching the
sibling repos (which are public, with Pages built from `master` at the root).

**After going live, two things are owed:**

1. Put the privacy-policy URL in the store listing.
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
