# IHK Thüringen CRM & BI Demo
## Datenherkunft und Erzeugungslogik

Stand: 06.10.2026

## 1. Ziel des Projekts

Dieses Demonstrationsprojekt bildet einen beispielhaften Datenmanagement-, CRM- und BI-Prozess für ein IHK-ähnliches Umfeld ab. Es ist keine Kopie von EVA und verwendet keine internen Daten der IHK Erfurt.

Öffentlich verfügbare statistische Daten des Thüringer Landesamtes für Statistik bilden die reale fachliche Grundlage. Nicht öffentlich verfügbare CRM-Informationen werden synthetisch erzeugt.

## 2. Grundprinzip

Es gibt drei Datenarten:

1. REALE ÖFFENTLICHE DATEN
   - Statistische Daten des Thüringer Landesamtes für Statistik.
   - Werte werden als fachliche Referenz verwendet.

2. SYNTHETISCHE CRM-DATEN MIT REALER VERTEILUNG
   - Keine echten personenbezogenen CRM-Daten.
   - Kreis, Rechtsform und Unternehmensgröße orientieren sich an realen Thüringer Verteilungen.
   - Weitere CRM-Merkmale werden für Demonstrationszwecke erzeugt.

3. KÜNSTLICH EINGEBAUTE DATENQUALITÄTSPROBLEME
   - Dienen ausschließlich zur Demonstration von Datenprüfung, ETL, Bereinigung und Auditierung.
   - Die Fehlerquoten sind keine Aussage über die Datenqualität einer IHK oder des Thüringer Landesamtes.

## 3. Öffentliche Datenquellen

### A. Gewerbean- und -abmeldungen
Quelle: Thüringer Landesamt für Statistik
Tabelle: KM000482 – Gewerbean- und -abmeldungen nach Wirtschaftsbereichen und Kreisen
Referenz: Juli 2026

Verwendung:
- Gewerbeanmeldungen
- Gewerbeabmeldungen
- Saldo = Anmeldungen - Abmeldungen
- regionale Auswertung nach Kreis/kreisfreier Stadt

Beispielwerte Juli 2026:
- Thüringen: 993 Anmeldungen, 813 Abmeldungen, Saldo +180
- Erfurt: 151 Anmeldungen, 103 Abmeldungen, Saldo +48

### B. Neuerrichtungen und Aufgaben nach Rechtsform
Quelle: Thüringer Landesamt für Statistik
Tabelle: KM000414 – Neuerrichtungen und Aufgaben nach Rechtsformen und Kreisen
Referenz: Juli 2026

Verwendung:
- Anzahl der synthetischen CRM-Unternehmensdatensätze
- regionale Verteilung
- Verteilung der Rechtsformen

Für Version 1 wurden 843 CRM-Basisdatensätze erzeugt, weil für Thüringen im Referenzmonat 843 Neuerrichtungen ausgewiesen wurden.

Wichtig:
Gewerbeanmeldung und Neuerrichtung sind unterschiedliche statistische Konzepte und werden im Modell nicht gleichgesetzt.

### C. Unternehmensgröße
Quelle: Thüringer Landesamt für Statistik
Tabelle: LD000463 – Niederlassungen nach Beschäftigtengrößenklassen und Wirtschaftsabschnitten
Referenz: 2024

Thüringen gesamt: 83.864 Niederlassungen

Verteilung:
- 0–9 Beschäftigte: 69.657 = ca. 83,1 %
- 10–49 Beschäftigte: 11.208 = ca. 13,4 %
- 50–249 Beschäftigte: 2.599 = ca. 3,1 %
- 250+ Beschäftigte: 400 = ca. 0,5 %

Verwendung:
Die Größenklasse der synthetischen CRM-Unternehmen wird anhand dieser realen Verteilung erzeugt. Wo ausreichend Detaildaten vorliegen, soll die Logik in späteren Versionen zusätzlich nach Wirtschaftszweig differenziert werden.

### D. Wirtschaftsbereiche / Branchen
Quelle: Thüringer Landesamt für Statistik
Tabelle: KM000480 – Gewerbeanmeldungen nach Wirtschaftsabschnitten und Kreisen
Referenz: verfügbare Monatsdaten 2026

Verwendung:
- Dimension Branche/Wirtschaftsabschnitt
- fachliche Grundlage für die Verteilung synthetischer Branchen
- spätere Verfeinerung auf Kreis × Branche

## 4. Synthetische CRM-Daten

Die CRM-Daten enthalten keine realen Ansprechpartner oder personenbezogenen Daten.

