# Digital business card

Static vCard hosted on GitHub Pages at **https://rasheedamh.github.io/vcard/**.

| File | Purpose |
| --- | --- |
| `contact.vcf` | The vCard (fill in the phone number). CRLF line endings, vCard 3.0. |
| `index.html` | Landing page. Auto-navigates to `contact.vcf` and shows an "Add to Contacts" button as fallback. |
| `.nojekyll` | Disables Jekyll processing. |
| `qr-card.png` | 2460 x 2460 px, 600 dpi, error-correction level H. Encodes `https://rasheedamh.github.io/vcard/`. |

## Setup

1. Push these files to the `main` branch of the `vcard` repo.
2. Repo **Settings → Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The site is live at https://rasheedamh.github.io/vcard/ about a minute later.

## How the iOS "Add Contact" sheet is triggered

Whether iOS Safari shows the contact sheet or just downloads the file depends on the
`Content-Type` GitHub Pages sends for `contact.vcf`. Check it with:

```
curl -sI https://rasheedamh.github.io/vcard/contact.vcf | grep -i content-type
```

* `text/vcard` (expected from GitHub Pages): both the auto-redirect in `index.html` and the
  button open the native contact preview with "Create New Contact" / "Add to Existing Contact".
* Anything else: Safari shows a download prompt; the contact sheet appears once the user taps
  the downloaded file. GitHub Pages does not allow custom headers, so this cannot be changed
  from the repo.

Open `https://rasheedamh.github.io/vcard/?stay` to view the landing page without the auto-redirect.
