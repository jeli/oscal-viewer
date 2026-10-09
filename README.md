# OSCAL-Viewer

**OSCAL-Kataloge offline im Browser ansehen — eine einzige HTML-Datei, keine Installation, keine Netzwerkzugriffe.**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
![Format: eine HTML-Datei](https://img.shields.io/badge/Format-eine%20HTML--Datei-success)
![Betrieb: offline](https://img.shields.io/badge/Betrieb-offline-informational)
![Abhängigkeiten: keine](https://img.shields.io/badge/Abh%C3%A4ngigkeiten-keine-success)

Der Viewer lädt OSCAL-Kataloge im JSON-Format und stellt sie als aufklappbaren Baum dar:
**Praktikenfeld → Praktik → Anforderung** — mit Statement, aufklappbarer Erläuterung und
Klartext-Eigenschaften je Anforderung. Entwickelt und getestet für den
**BSI-Stand-der-Technik-Kernel** (Grundschutz++); jeder OSCAL-Katalog mit der Struktur
`catalog.groups[].groups[].controls[]` funktioniert.

Der Katalog bleibt vollständig lokal: Das Einlesen erfolgt ausschließlich über die
Browser-Datei-API (FileReader) — kein `fetch`, keine externen Ressourcen, keine Übertragung.

## Steckbrief

| Eigenschaft | Wert |
| --- | --- |
| Projekttyp | Single-File-HTML-Anwendung — direkt im Browser lauffähig (auch über `file://`) |
| Version | 1.0 (Stand: 08.10.2026) |
| Lizenz | GNU General Public License v3.0 · SPDX: `GPL-3.0-or-later` |
| Technologie | HTML5, CSS, Vanilla-JavaScript (ES2015) |
| Abhängigkeiten | keine — kein Framework, kein Build-Schritt, keine CDN-Ressourcen |
| Netzwerkzugriffe | keine — Datei-Dialog, FileReader und localStorage, mehr nicht |
| Eingabeformat | OSCAL-Katalog-JSON (`catalog.groups[].groups[].controls[]`) |
| Getesteter Katalog | BSI-Stand-der-Technik-Kernel (Grundschutz++), maschinenlesbar aus der BSI-Bibliothek |
| Oberflächensprache | Deutsch |
| Browser | jeder ES2015-fähige Browser (ab ca. 2015); Vorab-Prüfung über die Browser-Check-Datei |

## Funktionen

- **Katalog laden**: per Datei-Auswahl oder Drag &amp; Drop — auch nachträglich überall auf der Seite
- **Baumdarstellung**: Praktikenfeld → Praktik → Anforderung, alles aufklappbar (`details`/`summary`)
- **Volltextsuche**: über IDs, Titel, Statements und Erläuterungen; mehrere Begriffe werden UND-verknüpft
- **Filter als Mehrfachauswahl-Checkboxen**: Schutzstufe (normal-SdT / erhöht), Verbindlichkeit (MUSS / SOLLTE / KANN), Aufwand (0–5)
- **Klartext-Chips je Anforderung**: Schutzstufe, Aufwand, Verbindlichkeit (MUSS hervorgehoben), Dokumentationsvorgabe, Zielobjektkategorien, Handlungswort, Ergebnisspezifikation
- **Erläuterungen**: die Guidance zu jeder Anforderung als aufklappbares Panel unter dem Statement
- **Live-Zähler**: „X von N Anforderungen sichtbar“ bei jedem Such- und Filterschritt
- **Hell/Dunkel**: automatisch passend zum System, manuell umschaltbar (3 Zustände), Auswahl wird gespeichert
- **Sicherheit**: alle Kataloginhalte werden HTML-maskiert — kein XSS aus Katalogdaten

## Schnellstart

1. `oscal-viewer.html` herunterladen.
2. Datei im Browser öffnen (Doppelklick genügt).
3. Katalog-JSON hineinziehen oder über „Datei auswählen“ laden — fertig.

### Katalog beziehen (BSI-Stand-der-Technik-Kernel)

Der Kernel-Katalog liegt maschinenlesbar in der BSI-Bibliothek auf GitHub:

- Repository: <https://github.com/BSI-Bund/Stand-der-Technik-Bibliothek>
- Direkter Download (JSON): [BSI-Stand-der-Technik-Kernel-catalog.json](https://raw.githubusercontent.com/BSI-Bund/Stand-der-Technik-Bibliothek/main/control_layer/Grundschutz%2B%2B/sources/catalogs/Kernel/BSI-Stand-der-Technik-Kernel-catalog.json)

Hinweis: Kernel-IDs sind zwischen Releases nicht stabil — nach einem Katalog-Update prüfen,
ob sich Anforderungs-IDs verschoben haben.

## Browser-Prüfung

Läuft der Viewer nicht (gesperrtes JavaScript, blockierter Datei-Dialog, alter Browser), vorab
`oscal-viewer-browsercheck.html` öffnen. Die Prüfseite:

- testet automatisch JavaScript-Syntax (ES2015), Datei-API, Drag &amp; Drop, Dialoge und Darstellung,
- enthält einen Live-Test, der exakt den Ladevorgang des Viewers nachbildet
  (Datei-Auswahl → FileReader → JSON.parse → Strukturprüfung),
- erzeugt einen Textbericht zum Zurückmelden (z. B. an die IT).

## Projektdateien

| Datei | Inhalt |
| --- | --- |
| `oscal-viewer.html` | Der Viewer — die einzige Datei, die man braucht |
| `oscal-viewer-browsercheck.html` | Selbsttest für Browser und Umfeld, erzeugt Textbericht |
| `LICENSE` | Volltext der GNU General Public License v3.0 |

## Lizenz

Copyright (C) 2026 Christian

Dieses Programm ist freie Software: Sie können es unter den Bedingungen der GNU General
Public License, wie von der Free Software Foundation veröffentlicht — Version 3 der Lizenz
oder (nach Ihrer Wahl) eine spätere Version — weitergeben und/oder modifizieren.

Dieses Programm wird in der Hoffnung verbreitet, dass es nützlich ist, aber OHNE JEDE
GEWÄHRLEISTUNG — sogar ohne die implizite Gewährleistung der MARKTREIFE oder der
VERWENDBARKEIT FÜR EINEN BESTIMMTEN ZWECK. Details siehe [LICENSE](LICENSE).

Volltext der Lizenz: <https://www.gnu.org/licenses/gpl-3.0.html>