Synthetisch erzeugte Felder können unter anderem sein:
- CRM_ID
- Kontaktkanal
- Anliegen/Kategorie
- Bearbeitungsstatus
- Bearbeitungsdauer
- KI-Kategorie
- KI-Confidence

Realitätsgebundene synthetische Merkmale:
- Kreis: orientiert an realen Thüringer Regionaldaten
- Rechtsform: orientiert an realen Neuerrichtungen nach Rechtsform
- Unternehmensgröße: orientiert an der realen Thüringer Größenverteilung
- Branche: orientiert an den veröffentlichten Wirtschaftsabschnitten; wird in der nächsten Ausbaustufe genauer an Kreis × Branche gekoppelt

## 5. Datenqualitäts-Demonstration

Für Version 1 wurden kontrolliert Fehler in die Rohdaten eingebaut, damit ein echter ETL-/Data-Quality-Prozess demonstriert werden kann.

Basis: 843 CRM-Basisdatensätze

Eingebaute Probleme:
- 42 Standardisierungsfälle = ca. 5,0 % der Basisdatensätze
- 25 fehlende Branchenwerte = ca. 3,0 %
- 12 ungültige Statuswerte = ca. 1,4 %
- 10 Duplikate = ca. 1,2 %

Hinweis:
Diese Kategorien können sich auf unterschiedliche Qualitätsregeln beziehen. Deshalb werden Prozentwerte nur mit eindeutig definiertem Nenner ausgewiesen und nicht blind addiert.

Ziel des ETL-Prozesses:
- Probleme erkennen
- automatisch korrigierbare Probleme bereinigen
- nicht sicher korrigierbare Fälle zur manuellen Prüfung markieren
- jede Änderung im Change Log dokumentieren

## 6. Audit / Nachvollziehbarkeit

Jede Datenkorrektur soll nachvollziehbar bleiben. Der Data-Quality-Change-Log enthält dafür unter anderem:
- Datensatz-ID
- betroffenes Feld
- alter Wert
- neuer Wert
- Fehlertyp
- Aktion
- Run-ID / Zeitpunkt

Dadurch kann im Dashboard nicht nur die Datenqualität angezeigt werden, sondern auch:
- wie viele Probleme erkannt wurden
- wie viele automatisch korrigiert wurden
- wie viele manuell geprüft werden müssen
- welche Arten von Problemen aufgetreten sind
- wie sich die Datenqualität vor und nach ETL verändert hat

## 7. Geplante BI-Struktur

Power-BI-Seiten:
1. Management Overview
2. Wirtschaftsstruktur
3. Datenqualität & ETL
4. CRM & Services
5. KI-Analyse

Grundregel für KPI-Anzeigen:
- Anzahl und Prozent gemeinsam, wenn ein fachlich sinnvoller Nenner existiert.
- Keine künstlichen oder bedeutungslosen Prozentwerte.
- Zeitvergleiche nur bei tatsächlich vergleichbaren Perioden.

## 8. Transparenzhinweis für Präsentation

Empfohlener Hinweis im Dashboard:

"Öffentliche Wirtschaftsdaten: Thüringer Landesamt für Statistik. CRM-Daten: synthetische Demonstrationsdaten, deren regionale und strukturelle Verteilungen sich an veröffentlichten Thüringer Statistiken orientieren. Keine personenbezogenen Daten und keine internen Daten der IHK Erfurt."

## 9. Versionshinweis

Version 1 ist der erste Datenprototyp. Vor dem finalen Power-BI-Dashboard werden insbesondere die Branchenverteilungen weiter auf reale Kreis-×-Branche-Verteilungen abgestimmt und die ETL-/Audit-Kennzahlen final aus den tatsächlich verarbeiteten Datensätzen berechnet.


## Ergänzung v2 (2026-10-08)
Die SQLite-Datenbank wurde aus den vorhandenen CSV-Dateien neu aufgebaut und mit PRAGMA integrity_check geprüft. Die 42 Standardisierungsereignisse werden als automatisch klassifiziert; andere Fehlerklassen gelten bis zur Verifikation als manuell zu prüfen. `fact_crm_clean` ist eine synthetische Soll-/Zielversion und darf nicht als Beweis für eine erfolgreiche automatische Behebung aller Fehler dargestellt werden. `dq_kpi.csv` dokumentiert die Bezugsbasis für Prozentsätze. Die öffentlichen aggregierten Daten wurden hier nicht erneut gegen das Landesamt validiert.
