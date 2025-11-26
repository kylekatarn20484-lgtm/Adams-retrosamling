# Adams retrosamling

En personlig katalog över datorer, prylar, spel & programvara och datorbyggen. Projektet är byggt i React + TypeScript (Vite) och använder ett enkelt PHP-API för att lagra data i en lokal JSON-fil samt hantera bilduppladdningar.

Syftet med projektet är att göra en helt portabel, privat samling som lätt kan flyttas mellan domäner, servrar och användare.

---

## Funktioner

- Skapa, redigera och ta bort prylar, spel och datorbyggen  
- Stöd för flera bilder per objekt  
- Huvudbild per objekt  
- Bildsortering och selektiv borttagning  
- Olika vyer:
  - Prylar  
  - Datorbyggen  
  - Spel & programvara (kortvy och hyllvy)  
- Avancerad filtrering:
  - Sökfält
  - Kategori
  - Status
  - Plattform
  - Monteringsstatus (lösa delar / monterade i datorer)
- Export / import av hela samlingen som JSON  
- Enkel lösenordsinloggning via PHP-session  

---

## Tekniköversikt

Frontend:
- React
- TypeScript
- Vite

Backend:
- PHP (`api.php`)
- JSON-lagring (`data.json`)
- Bilduppladdning via `upload.php`
- Bilder lagras i `uploads/`

Ingen databas behövs – allt körs via filer.

---

## Mappstruktur

På servern ska filerna ligga så här:

/
index.html
api.php
upload.php
data.json
/assets
/uploads

I GitHub-repo:t finns dessa viktiga mappar/filer:

- `src/` – källkod till frontenden
- `deploy/` – färdig version att ladda upp direkt till webbhotell
- `api.php` – backend för data
- `upload.php` – backend för bilder
- `data.json` – datalagring

---

## Installation på webbhotell

### Steg 1 – Skapa webbplats

1. Skapa en domän eller subdomän hos ditt webbhotell, exempel:
   - `retro.dindomän.se`
2. Peka domänen mot en tom mapp.

### Steg 2 – Ladda upp filer

Från `deploy/`-mappen, ladda upp följande till webbplatsens dokumentrot:

- `index.html`
- hela mappen `assets/`
- `api.php`
- `upload.php`
- `data.json`
- mappen `uploads/` (kan vara tom)

### Steg 3 – Filrättigheter

Servern måste få skriva till:

- `uploads/`-mappen  
- `data.json`

Vanliga rättigheter är:

- mappar: `755` eller `775`
- filer: `664` eller `666`

---

## Konfiguration

### API-anslutning

I `src/App.tsx` används relativa adresser till API:t:

```ts
const API_URL = "/api.php";
const UPLOAD_URL = "/upload.php";

### Steg 4 – Lösenord

Öppna api.php och leta upp raden:
$PASSWORD = 'byt-mig';

Ändra till ett eget lösenord, t.ex.:
$PASSWORD = 'EttRiktigtStarktLösenord123!';

Detta lösenord används för att logga in i webbgränssnittet.

Alla som kör sin egen kopia av projektet bör ändra lösenordet.

### Steg 5 – Användning

	1.	Gå till din domän i webbläsaren.
	2.	Logga in med lösenordet du ställde in i api.php.
	3.	Börja lägga till prylar, spel och datorbyggen.
	4.	Ladda upp bilder – de lagras i uploads/.

  Export och import

Export

Via knappen Exportera laddas en JSON-fil ner med:
	•	alla prylar
	•	alla spel
	•	alla datorbyggen

(observera: bildfilerna följer inte med – endast länkar till dem)

Backup

För en komplett backup:
	•	spara exporterad JSON-fil
	•	kopiera hela mappen uploads/

Återställning / flytt

För att flytta samlingen till ny server:
	1.	Ladda upp koden (index.html, assets, api.php, upload.php)
	2.	Kopiera över uploads/
	3.	Importera JSON-filen via Importera i gränssnittet
eller klistra in innehållet direkt i data.json.

Uppdatera / bygga projektet

Endast nödvändigt om du vill ändra i källkoden.

Installera beroenden
npm install

Köra lokalt
npm run dev

Bygga produktion
npm run build

Efter build:
	•	mappen dist/ innehåller färdig frontend
	•	kopiera innehållet till deploy/ tillsammans med:
	•	api.php
	•	upload.php
	•	data.json
	•	uploads/

  Prestanda och skalning

Ungefärliga riktvärden:
	•	0–2 000 objekt: mycket snabbt, även på mobil
	•	2–5 000 objekt: fullt användbart, något längre laddningar kan märkas
	•	5 000+ objekt: fungerar, men kan börja kännas tungt – då rekommenderas att byta till riktig databaslösning
