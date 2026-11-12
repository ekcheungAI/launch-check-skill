# The 20 checks

Use `curl -sIL` for headers and `curl -sL` for bodies. `H` = the homepage HTML you already fetched.

| # | Check | How |
|---|---|---|
| 1 | HTTPS works; http:// redirects to https:// | `curl -sI http://HOST` should be 301/302/307/308 to https |
| 2 | Custom 404 | request `/zz-made-up-url-12345`; status must be 404 and the body should be a real page, not a bare server error |
| 3 | sitemap.xml exists and parses | fetch `/sitemap.xml`; 200, XML, count `<loc>` |
| 4 | robots.txt exists and does not block the whole site | fetch `/robots.txt`; FAIL if `User-agent: *` has `Disallow: /` |
| 5 | Title and meta description | in H |
| 6 | Open Graph tags | `og:title`, `og:image` in H; image URL returns 200 |
| 7 | Favicon | `<link rel="icon">` in H, or `/favicon.ico` returns 200 |
| 8 | Mobile viewport | `<meta name="viewport"` in H |
| 9 | Privacy policy page exists and is linked from the footer | find the link in H, fetch it, expect 200 |
| 10 | The privacy page says what personal data is collected and why (where a form or signup exists) | read the page; see `hk-privacy-notes.md` |
| 11 | Tracking or cookie notice if analytics or ad scripts load | look for googletagmanager, gtag, fbq, hotjar, clarity in H and its scripts; if found, check for a consent notice or a disclosure on the privacy page |
| 12 | Terms or refund terms linked if anything is sold | look for prices, checkout, cart; if none seen, CAN'T TELL |
| 13 | No API keys, tokens or passwords in H or its JS | fetch H and the linked `.js` files; grep for `api[_-]?key`, `secret`, `token`, `service_role`, `eyJ` (JWT), `sk_live`, `password` ; report only real credential-shaped values |
| 14 | Security headers | `strict-transport-security`, `x-content-type-options`, and `content-security-policy` or `x-frame-options` |
| 15 | Image alt text | every `<img>` has an `alt`; list those missing; empty alt on decorative images is fine, say so |
| 16 | Image weight | HEAD each `<img src>` in H; FAIL anything over 500 KB (`content-length`) |
| 17 | Links on the homepage return 200 | HEAD each `<a href>` (internal first); report non-200; 403/405 from big publishers is usually bot-blocking, say so |
| 18 | Contact method visible | email, form, or messaging link on the site |
| 19 | Third-party fonts and scripts listed; nothing over http:// | list external hosts in H; flag any `http://` resource (ignore XML namespaces) |
| 20 | Canonical tag and no accidental noindex | `rel="canonical"` in H; `robots` meta must not say noindex on the homepage |

If a check cannot be done read-only, or the page blocks you, the result is CAN'T TELL.
