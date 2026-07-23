# Release Notes 4.0 (Deutsch)

> Hauptversion · Änderungen seit Version **3.0.2**
> **Hinweis:** Diese Release Notes decken den aktuellen Vorschau-Stand ab und wurden bisher bis einschließlich **4.0.0-preview.6** generiert. Sie werden mit den weiteren Preview-/RC-Ständen bis zur finalen 4.0.0 fortgeschrieben.

4.0 ist eine **große Hauptversion**. Kern ist eine **komplett neu entwickelte Terminplanung** im Stil von Microsoft Project, dazu eine durchgängig modernisierte Oberfläche, neue Web-Module (Auswertungen, Kapazität, Zusammenarbeit), ein neues **Administrationsportal** und ein neues Installations-/Rollout-Verfahren.

---

## ⭐ Highlights auf einen Blick

| | Highlight |
|---|---|
| 1 | **Neue Terminplanung** mit echter Vorgänger-/Nachfolger-Berechnung und MS-Project-Einschränkungen |
| 2 | **Projektkalender mit Arbeitszeiten** (Arbeitstage, Zeitfenster, Feiertage, ERP-Sync) |
| 3 | **Modernisierte Oberfläche** inkl. Dark Mode und durchgängiger Sprache (DE/EN) |
| 4 | **ERP-Integration** direkt in der Gantt (Bezüge, Stücklisten, Sync-Status) |
| 5 | **Neue Web-Auswertungen** mit Dashboards, Filter-Assistent und PDF-Export |
| 6 | **Angebote und Angebotspositionen** als Terminplanbezüge in einen Plan einfügen |
| 7 | **Neuer Installationsmechanismus über ReadyStackGo** (geführter, zentraler Rollout) |
| 8 | **Neues Administrationsportal** (Web) für Konfiguration, Benutzerrechte, Wartungsmodus, Fehler-Warteschlange und Client-Verteilung |

---

## Neue Terminplanung (MS-Project-orientiert)

Die Terminberechnung wurde von Grund auf neu gebaut (Critical-Path-Method, Vorwärts-/Rückwärtsrechnung):

- **Vorgänger-/Nachfolger-Beziehungen** in allen vier Typen: **Ende–Anfang (FS)**, **Anfang–Anfang (SS)**, **Ende–Ende (FF)**, **Anfang–Ende (SF)**, jeweils mit **Zeitabstand (Lag/Lead)**. Verschiebt sich ein Vorgang, ziehen abhängige Vorgänge automatisch korrekt nach.
- **Einschränkungen wie in MS Project**: „So früh wie möglich" (ASAP), „So spät wie möglich" (ALAP), „Frühestens/Spätestens anfangen am" (SNET/SNLT), „Frühestens/Spätestens enden am" (FNET/FNLT), „Muss anfangen/enden am" (MSO/MFO).
- **Konflikte werden ehrlich angezeigt** statt stillschweigend „geglättet": wenn ein Termin nicht einhaltbar ist, entsteht – wie in MS Project – **negativer Puffer** mit Warnhinweis (Indikator-Spalte in der Gantt), statt die Vorgaben unbemerkt zu verbiegen.
- **Sammelvorgänge (Summary Tasks)** fassen ihre Unteraufgaben korrekt zusammen: Start/Ende/Dauer werden automatisch hochgerollt; gerichtete Einschränkungen am Sammelvorgang wirken als Schranke für die Kinder.
- **Automatisch oder manuell** terminierte Vorgänge: manuell gepinnte Vorgänge behalten ihre Datümer, nehmen aber weiterhin an der Konfliktprüfung teil.
- **Meilensteine** mit korrektem Zeitbezug und sauberem Verhalten an arbeitsfreien Tagen.
- **Neue Warn- und Meldungs-Spalte (Indikatoren)** in der Gantt: eine eigene Spalte zeigt pro Vorgang auf einen Blick alle Hinweise – Termin-Warnungen (nicht einhaltbare Einschränkungen, negativer Puffer, Vorgänger-/Nachfolger-Konflikte, auf Arbeitstage verschobene Termine) ebenso wie ERP-Sync-Hinweise (Termin-Abweichung bzw. -Überschreitung). Jedes Symbol hat einen erklärenden Tooltip, sodass sich Probleme sofort erkennen und beheben lassen.

