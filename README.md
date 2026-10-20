# AUTOSERVICE

Landing page (alpha) for **Autoservice Oleh**, Kärntner Straße 105, 8053 Graz.

Domain: **autoserviceoleh.at** (registered at internex). Hosting: **Cloudflare Pages** (free plan), see [Hosting on Cloudflare Pages](#hosting-on-cloudflare-pages).

- `index.html` – single-page site (German), no build step. Open it in a browser or serve the folder statically.
- „Ohne Termin“ block (right after the yellow offer strip): oil change, tyre service and wheel alignment need no appointment, each card carries an orange stamp (inline SVG; ring text on `#stamp-ring`, rough ink from the `#stamp-ink` filter, colour `--stamp-orange`). All other services are by appointment; prices are given on request. The header menu shows from 1100 px; below that the jump links under the header take over.
- `uk.html` – the same page in Ukrainian; the header has a DE/UA switch. It uses self-hosted Montserrat (Poppins has no Cyrillic). The legal pages stay German.
- `impressum.html`, `datenschutz.html` – **drafts** of the Impressum and the Datenschutzerklärung (same look as the landing page, `noindex`, visible draft notice). Every missing fact is marked with a yellow „[bitte ergänzen: …]“ / „[bitte bestätigen: …]“ placeholder.
- `assets/logo/` – vector logo (SVG) in stacked and horizontal lockups, each in on-blue, on-light, mono-white and mono-blue, plus transparent PNG exports (600/1200 px).
- `assets/og-image.jpg` – 1200 × 630 link-preview image (Open Graph) for WhatsApp, Telegram, Facebook: stacked on-blue logo on `#042871`, address and phone in Poppins.
- `favicon.*`, `apple-touch-icon.png`, `icon-*.png`, `site.webmanifest` – browser and app icons.
- `assets/fonts/` – self-hosted Poppins (German page) and Montserrat with Cyrillic (Ukrainian page), both OFL. No request goes to Google Fonts.
- `assets/img/` – photos from the company Instagram @oleh_auto_graz. The page serves the WebP versions (`*-600.webp` and `motorraum-mpi.webp` for the gallery and „Über uns“, `werkstatt-hebebuehne-900.webp` for the hero) through `<picture>`; the `.jpg` files are the fallback for old browsers.

Privacy: the page sets no cookies and loads no tracking. The map in the Kontakt section is an OpenStreetMap embed that shows right away (`loading="lazy"`, `referrerpolicy="no-referrer"`); no request goes to Google. The „Route in Google Maps“ links are plain links. The marker sits at 47.052372, 15.416799 (the workshop); to move it, change `bbox` and `marker` in the iframe `src` in `index.html` and `uk.html`.

Logo notes: "AUTOSERVICE" is Montserrat ExtraBold 800 converted to outlines; "Oleh" is the client's own brush lettering, vectorised from the original sign (it is not a font — always use the logo files). On white use the `-on-light` files; below 32 px use `favicon.svg` / the on-blue mark.

## Open items before going live

- **Impressum und Datenschutz**: fill in all placeholders, have both drafts checked legally, then remove the draft notice and the `<meta name="robots" content="noindex">` line. Missing facts:
  - name of the owner or company name (Firmenwortlaut) and legal form,
  - e-mail address (required by § 5 Abs. 1 Z 3 ECG; also used in the Datenschutzerklärung). Once it exists, it can also go into the Kontakt section of `index.html` as a `mailto:` link,
  - Gewerbeberechtigung (wording from the GISA extract, possibly a separate one for the towing service) and GISA-Zahl,
  - Berufsbezeichnung and the state that granted it (§ 5 Abs. 1 Z 6 ECG; the draft says „verliehen in Österreich“, to be confirmed),
  - who took the photos and who holds the rights to them and to the logo (Bildnachweis in the Impressum),
  - confirm Magistrat Graz as Gewerbebehörde, and the Wirtschaftskammer membership (WKO Steiermark, Fachgruppe/Innung),
  - UID number, Firmenbuch number and court – only if they exist,
  - hosting provider: Cloudflare is filled in; confirm the address, the Data Processing Addendum and the Data Privacy Framework certification, and add the log retention,
  - check the RIS link to the GewO and the statement on the EU-US Data Privacy Framework.
- **Opening hours**: not known yet. Add them to the Kontakt section and as `openingHoursSpecification` in the JSON-LD block of `index.html`.
- **Connect the domain**: canonical, `og:url`, `og:image`, `hreflang`, the JSON-LD `url`/`image` and the vCard already point at `https://autoserviceoleh.at/` (German) and `https://autoserviceoleh.at/uk` (Ukrainian). They only work once the steps in [Hosting on Cloudflare Pages](#hosting-on-cloudflare-pages) are done.
- **Photos**: the gallery („Einblicke“) still repeats the hero photo (Werkstatt with lift). The Mercedes engine, which is also in „Über uns“ just above, was replaced by `motorraum-mpi.jpg/.webp`, the sticker-free top part of an Instagram post (436 × 582 px, so slightly soft on high-density tablets). The other Instagram posts carry text overlays, stickers or effects; ask the client for one or two more clean workshop photos (ideally 900 px wide or more) and use one in place of the gallery copy of `werkstatt-hebebuehne`.

## Hosting on Cloudflare Pages

The site has no build step, so Cloudflare Pages serves the repository root as it is. Set it up once:

1. **Cloudflare account** (free plan), ideally on an e-mail address of the business so it can be handed over.
2. **Add the domain to Cloudflare**: dashboard → *Add a domain* → `autoserviceoleh.at` → *Free*. Cloudflare then shows two nameservers (`….ns.cloudflare.com`).
3. **Point the domain at Cloudflare in internex**: [internex terminal](https://terminal.internex.com) → top menu *Domain & E-Mail* → *Domain Manager Pro* → `autoserviceoleh.at` → nameservers → enter the two Cloudflare nameservers. This switches off internex's own DNS for the domain. The change can take up to 24 hours; Cloudflare sends an e-mail when the domain is active.
4. **Create the Pages project**: *Workers & Pages* → *Create* → *Pages* → *Connect to Git* → GitHub → `CyrexxOne/AUTOSERVICE`.
   - Production branch: `main`
   - Framework preset: *None*
   - Build command: leave empty (or `exit 0`)
   - Build output directory: `/` (the repository root, where `index.html` is)
5. **Custom domain**: in the Pages project → *Custom domains* → add `autoserviceoleh.at`, then `www.autoserviceoleh.at`. Send `www` to the bare domain with *Rules* → *Redirect Rules* → template *Redirect from WWW to root*, because the canonical URLs use `https://autoserviceoleh.at/`.
6. **E-mail (optional, free)**: *Email* → *Email Routing* → forward e.g. `info@autoserviceoleh.at` to the owner's mailbox. That address can then go into the Impressum and the Datenschutzerklärung.

Every push to `main` then deploys automatically. Cloudflare Pages serves `uk.html` as `/uk` and `index.html` as `/` (the `.html` links in the pages still work, they redirect). Once the site runs on the domain, `.github/workflows/pages.yml` (the old GitHub Pages deploy) can be deleted; until then the GitHub Pages copy stays online, and its canonical tags point search engines at the domain.
