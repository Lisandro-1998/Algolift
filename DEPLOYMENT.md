# Algolift Website — Deployment Anleitung

Komplette Schritt-für-Schritt-Anleitung wie du die Website live bringst. Alles über den Browser, kein Terminal nötig.

---

## Was du am Ende hast

Eine live Website auf **algolift.de** mit:
- Auto-Deploy: Du änderst was auf GitHub → 30 Sekunden später ist es live
- Free SSL (HTTPS automatisch)
- Globales CDN (überall schnell)
- Kostenlos für deinen Traffic-Bereich

---

## Was du brauchst

1. Die 7 Dateien aus diesem Lieferpaket (siehe unten)
2. Einen GitHub-Account → [github.com](https://github.com) (kostenlos)
3. Einen Vercel-Account → [vercel.com](https://vercel.com) (kostenlos, mit GitHub einloggen)
4. Zugriff auf den DNS deiner Domain algolift.de

---

## Die 7 Dateien

Alles aus diesem Output-Ordner:

| Datei | Wofür |
|---|---|
| `algolift.html` | Hauptseite — **muss zu `index.html` umbenannt werden** |
| `impressum.html` | Impressum-Page |
| `datenschutz.html` | Datenschutz-Page |
| `sitemap.xml` | Für Google |
| `robots.txt` | Crawler-Regeln |
| `manifest.json` | PWA-Hinweise |
| `founders.webp` | Founder-Foto |

---

## SCHRITT 1 — Dateien vorbereiten (1 Minute)

1. Erstelle einen leeren Ordner auf deinem Computer, z.B. `algolift-website`
2. Kopiere alle 7 Dateien rein
3. **Wichtig:** Benenne `algolift.html` um in `index.html`
   - Mac: rechtsklick → "Umbenennen"
   - Windows: F2-Taste

Der Ordner sollte jetzt so aussehen:

```
algolift-website/
├── index.html         ← war algolift.html
├── impressum.html
├── datenschutz.html
├── sitemap.xml
├── robots.txt
├── manifest.json
└── founders.webp
```

---

## SCHRITT 2 — GitHub-Repo erstellen (3 Minuten)

1. Geh auf [github.com](https://github.com) und login
2. Oben rechts: **"+" → "New repository"**
3. Einstellungen:
   - **Repository name:** `algolift-website`
   - **Description:** `Algolift Website`
   - **Public** auswählen (oder Private, beides geht)
   - Den Haken bei "Add a README file" ✅ setzen
4. Unten klicken: **"Create repository"**

Du landest auf der Repo-Seite. Sieht aus wie ein leeres Repo mit nur einer README.md.

---

## SCHRITT 3 — Dateien hochladen (2 Minuten)

1. Auf der Repo-Seite: **"Add file" → "Upload files"** (Button oben in der Mitte)
2. Drag & Drop **alle 7 Dateien** aus deinem Ordner in das große Feld
   - Wichtig: **Auch `founders.webp` mit reinziehen!** Das ist das Foto.
3. Warte bis alle hochgeladen sind (siehst du am Häkchen)
4. Unten:
   - **Commit message:** `Initial upload`
5. Button klicken: **"Commit changes"**

Nach 5 Sekunden siehst du alle 7 Dateien plus die README im Repo. Wenn `founders.webp` fehlt → nochmal Upload-Button und nur die Datei rüberziehen.

---

## SCHRITT 4 — Auf Vercel deployen (3 Minuten)

1. Geh auf [vercel.com](https://vercel.com)
2. **"Sign Up"** klicken → **"Continue with GitHub"** wählen
3. Vercel fragt nach Permission → "Authorize Vercel" klicken
4. Auf dem Vercel-Dashboard: **"Add New" → "Project"** klicken
5. Du siehst alle deine GitHub-Repos. **`algolift-website`** finden → **"Import"** klicken
6. Auf der nächsten Seite:
   - **Framework Preset:** "Other" auswählen (es ist statisches HTML)
   - **Root Directory:** leer lassen (default)
   - Sonst nichts ändern
7. **"Deploy"** klicken

Vercel buildet jetzt — dauert 20-40 Sekunden. Am Ende siehst du Konfetti 🎉 und einen Link wie `algolift-website-xxx.vercel.app`. Klick drauf → deine Site ist live!

---

## SCHRITT 5 — Custom Domain verbinden (5 Minuten)

Damit `algolift.de` auf die Site zeigt:

### 5a. Auf Vercel:
1. Im Project: **"Settings" → "Domains"**
2. Im Feld: `algolift.de` eintragen → **"Add"**
3. Vercel zeigt dir DNS-Records die du setzen musst. Format:
   - **A Record:** `@` → `76.76.21.21`
   - **CNAME Record:** `www` → `cname.vercel-dns.com`
4. Lass das Fenster offen — wir kommen gleich zurück.

### 5b. Bei deinem Domain-Anbieter (wo du algolift.de gekauft hast):
1. Login bei deinem Provider (z.B. IONOS, GoDaddy, Cloudflare, Strato, etc.)
2. **DNS-Verwaltung** für `algolift.de` öffnen
3. Bestehende A/CNAME Einträge für `@` und `www` **löschen** falls vorhanden
4. Neue Einträge anlegen:
   - **Typ A**, Name `@` (oder leer), Wert `76.76.21.21`
   - **Typ CNAME**, Name `www`, Wert `cname.vercel-dns.com`
5. Speichern

### 5c. Warten:
- DNS braucht 5 Minuten bis 24 Stunden zum Propagieren (meist 15 Min)
- Vercel checkt automatisch und schaltet HTTPS frei sobald die Domain antwortet
- Dann ist `algolift.de` live mit grüner SSL-Plombe ✓

---

## SCHRITT 6 — Was du JETZT noch machen musst

Bevor du die Site komplett live nimmst, tausche diese Platzhalter aus:

### A) Impressum-Platzhalter füllen
Öffne `impressum.html` (auf GitHub direkt: Datei klicken → Stift-Icon zum Bearbeiten):

Suche nach `[Vollständige US-Adresse einfügen` und ersetze:
- Die US-Adresse deiner LLC
- State of Formation (z.B. Delaware, Wyoming)
- LLC Registration Number

Speichern → Vercel deployt automatisch neu.

### B) Bilder hochladen die noch fehlen
Diese 6 Bilder fehlen noch und werden im HTML referenziert. Solange die nicht da sind, gibt's 404er für die Files (aber die Site funktioniert weiter):

| Datei | Größe | Wofür |
|---|---|---|
| `og-image.jpg` | 1200×630px | Vorschau-Bild beim Teilen auf WhatsApp/LinkedIn |
| `favicon.png` | 512×512px | Tab-Icon |
| `favicon.svg` | beliebig | Vektor-Tab-Icon |
| `apple-touch-icon.png` | 180×180px | iPhone Home-Screen-Icon |
| `safari-pinned-tab.svg` | beliebig | Safari Pinned Tab |
| `icon-192.png` + `icon-512.png` | 192×192 / 512×512 | PWA-Icons |

Schnell-Variante: Du brauchst nur ein Logo (am besten als SVG oder hochaufgelöstes PNG), dann nutzt du [realfavicongenerator.net](https://realfavicongenerator.net) — der spuckt alle Varianten in einem Zip aus. Ins Repo hochladen, fertig.

Für `og-image.jpg`: Mach einen Screenshot von deinem Hero (im Browser, 16:9 / 1200×630) oder bau eine simple Brand-Karte in Canva.

### C) Google bei Search Console anmelden
Erst nach Custom-Domain-Setup:
1. [search.google.com/search-console](https://search.google.com/search-console)
2. Property hinzufügen → `algolift.de`
3. Verify (am einfachsten: HTML-Tag-Methode → Code in `<head>` von index.html einfügen)
4. **Sitemaps** → `https://algolift.de/sitemap.xml` einreichen
5. Innerhalb 3-7 Tage taucht die Site in Google auf

---

## So änderst du was nach dem Deployment

Du musst nicht jedes Mal alles neu hochladen. Dank GitHub kannst du:

**Option A: Direkt auf GitHub editieren** (für kleine Sachen)
1. Repo öffnen
2. Datei klicken (z.B. `index.html`)
3. Stift-Icon (rechts oben) → bearbeiten
4. Änderungen machen → unten "Commit changes"
5. Vercel deployt automatisch in ~30 Sekunden

**Option B: Datei ersetzen** (wenn ich dir eine neue Version schicke)
1. Repo öffnen
2. Alte Datei klicken → Mülltonne-Icon → Commit
3. **"Add file" → "Upload files"** → neue Datei hochladen → Commit
4. Vercel deployt automatisch

---

## Troubleshooting

**Bild zeigt 404 / kaputt an:**
- Prüfen ob `founders.webp` im GitHub-Repo wirklich drin ist (nicht nur lokal)
- Dateinamen sind case-sensitive: `founders.webp` ≠ `Founders.webp`

**Domain zeigt noch alte Page oder Fehler:**
- DNS braucht oft Zeit. Mit `https://www.whatsmydns.net/#A/algolift.de` prüfen wo's schon propagiert ist
- Browser-Cache leeren (Cmd+Shift+R / Ctrl+F5)

**Vercel-Deploy schlägt fehl:**
- Auf Vercel → Project → Deployments → letzter Deploy → Logs lesen
- Meistens HTML-Tag-Fehler oder fehlende Datei

**Site ist live aber Cookie-Banner kommt nicht:**
- Browser-DevTools öffnen (F12) → Console → Fehler lesen
- Oft: JavaScript wurde im Browser blockiert

---

## Die wichtigsten Links

- Repo bearbeiten: `https://github.com/DEIN-USER/algolift-website`
- Live-Site: `https://algolift.de` (nach DNS-Setup)
- Vercel Dashboard: `https://vercel.com/dashboard`
- Google Search Console: `https://search.google.com/search-console`
- DNS Check: `https://www.whatsmydns.net/#A/algolift.de`
- Rich Results Test: `https://search.google.com/test/rich-results`

---

## Geschätzter Zeitaufwand

| Schritt | Dauer |
|---|---|
| 1. Dateien vorbereiten | 1 min |
| 2. GitHub-Repo | 3 min |
| 3. Dateien hochladen | 2 min |
| 4. Vercel deployen | 3 min |
| 5. Domain verbinden | 5 min + DNS-Wartezeit (~15 min) |
| 6. Impressum füllen | 5 min |
| 6. Bilder generieren + hochladen | 15 min |
| **TOTAL** | **~30 min aktiv + 15 min DNS-Wartezeit** |

Das ist alles. Bei Stolpersteinen: Frag mich.
