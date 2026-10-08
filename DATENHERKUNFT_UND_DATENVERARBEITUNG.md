# IHK Thüringen – CRM- & BI-Web-Dashboard (Demoprojekt)

## Datenherkunft und Datenverarbeitung

**Stand:** 08.10.2026  
**Anwendung:** Interaktives Web-Dashboard auf Basis von HTML, CSS und JavaScript  
**Hinweis:** Eigenständiges Demonstrationsprojekt; keine offizielle Anwendung der IHK Erfurt.

## 1. Ziel des Projekts

Dieses Demonstrationsprojekt zeigt, wie öffentlich verfügbare Wirtschaftsdaten und synthetische CRM-Datensätze für Datenanalyse, Datenqualitätskontrolle und interaktive Berichte in einem IHK-ähnlichen Umfeld genutzt werden können. Es bildet weder das interne CRM-System EVA nach noch verwendet es interne Daten der IHK Erfurt.

Das veröffentlichte Dashboard ist eine eigenständige Webanwendung. **Power BI ist für die Nutzung nicht erforderlich.** Die Darstellung und Interaktion erfolgen im Browser; die hier beschriebenen Vorbereitungs- und Qualitätsprozesse sind davon zu unterscheiden.

## 2. Grundprinzip und Kennzeichnung

Es werden drei Datenarten unterschieden:

1. **Öffentliche amtliche Statistiken:** Veröffentlichte aggregierte Werte des Thüringer Landesamtes für Statistik dienen als fachliche Referenz.
2. **Synthetische CRM-Daten:** Es werden keine realen personenbezogenen CRM-Daten verwendet. Regionale und strukturelle Merkmale orientieren sich an veröffentlichten Verteilungen; weitere CRM-Felder sind für die Demonstration erzeugt.
3. **Gezielt eingebaute Datenqualitätsprobleme:** Diese illustrieren Prüf-, Bereinigungs- und Audit-Konzepte. Die Fehlerquoten sind **keine Aussage** über die Datenqualität der IHK oder der amtlichen Statistik.

## 3. Öffentliche Datenquellen

### A. Gewerbean- und -abmeldungen

- **Quelle:** Thüringer Landesamt für Statistik, Tabelle **KM000482** – Gewerbean- und -abmeldungen nach Wirtschaftsbereichen und Kreisen
- **Referenzzeitraum:** Juli 2026
- **Verwendung:** Anmeldungen, Abmeldungen, Saldo und regionale Vergleiche

Im zugrunde liegenden Datenstand genannte Beispielwerte:

| Region | Anmeldungen | Abmeldungen | Saldo |
|---|---:|---:|---:|
| Thüringen | 993 | 813 | +180 |
| Erfurt | 151 | 103 | +48 |

**Hinweis:** Die angegebenen amtlichen Aggregatwerte wurden im Rahmen der Ergänzung vom 08.10.2026 nicht erneut mit dem Landesamt abgeglichen.

### B. Neuerrichtungen und Aufgaben nach Rechtsform

- **Quelle:** Thüringer Landesamt für Statistik, Tabelle **KM000414** – Neuerrichtungen und Aufgaben nach Rechtsformen und Kreisen
- **Referenzzeitraum:** Juli 2026
- **Verwendung:** Orientierung für die Anzahl, regionale Verteilung und Rechtsformen synthetischer CRM-Unternehmensdatensätze

Für den ursprünglichen Datenprototyp wurden **843 CRM-Basisdatensätze** erzeugt, angelehnt an 843 ausgewiesene Neuerrichtungen im Referenzmonat. **Gewerbeanmeldung und Neuerrichtung sind unterschiedliche statistische Konzepte** und werden nicht gleichgesetzt.

### C. Unternehmensgröße

- **Quelle:** Thüringer Landesamt für Statistik, Tabelle **LD000463** – Niederlassungen nach Beschäftigtengrößenklassen und Wirtschaftsabschnitten
- **Referenzjahr:** 2024
- **Thüringen insgesamt:** 83.864 Niederlassungen

| Beschäftigte | Niederlassungen | Anteil (gerundet) |
|---|---:|---:|
| 0–9 | 69.657 | 83,1 % |
| 10–49 | 11.208 | 13,4 % |
| 50–249 | 2.599 | 3,1 % |
| 250+ | 400 | 0,5 % |

Diese Verteilung dient als Orientierung für die synthetische Größenklasse. Eine feinere Differenzierung nach Wirtschaftszweig wäre eine mögliche Weiterentwicklung.

### D. Wirtschaftsbereiche / Branchen

- **Quelle:** Thüringer Landesamt für Statistik, Tabelle **KM000480** – Gewerbeanmeldungen nach Wirtschaftsabschnitten und Kreisen
- **Referenz:** Verfügbare Monatsdaten 2026
- **Verwendung:** Branchenklassifikation und Orientierung für die synthetische Branchenverteilung

Eine genauere Verteilung nach **Kreis × Branche** ist als mögliche Erweiterung vorgesehen; sie wird hier nicht als bereits umgesetzt behauptet.

## 4. Synthetische CRM-Daten

Die CRM-Daten enthalten keine realen Ansprechpartner oder personenbezogenen IHK-Daten. Beispielhafte Felder sind:

