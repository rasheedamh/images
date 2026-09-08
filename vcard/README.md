# Digital business card

Static vCard hosted on GitHub Pages at **https://card.amhalrasheed.net/**.

| File | Purpose |
| --- | --- |
| `contact.vcf` | The vCard (fill in the phone number). CRLF line endings, vCard 3.0. |
| `index.html` | Landing page. Auto-navigates to `contact.vcf` and shows an "Add to Contacts" button as fallback. |
| `CNAME` | Custom domain for GitHub Pages. |
| `.nojekyll` | Disables Jekyll processing. |
| `qr-card.png` | 2460 x 2460 px, 600 dpi, error-correction level H. Encodes `https://card.amhalrasheed.net/`. |

## One-time setup

1. Push these files to the `main` branch of the `vcard` repo.
2. Repo **Settings → Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
3. At the DNS provider for `amhalrasheed.net`, add:

   | Type | Host / Name | Value | TTL |
   | --- | --- | --- | --- |
   | CNAME | `card` | `rasheedamh.github.io` | 3600 (or Auto) |

   The `CNAME` file in the repo pre-fills the custom domain, so **Settings → Pages → Custom domain** should already show `card.amhalrasheed.net`. If it does not, type it in and Save.
4. Wait for the DNS check to pass, then tick **Enforce HTTPS** (the checkbox becomes available a few minutes after the certificate is issued).

## How the iOS "Add Contact" sheet is triggered

Whether iOS Safari shows the contact sheet or just downloads the file depends on the
`Content-Type` GitHub Pages sends for `contact.vcf`. Check it with:

```
curl -sI https://card.amhalrasheed.net/contact.vcf | grep -i content-type
```

* `text/vcard` (expected from GitHub Pages): both the auto-redirect in `index.html` and the
  button open the native contact preview with "Create New Contact" / "Add to Existing Contact".
* Anything else (e.g. `application/octet-stream`): Safari shows a download prompt; the contact
  sheet appears once the user taps the downloaded file. Nothing in the repo can change this,
  since GitHub Pages does not allow custom headers.

Open `https://card.amhalrasheed.net/?stay` to view the landing page without the auto-redirect.
