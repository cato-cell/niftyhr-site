# CLAUDE.md – niftyhr-site

Instruks for Claude Code som styrer nettsiden og blogg-publisering for NiftyHR.

---

## 1. Hva dette repoet er

Rent statisk nettsted (HTML + CSS, ingen byggesteg, ingen framework). Hostet på Cloudflare Pages, deploy skjer automatisk ved merge til `main`.

**Domener:**
- `niftyhr.no` = offentlig landingsside (dette repoet). Skal erstatte .io som forside.
- All registrering/innlogging går til `https://www.niftyhr.io/auth/login` (appen – eget system, ikke dette repoet).
- Canonical for alt innhold = `https://niftyhr.no/...`

**Struktur:**
```
/index.html              forside (inkl. liste "Artikler og nyheter")
/style.css               felles styling
/posts/{slug}.html       én fil per bloggpost
/sitemap.xml             genereres/oppdateres manuelt (ingen build)
/robots.txt
/404.html
/niftyhr-logo.svg + logo-varianter
```

Fordi det ikke finnes byggesteg: **agenten skriver alle filer direkte.** Sitemap, forside-liste og robots oppdateres som vanlige filer i samme PR.

---

## 2. Arbeidsflyt – ny bloggpost

Hver ny post skjer i **én PR** og må gjøre alle fire stegene, ellers henger ting ikke sammen:

1. Opprett `posts/{slug}.html` fra malen i punkt 4.
2. Legg posten **øverst** i «Artikler og nyheter»-listen i `index.html` (nyeste først).
3. Legg URL-en til i `sitemap.xml`.
4. Skriv kvalitetsrapport (punkt 6) i PR-beskrivelsen + flagg om juridisk kontroll trengs.

**Slug-regel:** små bokstaver, bindestrek, æ→a/ø→o/å→a, ingen filendelse i selve slug-navnet (filen får `.html`). Eks: `de-fleste-sma-bedrifter-bryter-hr-regler-uten-a-vite-det.html`.

**Branch:** `blogg/{slug}`. **PR-tittel:** `Blogg: {tittel}`.

Aldri commit direkte til `main`. Cato merger = godkjenning = publisert.

---

## 3. Innholdsregler (brand)

Posisjonering: **enkelt, praktisk, AI-støttet HR-system små bedrifter faktisk bruker.** Aldri «nok et HR-system».

Målgruppe: daglige ledere, gründere, småbedrifter 5–50 ansatte uten egen HR-avdeling.

Struktur i hver post: **Problem → innsikt → praktisk løsning.** Start alltid med et reelt SMB-problem, ikke med produktet.

**Tone:**
- Naturlig norsk – aldri oversatt-engelsk følelse.
- Rolig, ærlig, konkret. Nordmenn er skeptiske til overdrevne løfter.
- Korte avsnitt. Sterk første setning.

**Bruk gjerne vinkler som:**
- «Mange små bedrifter har ikke et HR-problem. De har et hukommelsesproblem.»
- «Det farligste HR-systemet i en liten bedrift er hodet til daglig leder.»
- «Excel fungerer helt fint. Helt til noen slutter, blir syk eller skal følges opp.»

**Unngå alltid:** «revolusjonerende», «banebrytende», «disruptiv», «fremtiden for arbeid», «alt-i-ett HR-suite», «AI-drevet transformasjon», corporate floskler, AI-hype.

**Pris (hvis nevnt):** «gratis for inntil 10 ansatte, deretter 49 kr per ansatt/mnd». Alltid **ett bestemt tall** – aldri intervall.

**Agent44 (hvis nevnt):** operativ AI-medarbeider, ikke chatbot. Eies av Heisenbug AS, ikke NiftyHR. Omtales som **neste steg / kommende**, ikke som ferdig integrert funksjon. Ikke oversell.

**CTA:** myk, mot slutten. Standard: «Kom i gang med NiftyHR gratis for inntil 10 ansatte» → knapp til `https://www.niftyhr.io/auth/login`.

---

## 4. Post-mal

Bruk eksakt denne strukturen. Bytt ut `{{...}}`. Behold topbar, CTA og klassenavn likt eksisterende poster.

