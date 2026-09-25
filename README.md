# AUTOSERVICE

Landing page (alpha) for **Autoservice Oleh**, Kärntner Straße 105, 8053 Graz.

- `index.html` – single-page site (German), no build step. Open it in a browser or serve the folder statically.
- `uk.html` – the same page in Ukrainian; the header has a DE/UA switch. It uses self-hosted Montserrat (Poppins has no Cyrillic). The legal pages stay German.
- `impressum.html`, `datenschutz.html` – **drafts** of the Impressum and the Datenschutzerklärung (same look as the landing page, `noindex`, visible draft notice). Every missing fact is marked with a yellow „[bitte ergänzen: …]“ / „[bitte bestätigen: …]“ placeholder.
- `assets/logo/` – vector logo (SVG) in stacked and horizontal lockups, each in on-blue, on-light, mono-white and mono-blue, plus transparent PNG exports (600/1200 px).
- `assets/og-image.jpg` – 1200 × 630 link-preview image (Open Graph) for WhatsApp, Telegram, Facebook: stacked on-blue logo on `#042871`, address and phone in Poppins.
- `favicon.*`, `apple-touch-icon.png`, `icon-*.png`, `site.webmanifest` – browser and app icons.
- `assets/fonts/` – self-hosted Poppins (German page) and Montserrat with Cyrillic (Ukrainian page), both OFL. No request goes to Google Fonts.
- `assets/img/` – photos from the company Instagram @oleh_auto_graz. The page serves the WebP versions (`*-600.webp` and `motorraum-mpi.webp` for the gallery and „Über uns“, `werkstatt-hebebuehne-900.webp` for the hero) through `<picture>`; the `.jpg` files are the fallback for old browsers.

Privacy: the page sets no cookies and loads no tracking. Google Maps is a two-click embed: the iframe is only inserted after the visitor clicks „Karte laden“ (with `referrerpolicy="no-referrer"`); the „Route in Google Maps“ links are plain links.

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
  - hosting provider (name, address, log retention, Auftragsverarbeitungsvertrag, server location),
  - check the RIS link to the GewO and the statement on the EU-US Data Privacy Framework.
- **Preise bestätigen und USt.-Angabe ergänzen**: the prices („ab 50 € / 80 €“, „Stand April 2026“) are from Instagram, and the date is several months old. Confirm the prices, update the month and state whether they include 20 % USt. (e.g. „Richtpreise inkl. 20 % USt., Stand … 2026“).
- **Opening hours**: not known yet. Add them to the Kontakt section and as `openingHoursSpecification` in the JSON-LD block of `index.html`.
- **Domain**: once the domain is known, make `og:image` (and the JSON-LD `image`) an absolute URL, e.g. `https://<domain>/assets/og-image.jpg`, and add `og:url`, `<link rel="canonical">` and the JSON-LD `url`. Link previews do not show the image until then.
- **Photos**: the gallery („Einblicke“) still repeats the hero photo (Werkstatt with lift). The Mercedes engine, which is also in „Über uns“ just above, was replaced by `motorraum-mpi.jpg/.webp`, the sticker-free top part of an Instagram post (436 × 582 px, so slightly soft on high-density tablets). The other Instagram posts carry text overlays, stickers or effects; ask the client for one or two more clean workshop photos (ideally 900 px wide or more) and use one in place of the gallery copy of `werkstatt-hebebuehne`.
