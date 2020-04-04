# coronaDat

In diesem Datenrepo werden automatisiert die vom Österreichischen Gesundheitsministerium unter  [`info.gesundheitsministerium.at`](https://info.gesundheitsministerium.at) bereitgestellten - Covid19 relevanten Daten - gesammelt und archiviert, sodass eine (spätere) Analyse auch im Zeitverlauf möglich ist.

## Updates
### 26.3.2020
An diesem Tag wurde Dashboard verändert. 

- die Anzahl der Hospitalisierungen bzw. Personen, die Intensivbetreuung benötigen  wurde aus dem Dashboard entfernt. Die Zahlen (inkl. Bundesländerauswertung) wird stattdessen täglich unter [diesem Link](https://www.sozialministerium.at/Informationen-zum-Coronavirus/Dashboard/Zahlen-zur-Hospitalisierung) bereitgestellt. Die relevante Tabelle wird seit diesem Zeitpunkt ebenfalls gescrapt

- die Datenaktualisierung ist seit diesem Zeitpunkt nur mehr stündlich (nicht mehr alle 15 Minuten)
- die Bezirksdaten enthalten seit diesem Zeitpunkt nur mehr einen Wert für Wien da einzelnen Wiener Bezirksergebnisse nicht mehr ausgewiesen werden

### 27.3.2020
Die originalen Datensätze (`*.js`) werden in `/archive/{day}/data/{day}_{timestamp}_orig_js.zip` mitgespeichert

### 2.4.2020
Die Anzahl der Sterbefälle und Gesundungen nach Bundesland werden in `/latest/sterbefaelle_bl.{csv|rds|json}` und `/latest/gesundungen_bl.{csv|rds|json}` bzw die Zeitreihen unter `/ts/sterbefaelle_bl.{csv|rds|json}` und `/ts/gesundungen_bl.{csv|rds|json}` abgespeichert.

### 4.4.2020
- Alle `csv` Files werden als *_en.csv* auch mit `,` als Separator abgespeichert, damit die Files in Github besser angezeigt werden ([issue #4](https://github.com/statistikat/coronaDAT/issues/4))

## Datenstruktur
Die Datenstruktur im erzeugten Datenrepository ist wie folgt:

### `/archive`
enthält die gescrapten Daten von [`info.gesundheitsministerium.at`](https://info.gesundheitsministerium.at). Dazu wird für jeden Tag ein Unterordner angelegt. Einzelne Dateien sind für jeden gescrapten Zeitpunkt als 

- `/archive/{day}/data/{day}_{timestamp}.rds` 
- `/archive/{day}/data/{day}_{timestamp}_hospitalisierung.rds` (Daten über Hospitalisierungen/Intensivfälle; seit `26.3.2020`)
- `/archive/{day}/data/{day}_{timestamp}_orig_js.zip` (die unmodifizierten js-datenfiles; seit dem `27.3.2020`)
- `/archive/{day}/data/{day}_{timestamp}_gesundungen_todesfaelle.rds` (Daten über Gesundungen/Todesfälle; seit `2.4.2020`)

im Repo enthalten.

### `/latest`
enthält Files für die einzelnen Auswertungen für den aktuellsten Zeitpunkt in verschiedenen Formaten. Insbesondere:

- `/latest/allgemein.{csv|rds|json}`: bestätigte Fälle, hospitalisierte Personen und Personen auf der Intensivstation (gesamt Österreich)
- `/latest/alter.{csv|rds|json}`: bestätigte Fälle nach Altersgruppen
- `/latest/bezirke.{csv|rds|json}`: bestätigte Fälle nach politischen Bezirken
- `/latest/bundesland.{csv|rds|json}`: bestätigte Fälle nach Bundesland
- `/latest/geschlecht.{csv|rds|json}`: Anteil der bestätigten Fälle nach Geschlecht
- `/latest/hospitalisierungen_bl.{csv|rds|json}`: Anzahl der Hospitalisierungen nach Bundesland (seit `26.3.2020`)
- `/latest/sterbefaelle_bl.{csv|rds|json}`: Anzahl der Sterbefaelle nach Bundesland (seit `2.4.2020`)
- `/latest/gesundungen_bl.{csv|rds|json}`: Anzahl der Gesundungen nach Bundesland (seit `2.4.2020`)

### `/ts`
enthält Zeitreihendaten für die einzelnen Auswertungen in verschiedenen Formaten. Insbesondere:

- `/ts/allgemein.{csv|rds|json}`: bestätigte Fälle, hospitalisierte Personen und Personen auf der Intensivstation
- `/ts/alter.{csv|rds|json}`: bestätigte Fälle nach Altersgruppen
- `/ts/bezirke.{csv|rds|json}`: bestätigte Fälle nach politischen Bezirken
- `/ts/bundesland.{csv|rds|json}`: bestätigte Fälle nach Bundesland
- `/ts/geschlecht.{csv|rds|json}`: Anteil der bestätigten Fälle nach Geschlecht
- `/ts/trend.{csv|rds|json}`: Anzahl der bestätigten Fälle gesamt
- `/ts/hospitalisierungen_bl.{csv|rds|json}`: Anzahl der Hospitalisierungen nach Bundesland (seit `26.3.2020`)
- `/ts/sterbefaelle_bl.{csv|rds|json}`: Anzahl der Sterbefaelle nach Bundesland (seit `2.4.2020`)
- `/ts/gesundungen_bl.{csv|rds|json}`: Anzahl der Gesundungen nach Bundesland (seit `2.4.2020`)

### `/coronadata_ts_latest.{rds|json}`
Diese Files enthalten die gesamte, gescrapte History exclusive Anzahl der Sterbefälle und Hospitalisierungen nach Bundesland.