> 📝 **Hinweis**: Da 4.0 eine neue Terminplanungs-Engine einführt, werden bestehende Projekte beim Upgrade auf die neue Engine umgestellt.

## Projektkalender mit Arbeitszeiten

- Echte **Arbeitstage und Arbeitszeitfenster** (z. B. Mo–Fr 08:00–17:00, mehrere Fenster pro Tag für Mittagspausen) statt reiner Kalendertage.
- **Ausnahmen/Feiertage** auf einer eigenen Unterseite je Kalender; sie gelten bei der Terminplanung als arbeitsfrei.
- **ERP-synchronisierte Kalender** sind in der Oberfläche schreibgeschützt (Quelle ist das ERP) und klar gekennzeichnet.
- **Standard-/Pflichtkalender**: jedes Projekt bekommt einen Kalender; ohne explizite Zuweisung greift ein Standardkalender.
- Zuweisung pro Projekt unter **Einstellungen → Kalender**.
- Detaillierte Schritt-für-Schritt-Anleitung: siehe [Kalender-Guide](../Guides/features/kalender.md).

## Projektliste & Archivierung

- **Neue Terminplan-Auswahlseite**: zentrale Einstiegsseite, auf der Terminpläne ausgewählt und geöffnet werden – wahlweise als **Kartenansicht** oder als **sortierbare Tabellenansicht** (umschaltbar, die Wahl wird gespeichert).
- **Suche und Filter** über Projektname, Manager, Sachbearbeiter, Geschäftsbereich und Revision sowie **Status-Tabs** (Alle / Aktiv / Archiviert) mit Anzahl-Anzeige.
- **Projekt archivieren**: Terminpläne lassen sich direkt aus der Projektliste archivieren. Archivierte Projekte erscheinen im Tab „Archiviert" und werden schreibgeschützt geführt. Die Archivierung läuft asynchron mit Fortschrittsanzeige in Echtzeit.

## Projekt aus Auftrag/Angebot anlegen

- **Neues Projekt direkt aus einem Auftrag oder Angebot** erzeugen: der Anlegen-Dialog ist jetzt web-basiert und übernimmt die ERP-Daten (z. B. Auftrags-/Angebotsnummer, Termin, Geschäftsbereich) als Vorbelegung; das angelegte Projekt bleibt mit dem ERP-Beleg verknüpft.

## Angebote & Aufträge in den Terminplan einfügen

- **Angebote und Angebotspositionen** lassen sich über den Dialog **„Terminplanbezüge"** direkt in einen bestehenden Plan einfügen (**„Angebote zuordnen"**) – wahlweise das Angebot als Ganzes oder gezielt einzelne Positionen.
- Die eingefügten Bezüge erscheinen als **ERP-Vorgänge in der Gantt** (Belegnummer, Typ-Symbol, Beschreibung) und bleiben **live mit ams.erp synchronisiert**.
- Ebenso lassen sich **Aufträge und Auftragspositionen** zuordnen; bestehende Bezüge können einzeln oder gesammelt wieder entfernt werden.

## ERP-Integration

