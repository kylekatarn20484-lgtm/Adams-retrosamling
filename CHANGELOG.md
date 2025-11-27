# Changelog

Alla större ändringar i **Adams retrosamling** dokumenteras här.

Formatet följer ungefär *Keep a Changelog* och semantisk versionshantering.

---

## [3.1.0] – 2025

### Added
- Stöd för att välja **befintliga bilder** via popup i både:
  - Prylar
  - Spel & programvara
  - Datorbyggen
- Möjlighet att markera flera bilder samtidigt.
- Grön markering på valda bilder i bildväljaren.

### Changed
- Förbättrad placering av knappar för bättre balans i formulär.
- Förenklat gränssnitt genom att ta bort onödiga snabbfilter.
- Kategorinamn uppdaterade:
  - `Projektmaskin` → `Projekt`
  - `Lånad ut` → `Utlånad`
  - Ny status: `I förvaring`

### Fixed
- Fixade problem där knappen *”Välj bland befintliga bilder…”* inte gick att klicka på.
- Åtgärdade trasiga handlers för bildval i datorbyggarvyn.
- Fix för att befintliga bilder inte visades korrekt i vissa formulär.
- Små UI-buggar i mobil- och desktoplayouter.

---

## [3.0.0] – 2025

### Added
- Separata vyer för:
  - Prylar
  - Datorbyggen
  - Spel & programvara
- Hyllvy och kortvy för spel.
- Stöd för lösenordsskydd via PHP-session.
- Export av hela samlingen som JSON.

### Changed
- Ombyggt hela UI:t till mörkt tema.
- Förbättrad mobilanpassning.
- Footer uppdaterad med versionsnummer.

---

## [2.x.x] – 2025

### Added
- Stöd för flera bilder per objekt.
- Huvudbild / frontbild-logik.
- Filtrering på kategori, status och år.
- Plattform- och eraval.

---

## [1.0.0] – 2025

### Added
- Första publika versionen av Adams retrosamling.
- Grundläggande CRUD för prylar.
- Lokal JSON som databas.
- Bilduppladdning via PHP.