```html
<!DOCTYPE html>
<html lang="no">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{{TITTEL}} – NiftyHR</title>
<meta name="description" content="{{META_BESKRIVELSE_MAKS_155_TEGN}}">
<link rel="canonical" href="https://niftyhr.no/posts/{{SLUG}}.html">
<meta property="og:title" content="{{TITTEL}}">
<meta property="og:description" content="{{META_BESKRIVELSE_MAKS_155_TEGN}}">
<meta property="og:type" content="article">
<meta property="og:url" content="https://niftyhr.no/posts/{{SLUG}}.html">
<meta property="og:image" content="https://niftyhr.no/nifty_preview.png">
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{TITTEL}}",
  "description": "{{META_BESKRIVELSE}}",
  "datePublished": "{{ISO_DATO}}",
  "author": { "@type": "Organization", "name": "NiftyHR" },
  "publisher": { "@type": "Organization", "name": "NiftyHR" },
  "mainEntityOfPage": "https://niftyhr.no/posts/{{SLUG}}.html"
}
</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="/style.css">
</head>
<body>
  <div class="topbar"><div class="topbar-inner">
    <a class="logo-link" href="/" aria-label="NiftyHR"><img class="logo-img" src="/niftyhr-logo.svg" alt="NiftyHR"></a>
    <a class="btn btn-green" href="https://www.niftyhr.io/auth/login">Logg inn</a>
  </div></div>

  <article class="post wrap">
    <a class="back" href="/">← Tilbake til forsiden</a>
    <div class="date">{{DATO_NORSK}}</div>
    <h1>{{TITTEL}}</h1>
    <div class="body">
      {{BRØDTEKST_I_P_OG_UL_TAGGER}}
    </div>
    <div class="cta">
      <h3>Klar til å få kontroll på HR?</h3>
      <p>Kom i gang med NiftyHR gratis for inntil 10 ansatte.</p>
      <a class="btn btn-green" href="https://www.niftyhr.io/auth/login">Opprett bruker gratis →</a>
    </div>
  </article>
</body>
</html>
```

Endring fra dagens maler: **canonical-tag** og **JSON-LD Article** er lagt til (manglet før).

---

## 5. Juridisk og faglig kontroll

Agenten skal **aldri**:
- finne på lover, regler, statistikk eller kilder
- fremstille usikker info som fakta

Ved temaer som berører norsk lovverk, HR-compliance, sykefravær, arbeidsavtaler eller personvern/GDPR:
- skill mellom faktum, anbefaling og praktisk råd
- **flagg posten `JURIDISK KONTROLL: JA`** i PR-beskrivelsen
- ikke skriv konkrete lovhenvisninger uten at de er verifisert

Cato/fagperson må godkjenne juridisk-flaggede poster manuelt før merge.

---

## 6. Kvalitetsport

Hver post vurderes før PR. Skår 1–10 på: relevans, faglig nøyaktighet, SEO, lesbarhet, naturlig norsk, originalitet, NiftyHR-relevans, CTA, «føles ikke AI-generert».

**Poster under 8/10 går ikke i PR.** Skriv om først.

PR-beskrivelse skal inneholde:
```
Tittel: ...
Slug: ...
Primært søkeord: ...
Kvalitetsskår: x/10
Svakheter: ...
JURIDISK KONTROLL: JA/NEI
```

---

## 7. Engangsoppgaver (gjør én gang nå)

1. **Legg til `robots.txt`** i rot:
   ```
   User-agent: *
   Allow: /
   Sitemap: https://niftyhr.no/sitemap.xml
   ```
2. **Opprett `sitemap.xml`** med forside + alle 5 eksisterende poster (canonical niftyhr.no-URL-er).
3. **Opprett `404.html`** og fjern evt. catch-all (`/* /index.html 200` i `_redirects`, eller «Single Page App»-modus i Cloudflare Pages). Nå returnerer ukjente URL-er forsiden med status 200 – det skal være ekte 404. Sjekk Pages-innstillinger hvis `_redirects` ikke finnes.
4. **Etterfyll de 5 eksisterende postene** med `canonical`-tag + JSON-LD (de mangler begge).

---

## 8. Responsstil til Cato

Kort, konkret, direkte. Konklusjon først. Maks 1–3 anbefalinger. Si ifra hvis noe er svakt. Ikke bygg mer kompleksitet enn nødvendig.
