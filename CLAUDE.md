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

## Priser (ENESTE gyldige tall – aldri vis intervaller)
- Nifty Go: Gratis, kostnadsfritt opptil 10 ansatte
- Nifty Plus: 49,- per ansatt/mnd, for bedrifter med flere enn 10 ansatte
- Nifty Business: Ta kontakt
- SMS-portal: fra 0,59 per SMS
- Agent44 (AI): omtales kun som KOMMENDE/neste steg – ALDRI som en live funksjon.

## Faste fakta (footer/kontakt)
- «NiftyHR, et produkt av Heisenbug®»
- team@niftyhr.io · +47 411 15 411 · Org. nr. 934 476 336
- Heisenbug: https://heisenbug.no/ · LinkedIn: https://www.linkedin.com/company/nifty-hr/ · Vilkår: https://www.niftyhr.io/betingelser

## Forsidens seksjoner
Header (logo + Logg inn) · Hero (overskrift + 2 CTA + gratis-hook + CSS-preview av ferie/fravær med donut) · Funksjoner (6 kort) · Video (YouTube-id JD3lNTJsqsw, klikk-for-å-spille, poster = /video-poster.jpg) · Priser (3 tiers) · Artikler (5 kort → /posts/) · FAQ (7 spørsmål) · Footer.

## Blogg
5 innlegg i /posts/, samme slugs som niftyhr.io, delt style.css + .post-stiler, hver med CTA til registrering nederst og «Tilbake til forsiden»-lenke.

## Status (faktisk repo-tilstand pr. nå)
- [x] Forside (index.html) – ferdig og live
- [x] style.css utskilt og lenket fra alle sider (index.html + alle /posts/)
- [x] 5 blogginnlegg i /posts/ opprettet og lenket fra forsiden
- [x] Rest-mappene «LOGO NIFTHR» og «NiftyHr site» slettet (allerede gjort)
- [ ] Footer-lenker satt riktig – IKKE gjort ennå: LinkedIn peker til generisk linkedin.com (skal være .../company/nifty-hr/), Heisenbug-lenke mangler helt, og «Vilkår» peker til niftyhr.io (skal være niftyhr.io/betingelser)
- [ ] Domenet niftyhr.no koblet i Cloudflare – ikke gjort (kjører foreløpig på niftyhr-site.pages.dev)

## Gjenstående SEO-grunnoppsett (engangsjobb)
Ingen av disse finnes i repoet ennå – alt gjenstår: robots.txt, sitemap.xml, 404.html, canonical-tag og JSON-LD på sidene.

## Arbeidsmåte
Konklusjon først, korte og konkrete svar. Lever komplett kode. Foreslå enklere løsning når den finnes. Commit til main når en endring er ferdig (det deployer siden).
