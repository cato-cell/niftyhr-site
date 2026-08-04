# NiftyHR.no – statisk landingsside

## Hva dette er
niftyhr.no er en statisk markedsførings- og hjelpeside som leder nye brukere til å registrere seg i selve appen på niftyhr.io. Den er IKKE appen. Mål: konvertere besøkende til registrerte brukere.

- Appen / registrering / innlogging: https://www.niftyhr.io/auth/login  (ALLE «opprett bruker»- og «logg inn»-CTA-er peker hit)
- Designet er en bevisst kopi av niftyhr.io sitt uttrykk (mørkt, grønn aksent), med egne, mer konverteringsrettede tekster.

## Teknisk stack og deploy
- Ren statisk HTML/CSS. Ingen rammeverk, ingen byggesteg, minimal JS.
- GitHub-repo: cato-cell/niftyhr-site → Cloudflare Pages.
- Cloudflare: production branch = main, build command = tom, output directory = /. Hver commit til main auto-deployer på ~30 sek.
- Live nå: niftyhr-site.pages.dev. Domenet niftyhr.no kobles på senere via Cloudflare → Custom domains.
- Bruk ROT-ABSOLUTTE stier på alle delte ressurser: /style.css, /niftyhr-logo.svg, /video-poster.jpg. Dette gjør at sider i /posts/ også funker.

## Filer
- index.html – forsiden
- style.css – all delt CSS (designtokens, komponenter, .post)
- niftyhr-logo.svg – HVIT logo (brukes på mørk bakgrunn, header + footer)
- niftyhr_logo_white/black.png/svg – kildefiler (svart versjon kun for lyse flater)
- video-poster.jpg – forsidebilde på videoen (Roger Eriksen, daglig leder)
- posts/<slug>.html – blogginnlegg

## Designsystem (allerede definert i style.css)
- Bakgrunn near-black: --bg #0A0A0A, kort --bg-2 #121212, indre --bg-3 #191919
- Tekst: --text #F4F4F4, dempet --muted #9A9A9A, linjer --line rgba(255,255,255,.09)
- Grønn aksent: --green #36B27D, --green-text #6FD3A2, --green-soft/-border/-deep, donut --mint #86D6A6
- Display-font: Space Grotesk (Google Fonts). Brødtekst: systemfont.
- Stil: premium SaaS, skandinavisk dark mode, minimalistisk, mobil-først, god spacing, tydelig CTA. Unngå glow, stockfølelse, falske dashboards, overdesign.

## Innholds- og språkregler
- Språk: norsk bokmål. Tone: rolig, konkret, litt spiss, ingen corporate buzzwords («revolusjonerende», «sømløs», «disruptiv» osv. er forbudt).
- Posisjonering: enkelt, praktisk, AI-forsterket HR for små bedrifter (5–50 ansatte) UTEN HR-avdeling. Ikke «enda et HR-system».
- ALL norsk tekst skal kvalitetssjekkes for særskriving/orddeling, bindestrek og staving før commit.

## Priser (gjeldende modell – speiler forsiden; INGEN permanent gratis-plan)
Inntakshook overalt = «Prøv gratis i 30 dager». Tre bokser på forsiden (Plus / Business / AI):
- **Plus** (inntak / konverteringsfunnel): 30 dager gratis prøve, deretter 49 kr per ansatt/mnd ved årlig forskudd (59 kr ved månedlig), min. 490 kr/mnd, alle bedriftsstørrelser. CTA «Opprett gratis bruker» → /auth/sign-up.
- **Business** (primær inntekt): Fra 490 kr pr mnd, for bedrifter med egne behov (skreddersøm). Alt i Plus + tredjepartsintegrasjoner, skreddersydde løsninger, prioritert support. CTA «Ta kontakt».
- **Nifty AI – Agent 44**: KOMMER – omtales ALDRI som en live funksjon. Tillegg til Plus eller Business. Prisnivåer ved lansering (per bedrift): inntil 15 ansatte 990 kr/mnd · 16–30 ansatte 1 190 kr/mnd · 31+ ansatte 1 490 kr/mnd. CTA «Få beskjed ved lansering».
- VIKTIG: Det finnes IKKE lenger en permanent «Nifty Go»-gratisplan for ≤5 (eller ≤10) ansatte på siden. «Gratis» = 30-dagers prøve. Ikke gjeninnfør gamle gratis-grenser.

## Lenker/CTA (viktig)
- «Opprett gratis bruker»-CTA-er → https://www.niftyhr.io/auth/sign-up
- «Logg inn» → https://www.niftyhr.io/auth/login

## Faste fakta (footer/kontakt)
- «NiftyHR, et produkt av Heisenbug®»
- team@niftyhr.io · +47 934 29 773 · Org. nr. 934 476 336
- Heisenbug: https://heisenbug.no/ · LinkedIn: https://www.linkedin.com/company/nifty-hr/ · Vilkår: https://www.niftyhr.io/betingelser

## Forsidens seksjoner
Header (logo + Logg inn + «Opprett gratis bruker») · Hero (overskrift + 2 CTA + 30-dagers-prøve-hook + trygghetsstripe + CSS-preview av ferie/fravær med donut) · Funksjoner (6 kort) · Video (YouTube-id rPUGB4fkIVI, klikk-for-å-spille, poster = /video-poster.jpg) · Priser (3 bokser: Plus/Business/AI) · Artikler (5 kort → /posts/) · FAQ (7 spørsmål) · Slutt-CTA · Footer.

## Blogg
5 innlegg i /posts/, samme slugs som niftyhr.io, delt style.css + .post-stiler, hver med CTA til registrering nederst og «Tilbake til forsiden»-lenke.

## Status (faktisk repo-tilstand pr. nå)
- [x] Forside (index.html) – ferdig og live
- [x] style.css utskilt og lenket fra alle sider (index.html + alle /posts/)
- [x] 5 blogginnlegg i /posts/ opprettet og lenket fra forsiden
- [x] Rest-mappene «LOGO NIFTHR» og «NiftyHr site» slettet
- [x] SEO-grunnoppsett gjort: robots.txt, sitemap.xml, 404.html, canonical + JSON-LD (Organization/WebSite på forsiden, BlogPosting på hvert innlegg)
- [x] Footer-lenker riktige på forside + 404 (LinkedIn .../company/nifty-hr/, Heisenbug heisenbug.no, Vilkår niftyhr.io/betingelser)
- [x] Kontaktnummer +47 934 29 773 overalt; video rPUGB4fkIVI; sign-up-CTA → /auth/sign-up
- [ ] Footer-lenker i /posts/ – GJENSTÅR: de 5 blogginnleggene har fortsatt gamle footer-lenker (LinkedIn generisk, «Gå til niftyhr.io», Vilkår → niftyhr.io)
- [ ] Domenet niftyhr.no koblet i Cloudflare – ikke gjort (kjører foreløpig på niftyhr-site.pages.dev)

## Gjenstående SEO (nice-to-have, ikke grunnoppsett)
Grunnoppsettet er på plass. Mulige neste steg: OG-bilde (og:image), flere strukturerte data, ytelse/Lighthouse-finpuss.

## Arbeidsmåte
Konklusjon først, korte og konkrete svar. Lever komplett kode. Foreslå enklere løsning når den finnes.

**Git-regel:** Commit og push ALLTID direkte til `main` når en endring er ferdig – det deployer siden. Ikke lag feature-branch eller PR med mindre Cato ber om det. Unntak: hvis endringen er risikabel (større omskriving, noe som kan brekke forsiden, noe som er vanskelig å reversere), lag branch + PR og si fra hvorfor.
