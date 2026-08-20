# VentPro

Buildie-inspirerad fältapp för VA-ventiler. Öppna, välj ventil, välj fel, spara — klart på 10 sekunder. Foto, GPS och tidsstämpel sparas automatiskt, precis som i [Buildie](https://buildie.fi/sv).

Ingen inloggning, ingen kommun-branding — bara ett snabbt verktyg för fältpersonal.

## Flöde

**Foto-först (kamera-pillen på kartan)** — den snabbaste vägen, Buildie-stil:
1. Tryck kamera-pillen nere höger på kartan → telefonens kamera öppnas direkt
2. Foto tas → en snabbrapport-sheet öppnas automatiskt med foto + GPS + tid redan ifyllt
3. Typ + nummer, problem + detalj, fritext-notering → **Spara**
4. Rapporten hamnar direkt som en "foto-notis" på kartan: en markör färgad och symboliserad efter problemet (röd kors = trasig, orange varning = trög, gul = övertäckt, grå skiftnyckel = betäckning defekt, vit frågetecken = ej kontrollerad, grön bock = åtgärdad). Finns foto visas det som rund miniatyr i markören med färgad ram. Nya markörer (<5 min) pulserar.

**Fullständig rapport (+ -knappen)** — för manuell registrering med område/plats:
1. Ventiltyp (VAV/VBP stort överst, VSP/DNB/SNB/VSV under) + ventilnummer
2. Fel (Trasig, Trög, Övertäckt, Betäckning defekt, Ej kontrollerad, Åtgärdad) + valfri detalj
3. Område (Tullinge/Tumba/Vårsta/Grödinge/Norra), plats (GPS eller fritext), notering, foto
4. Bekräfta — tid, GPS-koordinater och foto visas automatiskt — **Spara**

Klick på en markör öppnar en liten ruta: titel, färgad problem-badge, fritext, klickbar fotominiatyr (fullskärm), tid/vem/GPS, samt Visa detaljer / Rutt / Radera. Allt hamnar direkt i karta, listor och statistik — inget dubbelarbete.

## Vyer

- **Hem** — statistik (Totalt/Trasiga/Tröga/Betäckning/Övertäckt) och senaste 4 rapporter
- **Karta** — mörk Leaflet-karta, foto-notis-markörer färgade per problem, klustring, GPS/Live/Nål/Foto-kontroller, adressökning
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
- Foton komprimeras client-side (canvas, max 800px, JPEG-kvalitet 0.7) innan de sparas som base64

## Köra lokalt

Öppna `index.html` direkt i en webbläsare, eller servera mappen med valfri statisk server, t.ex.:

```bash
python3 -m http.server 8080
```

## Deploy

Statisk sajt utan byggsteg — pushar till `main` deployas direkt av Vercel (`vercel.json` är tom och låter Vercel auto-detektera det statiska projektet).
