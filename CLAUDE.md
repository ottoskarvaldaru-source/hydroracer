# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

HydroRacer — Eesti esimene vesinikuvõistluspaat. TalTech TiVo üliõpilasmeeskond, sihiks Monaco Energy Boat Challenge 2027.

## Dev server

```bash
python3 -m http.server 3000 --directory website
```

Leht: http://localhost:3000 (konfigureeritud `.claude/launch.json`-s)

## Struktuur

```
website/
  index.html        # Kogu sait — üks fail, kõik CSS/JS inline
  images/
    hydroracer-logo.jpg   # Hero taustapilt
    tivo-logo.jpg         # TiVo logo (mix-blend-mode: screen)
    hydroteam.jpeg        # Meeskonnafoto
luksusjaht.png, cp.png, taltech.png ...  # Partnerite logod (juurkaustas)
```

## Arhitektuur

Üheleheline staatiline HTML/CSS/JS sait ilma build-tööriistadeta.

**`website/index.html`** sisaldab kõike ühes failis:
- `<style>` — kogu CSS (~1200 rida), CSS muutujad `:root`-is
- `<body>` — sektsioonid järjekorras: nav → hero → missioon → meeskond → alammeeskonnad → tehnoloogiad → monaco → ajakava → partnerid → kontakt → footer
- `<script>` — scroll reveal (IntersectionObserver), counter-animatsioon, nav burger, kontaktvormi valideerimine, back-to-top nupp

## Brändi värvid (CSS muutujad)

```css
--cyan:   #3CC8E8   /* põhivärv */
--orange: #E8682C   /* aktsent, HYDRO[R][A]CER tähed Y ja A */
--dark:   #06090D   /* tume taust */
--light:  #0D1B28   /* ookeani sinine sektsioonide taust */
```

## Logo

- **HYDRORACER** — puhas CSS tekst (`Space Grotesk` font), Y ja A tähed `--orange`-s, klass `.brand-logo-sm` (nav) / `.brand-logo-lg` (hero)
- **TiVo** — `images/tivo-logo.jpg` + `mix-blend-mode: screen`
- **Hero taust** — `images/hydroracer-logo.jpg` CSS `background-image`-na `.hero`-l

## Sektsioonide CSS klassid

- `.section--dark` → `--dark` taust
- `.section--light` → `--light` taust  
- `.section--light-alt` → `--light-s` taust
- `.reveal` → scroll-animatsioon (IntersectionObserver lisab `.visible` klassi)
- `.reveal-delay-1` kuni `.reveal-delay-4` → stagger-viited

## Deploy

GitHub: `ottoskarvaldaru-source/hydroracer` (haru `main`)  
GitHub Pages: `index.html` juurkaustas redirectib `website/`-le