- **ERP-Bezüge und -Termine** direkt in der Gantt sichtbar: Beschriftung, Typ-Symbole und Tooltips, auch für live angelegte ERP-Vorgänge.
- **Stücklisten-Synchronisation** mit korrekter Dauer (aus der Arbeitstage-Spanne, nicht mehr fix „1 Tag") und ohne fälschliches Meilenstein-Verhalten.
- **Sync-Status pro Aufgabe** („in Sync / nicht in Sync") und Schaltfläche **„ERP neu synchronisieren"**.
- Robustere ERP-Datum-Verteilung (zentraler Datum-Hub je Projekt).

## Aufgaben-Detailansicht (modernisiert)

- Der Detailbereich einer Aufgabe ist neu und web-basiert, eingebettet im Desktop-Client (WebView2).
- Reiter für **Vorgänger**, **Diskussion**, **Notizen (Memo)** und **Stückliste (BOM)**.
- Einschränkungen/Termine einer Aufgabe werden hier gepflegt, konsistent mit der neuen Terminplanung.
- Die Detailansicht lässt sich als **eigenes Fenster ablösen**, das zuverlässig im Vordergrund bleibt.
- Ein hängengebliebener oder ausgeblendeter Detailbereich lässt sich jederzeit über **„Detailbereich zurücksetzen"** wiederherstellen; der Konflikte-Bereich ist jetzt scrollbar.

## Auswertungen & Kapazität

- Neue **Web-Auswertungen** mit **Dashboards** und einem **Filter-Assistenten** (Konfiguration ohne SQL-Kenntnisse).
- **Interaktive Diagramme**: Hot-Edit, Drill-down, Hyperlinks, Drucken und **PDF-Export** direkt aus der Analyse-Seite.
- **Erweiterter PDF-Export** der Auswertungen: einstellbare Ränder, Seitenzahlen, „an Breite anpassen" sowie optionale Aufteilung großer Diagramme auf mehrere Seiten (N × M).
- **Kapazitätsauswertung** mit klareren Diagrammen: einstellbare Diagrammgröße und Spaltenanzahl, Auswahllisten für Auswertungsart/Gruppierung, Verfügbar- und Kapazitätsfaktor-Linien sowie deutlich hervorgehobene Überlast-Hinweise.
- **Kapazitätsplanung** mit neuen Web-Buchungsdialogen (Iststunden, Fertigstellungsgrad, Fertigungskennung).

## Zusammenarbeit

- **Diskussionen** je Aufgabe in Echtzeit.
- **Notizen (Memos)** je Aufgabe; beim Kopieren von Aufgaben optional mit übernehmbar.
- Die Diskussions- und Notiz-Bereiche nutzen jetzt das **einheitliche Design-System (ConsistentUI)** und fügen sich in Look-and-Feel und Dark Mode nahtlos ein.

## Kopieren & Einfügen

- Vorgänge inkl. **Unteraufgaben** kopieren – wahlweise **nur die Unteraufgaben** ohne den Kopf-Vorgang.
- **Notizen** beim Kopieren optional mitkopieren.

## Oberfläche, Sprache & Bedienung

- **Durchgängige Sprache (Deutsch/Englisch)**: alle Module folgen der gewählten Sprache; **Sprachumschalter** im Desktop-Client (gespeichert, jederzeit änderbar). Keine gemischt-sprachige Oberfläche mehr.
- Modernisierte **Shell**: neue Titelleiste, Fluent-Farbpalette, **Dark Mode**.
- **Dark Mode weiter ausgebaut**: die Umschaltung wirkt jetzt auch in den eingebetteten Web-Modulen und im WPF-Menü und schaltet live um. Der Dark Mode ist noch **nicht vollständig** – u. a. das Gantt-Diagramm und einzelne WPF-Dialoge folgen in den nächsten Vorschau-Ständen.
- Web-Module werden nahtlos im Desktop-Client gehostet.
- **Mehrprojekt-Zeitachse**: ein **Bearbeitungsmodus (F2)** verhindert versehentliches Verschieben von Terminen. Zusätzlich wurde ein **Fehler beim Verschieben per Maus behoben** – Termine springen jetzt exakt an die Zielposition (und rasten sauber ein), statt durch aufsummierte Maus-Bewegungen zu verrutschen.
- Einheitliche **Wochenend-/Feiertags-Schattierung** in der Gantt.
- Neues, integriertes **Kundendoku-Portal** (Hilfe).

## Administrationsportal (neu) *(für Administratoren)*

Neben der Anwendung selbst gibt es jetzt ein eigenes, web-basiertes **Administrationsportal** mit moderner Oberfläche (Seitenleiste, Dark Mode, Deutsch/Englisch, An-/Abmeldung mit Anzeige des angemeldeten Benutzers):

- **Zentrale Konfiguration**: systemweite Einstellungen werden zentral gepflegt und über einen **Freigabe-Schalter** aktiv geschaltet; Clients laden ihre Einstellungen beim Start automatisch vom Server – manuelle Verteilung von Konfigurationsdateien entfällt.
- **Benutzer-/Administratorrechte**: Administratoren werden im Portal verwaltet; der erste Anmeldende kann automatisch als Administrator freigeschaltet werden (inkl. Wiederherstellungs-Zugang nach Neuinstallation oder Übergabe).
- **Funktionsschalter (Feature-Flags)** und **Änderungsprotokoll (Audit-Log)** direkt im Portal.
- **Wartungsmodus**: das System lässt sich – mit Ankündigung und Countdown-Schonfrist – in einen Wartungsmodus versetzen; angemeldete Clients werden rechtzeitig gewarnt.
- **Fehler-/Warteschlangen-Verwaltung**: fehlgeschlagene Hintergrund-Vorgänge werden übersichtlich angezeigt und lassen sich gezielt **erneut ausführen oder verwerfen**.
- **Mandant.ini-Import**: bestehende Mandanteneinstellungen lassen sich per Dialog einlesen und übernehmen.
- **Client-Verteilung aus dem Portal**: der Desktop-Client kann direkt aus dem Portal an einen Netzwerkpfad verteilt werden – mit **Live-Fortschrittsanzeige**.

## Installation & Betrieb *(für Administratoren)*

- **Neuer Installationsmechanismus über ReadyStackGo (RSGO)**: Die gesamte Anwendung wird zentral und geführt ausgerollt – die einzelnen Dienste/Container werden anhand eines Manifests installiert und aktualisiert, ohne dass jeder Bestandteil manuell eingerichtet werden muss.
- **Ein RSGO für mehrere Zielserver**: dieselbe ReadyStackGo-Instanz kann mehrere Umgebungen/Zielserver bedienen (Remote-Umgebungen).
- **Geführter Client-Installer**: richtet den Desktop-Client beim Kunden ein (Versionsauswahl, Mandantennummer, Zielverzeichnis). Die passende Version wird **bedarfsgesteuert vom Server geladen**; die Mandantennummer kann zentral aus der Konfiguration vorbelegt werden, ein dauerhafter Hintergrunddienst ist nicht mehr nötig.

## Stabilität, Verbesserungen & Fehlerbehebungen im Detail

Neben den großen Neuerungen sind in 4.0 zahlreiche Verfeinerungen und Fehlerbehebungen eingeflossen:

**Öffnen & Sitzung**
- Projekte lassen sich auch nach längerer Inaktivität zuverlässig öffnen – die Sitzung wird automatisch erneuert, statt mit einem plötzlichen Abmelde-Fehler abzubrechen.
- Terminpläne öffnen auch in verteilten Installationen zuverlässig (eine intern fehlende Verbindungsangabe wird jetzt vollständig aufgelöst).

**Terminplanung**
- Datumsgebundene Meilensteine (frühestens/spätestens anfangen bzw. enden am) behalten an arbeitsfreien Tagen ihren Tag bzw. rücken korrekt auf den nächsten Arbeitstag.
- „So spät wie möglich" (ALAP) berücksichtigt jetzt den frühesten machbaren Starttermin und hält die Vorgänger-/Nachfolger-Reihenfolge ein.
- Sammelvorgänge erzeugen keine falschen „auf Arbeitstag verschoben"-Hinweise mehr.
- Vorgänger-/Nachfolger-Beziehungen werden zuverlässig in der Übersicht angezeigt.
- Nicht einhaltbare Termine werden konsequent als negativer Puffer mit Warnung dargestellt (MS-Project-konform).

**ERP-Integration**
- Korrekte Beschriftung und Typ-Symbole auch für live angelegte ERP-Vorgänge.
- Kein Datumsversatz (−1 Tag) mehr bei ERP-Plan-Terminen.
- Stücklisten-Synchronisation mit korrekter Dauer und ohne fälschliches Meilenstein-Verhalten.
- Geerbte Auftragsbezüge tragen keinen falschen ERP-Termin mehr.
- Behobener Anzeige-Absturz bei bestimmten live angelegten ERP-Vorgängen.

**Auswertungen & Kapazität**
- Robusterer PDF-Export: der Export-Dialog schließt nicht mehr versehentlich, funktioniert auch im Kiosk-Modus und exportiert alle Diagramme.
- Korrektes deutsches Datumsformat in den Export-Spalten.
- Überlast-Hinweise werden auch bei 0 Stunden korrekt angezeigt; stabile, einheitliche Label-Farben über alle Kapazitäts-Diagramme.

**Administrationsportal**
- Sprachumschaltung (DE/EN) greift zuverlässig; Abmelde-Knopf und Anzeige des tatsächlich angemeldeten Benutzers.
- Symbole und Formulare werden korrekt dargestellt; Navigation im Dark Mode gut lesbar.
- Speichern der Konfiguration behoben.

**Oberfläche & Desktop**
- WPF-Menü folgt dem Dark Mode (neutrales Grau statt AMS-Blau).
- Detailfenster bleibt zuverlässig im Vordergrund; ein hängengebliebener Detailbereich lässt sich über „Detailbereich zurücksetzen" wiederherstellen.
- Formularfelder verlieren keine Werte mehr, wenn sie erst durch eine Bedingung eingeblendet werden.
- Beim Verlassen eines Plans werden der aktive Plan und seine Menüs sauber geschlossen.
- Kopieren/Einfügen von Notizen: behobener Absturz beim Einfügen.
- Notizen: Wird eine Notiz geleert, verschwindet das Notiz-Symbol in der Tabelle.
- Stücklisten-Liste sortiert die Vorgangs-ID jetzt numerisch statt alphanumerisch.

**Installation**
- Zahlreiche Robustheits-Verbesserungen am Client-Installer (bedarfsgesteuerter Download, Vorbelegung von Zielverzeichnis und Mandantennummer, korrekte Behandlung von UNC-Pfaden und Platzhaltern).

**Weitere Fehlerbehebungen (Vorschau-Stände preview.3 – preview.6)**
- **Anmeldung/Sitzung:** Nach längerer Inaktivität erscheint statt einer technischen Fehlermeldung („Correlation failed" / Fehler 500) eine verständliche Seite **„Sitzung abgelaufen"** mit erneuter Anmeldung; die Neu-Anmeldung läuft ohne Weiterleitungs-Schleife.
- **Terminplan (Gantt):** Das **Ändern der Dauer per Ziehen** berücksichtigt jetzt den **Kalender** (Wochenenden/Feiertage); die im Tooltip angezeigte Dauer entspricht der gespeicherten (Ein-Tag-Versatz behoben).
- **Abgekoppeltes Detailfenster:** ist wieder voll bedienbar (Klicks und Eingaben) und trägt den deutschen Titel **„Task-Details"**.
- **Desktop-Start:** Das Windows-**Taskleisten-Symbol** wird wieder angezeigt; die Startmeldung „Konfiguration wird geladen" ist lokalisiert; die Startkonfiguration wird bei einer Zeitüberschreitung automatisch erneut geladen.
- **Druckansicht** (Auswertungen) öffnet im App-Fenster mit korrekter Projekt-Zuordnung.
- **Betrieb:** Plattform-Dienst und Installer starten auch bei bestimmten Log-Level-Einstellungen stabil (kein Absturz mehr).

## Geändert / Entfernt

- Das Feld **„Typkurve"** in den Dialogen **„Ressource zuweisen"** und **„Sollwert ändern"** entfällt. Es wird im neuen Web-Workflow nicht mehr benötigt; der hinterlegte Typkurven-Wert eines Vorgangs bleibt erhalten und wird weiterhin verarbeitet.
