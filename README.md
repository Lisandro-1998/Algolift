# AlgoLift Website

Statische Website. Kein Build, kein Framework, keine Abhängigkeiten.

## Dateien

| Datei | Wofür |
|---|---|
| `index.html` | Die Website |
| `404.html` | Fehlerseite im gleichen Design |
| `assets/` | Video, Bilder, Logo, Icons, Schriften |
| `CNAME` | Domain für GitHub Pages: `algolift.de` |
| `.nojekyll` | verhindert, dass GitHub die Dateien verarbeitet |
| `robots.txt`, `sitemap.xml` | Suchmaschinen |
| `algolift-standalone.html` | Nur zum Ansehen ohne Server. **Nicht hochladen.** |

## Zu GitHub Pages

```bash
git init
git add .
git commit -m "AlgoLift Website"
git branch -M main
git remote add origin https://github.com/DEIN-NAME/algolift.git
git push -u origin main
```

Dann im Repository: **Settings -> Pages -> Source: Deploy from a branch -> main / (root) -> Save.**
Unter *Custom domain* `algolift.de` eintragen und *Enforce HTTPS* aktivieren.

Beim Domain-Anbieter setzen:

| Typ | Name | Wert |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | DEIN-NAME.github.io |

Die DNS-Umstellung braucht bis zu 24 Stunden.

## Assets austauschen

| Datei | Ersetzen durch | Format |
|---|---|---|
| `assets/hero-1080.mp4` | eigenes Hero-Video | MP4, H.264, ohne Ton |
| `assets/hero-mobile.mp4` | dasselbe in 1280 px | MP4, ca. 2 MB |
| `assets/hero-mobile.webm` | dasselbe als WebM | optional |
| `assets/poster.jpg` | Standbild aus dem Video | 1280 px breit |
| `assets/card-a` bis `card-d` | eigene Fotos | 2400 x 1400, links unten ruhig |
| `assets/team.jpg` / `.webp` | Teamfoto | 1200 x 1500 |
| `assets/og.jpg` | Vorschaubild fuers Teilen | 1200 x 630 |

Bei allen Bildern **JPG und WebP** ersetzen, sonst zeigen moderne Browser weiterhin das alte Bild.

Nahtlosen Video-Loop erzeugen (vorwaerts + rueckwaerts):

```bash
ffmpeg -i quelle.mp4 -filter_complex "[0:v]split[a][b];[b]reverse[r];[a][r]concat=n=2:v=1[v]" \
  -map "[v]" -c:v libx264 -crf 18 -preset slow -pix_fmt yuv420p -movflags +faststart -an assets/hero-1080.mp4
```

## Technisch enthalten

Lokale Schriften (kein externer Aufruf), WebP mit JPG-Rueckfall, Lazy Loading, feste Bildmasse, eigene Mobilvariante des Videos, Datensparmodus, funktioniert ohne JavaScript, Burger-Menue, Touchflaechen ab 44 px, Sprungmarke, Open Graph, Twitter Cards, Favicons, JSON-LD (ProfessionalService + WebSite), Canonical, Sitemap, Impressum und Datenschutz als Overlay.

## Noch offen

- Kartenfotos A, C, D sind hochskaliertes Stockmaterial
- Kennzahlen pruefen: "99+ Tage Editing", "5+ Jahre Handwerk", "20 Minuten im Monat"
- Kundenlogos Brugger Holzbau und Unit Baudienste
- Sektionen "Ueber uns" und FAQ fehlen (gut fuer SEO)
