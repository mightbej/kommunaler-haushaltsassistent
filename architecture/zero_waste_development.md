# Zero-Waste Development (ZWE) – Methodischer Rahmen v1
> **Kurzbeschreibung:**  
> Dieses Dokument beschreibt das Konzept der Zero-Waste-Entwicklung (ZWE) für den Kommunalen Haushaltsassistenten (KHHA).  
> Es dient als methodische Grundlage für die adaptive, LLM-gestützte Tool-Entwicklung im Projekt.

## Inhaltsverzeichnis
- [1. Hintergrund](#1-hintergrund)
- [2. Definition](#2-definition-zero-waste-entwicklung-zwe)
- [3. Grundprinzip](#3-grundprinzip)
- [4. On-Demand-Funktionserzeugung](#4-on-demand-funktionserzeugung)
- [5. Rolle der RAC-Struktur](#5-rolle-der-rac-struktur)
- [6. Zero-Waste und die Tool-Registry](#6-zero-waste-und-die-tool-registry)
- [7. Vorteile](#7-vorteile-des-ansatzes)
- [8. Abgrenzung](#8-abgrenzung-zu-klassischen-verfahren)
- [9. Voraussetzungen und Grenzen](#9-voraussetzungen-und-grenzen)
- [10. Zusammenfassung](#10-zusammenfassung)
- [11. Status](#11-status)

---

## 1. Hintergrund
Klassische Softwareentwicklung arbeitet mit vorab definierten Funktionen, Modulen und strukturierten Datenflüssen. Für eine semantische Aufgabe wie die kommunale Haushaltsanalyse ist das nur begrenzt geeignet:  
Fachlogik ändert sich häufig, Datenquellen unterscheiden sich zwischen Kommunen, und die Art der Fragestellungen ist kaum planbar.

Der Kommunale Haushaltsassistent (KHHA) setzt daher auf eine adaptive und experimentelle Entwicklungslogik, die wir **Zero-Waste Development (ZWE)** nennen.

## 2. Definition: Zero-Waste-Entwicklung (ZWE)
**Zero-Waste-Entwicklung** bezeichnet ein KI-gestütztes, **experimentelles** Softwareentwicklungsverfahren, bei dem Systemfunktionalität nicht im Voraus vollständig entworfen wird. Sie entsteht **schrittweise bedarfsgetrieben** aus der tatsächlichen Nutzung heraus.

Die Architektur stellt nur minimale Grundregeln und ein Such- und Ausführungssystem bereit (z. B. MCP). Ein Planungs-LLM analysiert reale Nutzeranfragen und entscheidet dynamisch, **welche Funktionen fehlen**. Nur diese fehlenden Elemente werden anschließend implementiert.

ZWE ist **klar nutzerzentriert**: Die Entwicklung folgt den tatsächlichen Fragen und Arbeitsmustern der Anwender – nicht hypothetischen Szenarien. Dadurch wächst das System **organisch aus echter Nutzung heraus** und vermeidet unnötige Komponenten, überflüssige Planung und ungenutzten Code.

## 3. Grundprinzip
Zero-Waste Development bedeutet:

- **keine ungenutzten Module**  
- **keine vorab implementierte Fachlogik**  
- **keine Arbeit für hypothetische Funktionen**  
- **Funktionalität nur bei tatsächlichem Bedarf**

## 4. On-Demand-Funktionserzeugung
Die Funktionalität wird **im Moment der Anfrage** dynamisch aufgebaut:

1. Semantische Analyse der Nutzerfrage  
2. Identifikation relevanter Datenquellen und Tools  
3. Zusammenstellung einer passenden Prompt-/Tool-Pipeline  
4. Berechnung und Interpretation des Ergebnisses  
5. Rückbau nicht benötigter Logik

## 5. Rolle der RAC-Struktur
Die RAC-Struktur (**Retrieve – Analyze – Compose**) bildet die operative Logik:

- **Retrieve:** Daten- und Toolauswahl  
- **Analyze:** fachliche Regeln und Berechnungen  
- **Compose:** zielführende Tool- und Prompt-Ketten

## 6. Zero-Waste und die Tool-Registry
Die Tool-Registry dient als deklaratives Inventar. Sie enthält:

- Beschreibungen  
- Inputs  
- Outputs  
- fachliche Erwartungen  

aber **keine implementierte Logik**.  
Alles entsteht nur bei echtem Bedarf.

## 7. Vorteile des Ansatzes

### 7.1 Technische Vorteile
- kleine, fokussierte Codebasis  
- keine toten Module  
- geringer Wartungsaufwand  
- hohe Modularität  

### 7.2 Fachliche Vorteile
- Logik passt exakt zu realen Haushaltsfragen  
- jede Kommune erzeugt ihren eigenen Funktionspfad  
- Gesetzes- und Produktänderungen fließen textuell ein  
- keine Programmierkenntnisse für neue Fachlogik notwendig

## 8. Abgrenzung zu klassischen Verfahren
| Verfahren | Eigenschaften |
|----------|---------------|
| Klassisch | Funktionen vorab entwickelt, oft ungenutzt |
| Zero-Waste | Funktionen entstehen bei Bedarf |
| Klassisch | Logik im Code verankert |
| Zero-Waste | Logik dynamisch erzeugt |
| Klassisch | hoher Refactoringbedarf |
| Zero-Waste | kaum Altlasten |

## 9. Voraussetzungen und Grenzen
ZWE funktioniert, wenn:

- Fachlogik textlich gut ausdrückbar ist  
- Tools deklarativ beschreibbar sind  
- solide Retrieval-/Analysefähigkeiten vorhanden sind  

Deterministische Fachlogik bleibt in klassischen Tools.

## 10. Zusammenfassung
ZWE ist ein experimenteller, nutzerzentrierter Entwicklungsansatz.  
Funktionen entstehen nur on-demand, bleiben temporär und folgen realer Nutzung.

## 11. Status
Version 1.0 – Grundlage für die weitere Ausarbeitung im KHHA-Prototyp.
