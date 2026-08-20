# VentPro

Buildie-inspirerad fältapp för VA-ventiler. Öppna, välj ventil, välj fel, spara — klart på 10 sekunder. Foto, GPS och tidsstämpel sparas automatiskt, precis som i [Buildie](https://buildie.fi/sv).

Ingen inloggning, ingen kommun-branding — bara ett snabbt verktyg för fältpersonal.

## Flöde

1. **+** öppnar en bottensheet i fyra steg:
   1. Ventiltyp (VAV/VBP stort överst, VSP/DNB/SNB/VSV under) + ventilnummer
   2. Fel (Trasig, Trög, Övertäckt, Betäckning defekt, Ej kontrollerad, Åtgärdad) + valfri detalj
   3. Område (Tullinge/Tumba/Vårsta/Grödinge/Norra), plats (GPS eller fritext), notering, foto
   4. Bekräfta — tid, GPS-koordinater och foto visas automatiskt — **Spara**
2. Rapporten hamnar direkt i karta, listor och statistik. Inget dubbelarbete.

## Vyer

- **Hem** — statistik (Totalt/Trasiga/Tröga/Betäckning/Övertäckt) och senaste 4 rapporter
- **Karta** — mörk Leaflet-karta, färgad markör per ventiltyp, klustring, GPS/Live/Nål/Foto-kontroller, adressökning
- **Åtgärder** — aktiva ärenden grupperade per feltyp
- **Trasiga** — trasiga ventiler, aktiva och åtgärdade
- **Statistik** — KPI:er och fördelning per status/typ
- **Profil** — namn, egna rapporter, anteckningar

Mobilt: mörk vy med flytande bottennav och FAB. Desktop (≥1024px): ljus admin-vy med 260px-sidomeny, karta och lista sida vid sida.

## Teknik

- En enda `index.html` — ingen build, inget npm
- Handskriven CSS (inga UI-ramverk)
- [Leaflet](https://leafletjs.com/) + [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) via CDN, mörka kartplattor från CARTO
- [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts
- Nominatim (OpenStreetMap) för adressökning och omvänd geokodning
- Data sparas lokalt i `localStorage` (`vab8` = ventiler, `vab8u` = användarnamn, `vab8n` = anteckningar) — appen fungerar offline; endast karttiles, adressökning och omvänd geokodning kräver nät

## Köra lokalt

Öppna `index.html` direkt i en webbläsare, eller servera mappen med valfri statisk server, t.ex.:

```bash
python3 -m http.server 8080
```

## Deploy

Statisk sajt utan byggsteg — pushar till `main` deployas direkt av Vercel (`vercel.json` är tom och låter Vercel auto-detektera det statiska projektet).
