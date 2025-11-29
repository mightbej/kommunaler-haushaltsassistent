# # System Design – Kommunaler Haushaltsassistent (KHHA)

## 1. Zielsetzung
Der Kommunale Haushaltsassistent (KHHA) soll kleinen kommunalen Fraktionen ermöglichen, Haushaltspläne effizienter zu analysieren.  
Das System bietet Funktionen zur Strukturierung, Auswertung und Interpretation kommunaler Haushaltsdaten und ist so aufgebaut, dass es für unterschiedliche kommunale Haushaltsdokumente anpassbar bleibt.

## 2. Grundprinzip der Architektur
Die Architektur folgt einem modularen Ansatz.  
Fachliche Analysefunktionen werden als klar definierte, voneinander unabhängige Bausteine („Tools“) umgesetzt.  
Diese Bausteine können je nach Fragestellung einzeln aktiviert, kombiniert oder erweitert werden.

Zentrale Eigenschaften:
- **Modularität:** Jeder Funktionsbaustein erfüllt eine klar abgegrenzte Aufgabe (z. B. Trendanalyse, Budgetvergleich, Produktbereich-Auswertung).
- **Austauschbarkeit:** Bausteine können erweitert oder ersetzt werden, ohne das restliche System zu verändern.
- **Leichtgewichtige Tool-Schicht:** Die Ausführung erfolgt über eine schmale, deklarative Toolschnittstelle (z. B. MCP).

## 3. Komponentenübersicht
Die Architektur umfasst folgende Hauptkomponenten:

### 3.1. Datenaufnahme
- Einlesen von Haushaltsplänen aus PDFs, Tabellen oder strukturierten Exporten
- Vorverarbeitung und Strukturierung (Jahre, Produkte, Konten, Ansätze)

### 3.2. Datenmodell
Ein einfaches, aber erweiterbares Datenmodell bildet die Grundlage:
- **Produkte / Produktbereiche**
- **Kontenrahmen**
- **Jahre**
- **Ansätze, Aufwendungen, Erträge, Auszahlungen**

Das Modell ist bewusst minimal gehalten, um in der ersten Projektphase flexibel zu bleiben.

### 3.3. Analyse-Tools (modulare Funktionsbausteine)
Jede Analysefunktion ist als eigenständiges Tool definiert.

Beispiele:
- Extraktion und Strukturierung von Produktbereichen
- Vergleich Soll/Ist/Ansatz
- Trendberechnung über mehrere Jahre
- Identifikation auffälliger Veränderungen („Signifikanzfilter“)
- Vergleich zwischen Haushaltsjahren

Tools verfügen über:
- klar definierte Inputs  
- klar definierte Outputs  
- eine kurze Beschreibung  
- deklarative Spezifikation  

### 3.4. Dialog- und Auswertungslogik
Ein LLM übernimmt:
- Ansteuerung der Tools (je nach Frage)
- Interpretation von Zwischenergebnissen
- Zusammenstellung einer verständlichen Antwort

Damit können auch komplexe Auswertungen über mehrere Teilfunktionen realisiert werden, ohne dass der Nutzer diese manuell kombinieren muss.

## 4. Arbeitsweise
1. **Frageanalyse:**  
   Eine Nutzerfrage (z. B. „Wie entwickeln sich die Aufwendungen im Produktbereich Schulen seit 2022?“) wird semantisch analysiert.

2. **Toolauswahl:**  
   Das System wählt die passenden Funktionsbausteine aus (z. B. Zeitreihe, Trendanalyse).

3. **Datenverarbeitung:**  
   Die Tools erzeugen strukturierte Zwischenergebnisse (z. B. Listen, Tabellen).

4. **Auswertung:**  
   Die Ergebnisse werden fachlich interpretiert und in natürliche Sprache übersetzt.

Dieses Vorgehen erlaubt eine flexible Nutzung ohne starres Regelwerk.

## 5. Erweiterbarkeit
Das System lässt sich schrittweise erweitern:
- neue Tools können hinzugefügt werden, ohne bestehende zu verändern  
- zusätzliche Haushaltsstrukturen anderer Kommunen können eingebunden werden  
- spätere Module (z. B. Maßnahmenvergleich, Investitionsprogramm) lassen sich problemlos ergänzen  

Die Architektur ist darauf ausgelegt, ein funktionsfähiges MVP schnell bereitzustellen, aber gleichzeitig langfristige Erweiterungen zu ermöglichen.

## 6. Nichtziele (Phase 1)
Für die erste Projektphase ausdrücklich **nicht** Bestandteil:
- vollautomatische Extraktion aller denkbaren Haushaltsvarianten
- vollständige KI-gesteuerte Systemarchitektur
- politische Interpretation oder Empfehlungssysteme
- vollständige Normalisierung aller kommunalen Datenmodelle

Fokus bleibt auf:
- klar begrenzten Analysefunktionen  
- reproduzierbarer Auswertung  
- robusten Kernfunktionen  

## 7. Zusammenfassung
Die Systemarchitektur des KHHA ist modular, leichtgewichtig und erweiterbar.  
Fachliche Logik ist in unabhängigen Tools gekapselt und kann flexibel je nach Frage eingesetzt werden.  
Das Design ermöglicht sowohl eine schlanke MVP-Umsetzung als auch spätere funktionale Erweiterungen.


