# Seřazení fotek — stažení pro Windows

Aplikace pro seřazení JPG/JPEG fotografií podle data pořízení a přejmenování na `1.jpg`, `2.jpg`, … Obsah fotografií nemění. Fotografie se nikam nenahrávají.

## Stažení

**[Stáhnout nejnovější EXE](https://github.com/tomasbradac69/serazeni-fotek-download/releases/latest/download/prejmenuj_soubory_datum.exe)**

[Verze a soubory ke stažení](https://github.com/tomasbradac69/serazeni-fotek-download/releases/latest)

Windows x64, bez instalace Pythonu. Program není digitálně podepsaný; Windows může zobrazit bezpečnostní upozornění. Před spuštěním ověřte původ staženého souboru. Tento repozitář slouží jen k distribuci programu a návodu, nikoli zdrojového kódu.

## Použití

1. Nejprve zálohujte fotografie a vyzkoušejte program na jejich kopii na místním disku.
2. Spusťte EXE a vyberte složku. Zavřete editory fotografií a pozastavte synchronizaci složky.
3. Zkontrolujte náhled názvů a výslovně potvrďte změny. Zrušení nic nepřejmenuje.
4. K obnově původních názvů spusťte program znovu a vyberte stejnou složku; nabídne obnovu.

Podporuje `.jpg` a `.jpeg` bez ohledu na velikost písmen. Výstup má příponu `.jpg`. Datum čte přednostně z EXIF `DateTimeOriginal`, jinak z názvu `IMG_YYYYMMDD_HHMMSS`. Fotografie bez zjistitelného data přeskočí. Podadresáře nezpracovává.

## Bezpečnost a obnova

Před změnami kontroluje kolize, přejmenovává přes dočasné názvy a ukládá deník `.serazeni-fotek-journal.json`. **Deník ani dočasné `.stage` / `.restore` soubory nemažte.** Při chybě operaci zastaví; znovuspuštění umožní obnovu. Po úspěšném přejmenování deník zůstává pro návrat; další řazení je do obnovy blokované.

Deník není záloha fotografií. Změna jejich obsahu, kopírování na jiný disk nebo zásah jiného programu může obnovu zablokovat. Testovaný provoz je místní disk na Windows; síťová a cloudová úložiště nejsou ověřena. Nelze garantovat zotavení po výpadku napájení či selhání disku.

## Příkazový řádek

```powershell
.\prejmenuj_soubory_datum.exe --help
.\prejmenuj_soubory_datum.exe "C:\Fotky"              # pouze náhled
.\prejmenuj_soubory_datum.exe "C:\Fotky" --apply      # vyžaduje ANO
.\prejmenuj_soubory_datum.exe "C:\Fotky" --undo       # náhled obnovy
.\prejmenuj_soubory_datum.exe "C:\Fotky" --undo --apply
```

## Ověření vydání

U vydání je soubor `SHA256SUMS.txt`. Ve Windows můžete porovnat otisk EXE příkazem `Get-FileHash .\prejmenuj_soubory_datum.exe -Algorithm SHA256`.
