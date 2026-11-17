# Riva Computech — website

**rivacomputech.com** — the site for Devik Patel's remote IT consulting business (Microsoft 365, Azure, Windows Server and virtualization support for small businesses across the United States).

The site is a single page that *is* a Windows 11 desktop. The taskbar is the navigation, the hero is a working PowerShell terminal, and each section is introduced by the cmdlet that would fetch it (`Get-Service`, `Compare-Object`, `Test-ITHealth`, `Get-ADUser devik`…).

No framework, no build step — `index.html` **is** the site (HTML, CSS and JS in one file).

## Files

```
index.html            the whole site
404.html              custom "page not found" page (terminal style)
card.html             digital business card (opened from the QR code on the card, /card)
devik-patel.vcf       contact file used by the card's "Save contact" button
devik.jpg             profile photo
logo.svg              main logo (used on the site, card and 404 page)
brand/                logo source files (see Brand below)
favicon.svg           browser tab icon
favicon.ico           favicon for older browsers and Google
favicon-48x48.png     favicon for Google search results
favicon-192x192.png   favicon for Google search results and Android
apple-touch-icon.png  iPhone/iPad home-screen icon
og.png                1200×630 social preview image (links shared on LinkedIn, Facebook, etc.)
assets/logos/         technology logos for the "Hands-on with" strip
email/riva-logo.png   logo loaded by the email signatures (do not delete)
robots.txt            search engine rules
sitemap.xml           sitemap for Google Search Console
wrangler.jsonc        Cloudflare settings (enables the custom 404 page)
.assetsignore         files Cloudflare should not publish
```

## What is on the page

| Section | What it does |
| --- | --- |
| **Hero / desktop** | Wallpaper drawn in SVG (recolours for dark mode) and an interactive Windows Terminal. Try `help`, `Get-Service`, `Get-ADUser devik`, `ls`, `cd about`, `exit`. Tab-completion and ↑/↓ history work. |
| **Services** (`Get-Service`) | Service cards, each with its PowerShell-verb cmdlet and a plain-English line. |
| **Why** (`Compare-Object`) | A typical IT provider versus Riva Computech. |
| **Automation** (`Invoke-Automation`) | A real `Offboard-User.ps1` script with syntax highlighting and a **Run** button that plays the output. |
| **Health check** (`Test-ITHealth`) | Settings-style toggles that give a live score. The button pre-fills the contact form with the result. Nothing leaves the browser. |
| **About** (`Get-ADUser devik`) | Devik's profile and bio. |
| **Contact** (`Send-MailMessage`) | A request form for a free 30-minute call, with a preferred-time field and the availability hours. Posts to Formspree and uses reCAPTCHA. |

The shell around it: a fixed taskbar with scroll-spy, a Start menu with search, a power menu (Sleep shows a lock screen), Quick Settings (dark mode, reduced motion, copy email) and a calendar flyout. Light and dark follow the visitor's system until they choose one.

Easter eggs: the Konami code opens Windows 3.1 (Internet Archive emulator), and typing `devik` anywhere plays a song.

The Start button uses the Riva logo rather than the Windows logo, the wallpaper is original, and the footer carries a trademark disclaimer, so the site does not look affiliated with Microsoft.

## Brand

Logo source files live in `brand/`. They are not used by the site itself; they are kept for print, social profiles and future designs. Main colour: `#0067c0`.

| File | Use |
| --- | --- |
| `brand/riva-computech-logo.svg` | Full logo with "COMPUTECH", on light backgrounds (same as the root `logo.svg`) |
| `brand/riva-computech-logo-white.svg` | Full logo in white, for dark backgrounds |
| `brand/riva-logo.svg` | "riva" wordmark only, on light backgrounds |
| `brand/riva-logo-white.svg` | "riva" wordmark only, in white |
| `brand/riva-icon.svg` | Square app icon (white mark on a blue tile) |

The site loads the root `logo.svg`, not the copy in `brand/`. If you change the logo, update both.

## Hosting

- **Domain and hosting:** Cloudflare. The site is a Cloudflare Workers project that deploys from this GitHub repo; every push to `main` republishes it.
- **404 page:** `wrangler.jsonc` sets `not_found_handling` to `404-page`, so any unknown address shows `404.html`.
- **Not published:** files listed in `.assetsignore` stay out of the live site.
- **Email:** Zoho Mail (free plan) for `@rivacomputech.com`.
- **Form:** Formspree (`https://formspree.io/f/xvkkjper`). The notification address is set in the Formspree dashboard, not in the code. Formspree endpoints are public by design, and the form has a `_gotcha` honeypot field.
- **Search:** verified in Google Search Console (Domain property, DNS TXT record in Cloudflare). `sitemap.xml` is submitted there.

## Preview locally

```bash
python3 -m http.server 8080
```

Then open <http://localhost:8080>.

## Updating things

| To change | Edit |
| --- | --- |
| Text, phone, hours, prices | `index.html` (search for the words) |
| Phone or email on the business card | `card.html` and `devik-patel.vcf` |
| Address and phone shown to Google | the `application/ld+json` block near the top of `index.html` |
| Social preview image | replace `og.png` (keep 1200×630). Facebook and LinkedIn can take days to refresh; use their debugger tools to speed it up. |
| Logo | replace `logo.svg` and keep the `?v=` number in the links updated so browsers fetch the new one |
| Email signature logo | replace `email/riva-logo.png` with the same file name |

## Notes

- Fonts: Segoe UI Variable on Windows, SF on Apple, Inter elsewhere. Cascadia Code (Windows Terminal's font) for anything monospaced.
- Respects `prefers-reduced-motion` and `prefers-color-scheme`. Visitors can override both in Quick Settings.
- Honesty rules for the copy: 10+ years of experience, no Microsoft certifications claimed, and no testimonials until there are real ones.