- CRM-ID
- Kontaktkanal
- Anliegen / Kategorie
- Bearbeitungsstatus
- Bearbeitungsdauer (Tage)
- KI-Kategorie und KI-Confidence

Kreis, Rechtsform, Unternehmensgröße und Branche sind synthetische Merkmale, die sich teilweise an veröffentlichten Thüringer Verteilungen orientieren. Die übrigen Merkmale wurden für Demonstrationszwecke erstellt. **Ein KI-bezogenes Datenfeld belegt nicht automatisch den Einsatz eines produktiven KI-Modells.**

## 5. Demonstration von Datenqualität und Bereinigung

Im ursprünglichen Datenprototyp wurden ausgehend von **843 CRM-Basisdatensätzen** kontrolliert folgende Probleme vorgesehen:

| Problemart | Anzahl | Bezogen auf 843 Basisdatensätze |
|---|---:|---:|
| Standardisierungsfälle | 42 | ca. 5,0 % |
| Fehlende Branchenwerte | 25 | ca. 3,0 % |
| Ungültige Statuswerte | 12 | ca. 1,4 % |
| Duplikate | 10 | ca. 1,2 % |

Die Kategorien beschreiben unterschiedliche Prüfregeln. Ihre Prozentwerte dürfen nicht ohne Prüfung der Bezugsgrößen und Überschneidungen zu einer Gesamtfehlerquote addiert werden.

Das demonstrierte Datenqualitätskonzept unterscheidet zwischen Erkennung, regelbasierter Korrektur, manueller Prüfung und Dokumentation. **Die Existenz eines bereinigten Zieldatensatzes allein beweist nicht, dass sämtliche Fehler automatisch behoben wurden.**

## 6. Auditierbarkeit und Nachvollziehbarkeit

Ein Data-Quality-Change-Log kann unter anderem folgende Informationen dokumentieren:

- Datensatz-ID und betroffenes Feld
- Alter und neuer Wert
- Fehlertyp und Aktion
- Run-ID und Zeitpunkt

Damit lassen sich erkannte Probleme, automatische Korrekturen und Fälle für eine manuelle Prüfung nachvollziehbar unterscheiden. Für die Auswertung sind definierte Nenner und ein konsistenter Verarbeitungsstand erforderlich.

## 7. Aufbau und Technik des Web-Dashboards

Die veröffentlichte Demonstration ist als **interaktive Browser-Anwendung** konzipiert. Im Mittelpunkt stehen die Visualisierung und Auswertung von Wirtschafts-, CRM- und Datenqualitätsdaten, beispielsweise:

1. **Management-Überblick:** Kennzahlen und aggregierte Zusammenfassungen
2. **Wirtschaftsstruktur:** Regionale und strukturelle Vergleiche
3. **Datenqualität:** Qualitätskennzahlen und nachvollziehbare Prüfergebnisse
4. **CRM & Services:** Beispielhafte CRM-Datensätze, Status und Bearbeitungsdauer
5. **KI-Potenziale:** Demonstrative Kategorien und mögliche Analyseansätze

**Technische Abgrenzung:** Die Website wird über `index.html` bereitgestellt und nutzt HTML, CSS und JavaScript. Die dargestellten Daten können in die Webdatei eingebettet sein. Das Anzeigen von Daten im Browser ist nicht mit der Ausführung einer SQLite-Datenbank, eines Python-ETL-Prozesses oder einer Power-BI-Lösung im Browser gleichzusetzen.

## 8. Transparenzhinweis

> Öffentliche Wirtschaftsdaten: Thüringer Landesamt für Statistik. CRM-Daten: synthetische Demonstrationsdaten, deren regionale und strukturelle Verteilungen sich an veröffentlichten Thüringer Statistiken orientieren. Keine personenbezogenen Daten und keine internen Daten der IHK Erfurt.

## 9. Datenstand, Grenzen und Weiterentwicklung

Die beschriebenen Mengen und Regeln beziehen sich auf den dokumentierten Datenprototyp. Für eine belastbare Aussage über die **aktuell veröffentlichte Webversion** müssen die Kennzahlen mit den tatsächlich eingebetteten Daten abgeglichen werden.

Nach der Ergänzung vom 08.10.2026 wurde eine SQLite-Datenbank aus vorhandenen CSV-Dateien neu aufgebaut und mit `PRAGMA integrity_check` geprüft. Diese Datenbank ist ein Artefakt der Datenvorbereitung und **keine Laufzeitvoraussetzung des Web-Dashboards**. Die 42 Standardisierungsereignisse wurden als automatisch klassifiziert; andere Fehlerklassen gelten bis zur Verifikation als manuell zu prüfen. `fact_crm_clean` bezeichnet eine synthetische Soll-/Zielversion und ist kein Nachweis einer vollständig automatisierten Bereinigung. `dq_kpi.csv` dokumentiert die Bezugsbasis für Prozentangaben.

Mögliche nächste Schritte sind die genauere Abbildung von Kreis-×-Branche-Verteilungen, ein Abgleich der dokumentierten Kennzahlen mit der veröffentlichten Webversion sowie die weitere Präzisierung der Audit- und Qualitätskennzahlen.
