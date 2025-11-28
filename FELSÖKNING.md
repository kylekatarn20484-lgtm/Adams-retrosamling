# Felsökning: inget sparas till `data.json`

Detta dokument beskriver hur man felsöker problemet där **Adams retrosamling** fungerar i webbläsaren, men ingen data faktiskt sparas.

Typiska symtom:

✅ Du kan lägga till prylar / spel / datorer  
✅ Bilder laddas upp till `uploads/`  
❌ Efter sidladdning är allt borta  
❌ `data.json` ändras aldrig  

Detta beror nästan alltid på server- eller rättighetsproblem, inte på frontend-koden.

## Steg 1 – Kontrollera om `api.php` körs

1. Öppna webbläsarens utvecklarverktyg (F12).
2. Gå till fliken **Network**.
3. Lägg till en pryl.

Du ska se ett nätverksanrop till:

- `api.php`
- Metod: `POST`
- Status: `200`

Om du istället ser:
- `403`
- `500`
- eller inget anrop alls  
då fungerar inte backend korrekt.

## Steg 2 – Kontrollera filrättigheter

Logga in på servern eller containern:

```bash
ls -l data.json
ls -ld uploads
```

Sätt rättigheter:

chmod 666 data.json
chmod 775 uploads

Testa sedan att lägga till en pryl och spara.

---

## ✅ DEL 4 – Steg 3: Docker och read-only problem

```md
## Steg 3 – Docker + Nginx problem

Ett vanligt problem är read-only mount:

```yaml
volumes:
  - ./deploy:/var/www/html:ro
```

Detta ovan gör att data.json inte går att skriva till.

Lösning:

Ta bort :ro:

volumes:
  - ./deploy:/var/www/html

Eller separera data:

volumes:
  - ./deploy:/var/www/html:ro
  - ./data:/var/www/html/data

Och ändra i api.php:

$DATA_FILE = __DIR__ . '/data/data.json';

---

## ✅ DEL 5 – Steg 4: Sökväg till data.json

```md
## Steg 4 – Kontrollera sökvägen till `data.json`

I `api.php` ska det finnas:

```php
$DATA_FILE = __DIR__ . '/data.json';
```
Om filen ligger i undermapp:
$DATA_FILE = __DIR__ . '/data/data.json';

---

## ✅ DEL 6 – Steg 5: Test för skrivrättighet

```md
## Steg 5 – Testa om servern kan skriva

Skapa filen `write-test.php`:

```php
<?php
$file = __DIR__ . '/data.json';

file_put_contents(
  $file,
  json_encode(['test'=>time()]) . "\n",
  FILE_APPEND
);
echo "Test klart";
```

Besök: 
https://din-domän.se/write-test.php

---

## ✅ DEL 7 – Steg 6: Kontrollera API-URL i App.tsx

```md
## Steg 6 – Kontrollera API-URL

I `App.tsx` ska det stå:

```ts
const API_URL = "/api.php";
const UPLOAD_URL = "/upload.php";
```

Använd alltid relativa URL:er om frontend och backend ligger i samma mapp.

---

## ✅ DEL 8 – Debug-loggning

```md
## Steg 7 – Aktivera debug-logg i PHP

Lägg högst upp i `api.php`:

```php
$LOG_FILE = __DIR__ . '/api-debug.log';

function debug_log($msg) {
  global $LOG_FILE;
  file_put_contents($LOG_FILE, date('c') . " " . $msg . "\n", FILE_APPEND);
}

```
Lägg innan skrivning:
debug_log("Försöker skriva till data.json");

---

## ✅ DEL 9 – Checklista

```md
## Checklista

- [ ] POST-anrop till api.php syns
- [ ] Statuskod 200
- [ ] data.json är skrivbar
- [ ] Docker-volym inte read-only
- [ ] write-test.php fungerar
- [ ] api-debug.log skapas





