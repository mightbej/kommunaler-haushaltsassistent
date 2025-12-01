# OCR/Parsing – Architektur-Ideen für das KHHA

Der KHHA benötigt strukturierte Haushaltsdaten.

Das dazu notwendig Parsing kommunaler Haushaltspläne ist kein täglicher Prozess.  
In der Regel muss ein kommunaler Haushalt nur einmal pro Jahr eingelesen werden.

Diese Aufgabe ist aufgrund der heterogenen Layouts kommunaler Haushaltspläne ungewöhnlich anspruchsvoll.  

Deshalb wird das Parsing im Rahmen des Projekts systematisch analysiert und ab Förderbeginn in eine robuste, modulare Pipeline überführt.“

Der Haushaltsassistent bleibt vollständig funktionsfähig, auch wenn Daten auf anderem Wege bereitgestellt werden.

## 1. Problemkontext
Kommunale Haushaltspläne liegen überwiegend in PDF‑Form vor. 
Sie sind **heterogen, schwer auslesbar und oft nicht maschinenlesbar**. Typische Merkmale:

- unterschiedliche Layouts je Kommune  
- Tabellen als Bilder statt Text  
- Farbige oder schlecht kontrastierte Schriften  
- verdrehte oder gescannte Seiten  
- Tabellen über mehrere Seiten ohne wiederholte Überschriften  
- uneinheitliche Formatierungen, Mischformen aus Text, Zahlen, Fußnoten  

Diese Eigenschaften machen klassische Parser (z. B. Regex, PDF‑Extraktion) unzuverlässig und erfordern einen mehrstufigen, KI‑gestützten Ansatz.

## 2. Grundprinzip der Lösung
Statt einen einzigen Parser zu entwickeln, setzt das KHHA auf eine **pipeline-basierte, modulare Architektur**, die Daten aus mehreren Quellen kombiniert:

1. **Visuelle Information** der PDF-Seite (Bilddaten)  
2. **Plumber‑Extrakte** (Text, Tabellenfragmente)  
3. **OCR‑Ergebnisse**  
4. **Haushaltsspezifisches Prompting** beim LLM  

## 3. Architektur-Bausteine für die Veröffentlichung

### 3.1 Preprocessing-Schicht (konzeptionell)
- Drehen und Ausrichten von Seiten  
- Entfernen leerer Seiten  
- Normalisierung der Auflösung  
- Erkennen von tabellenlastigen vs. textlastigen Seiten  

### 3.2 Multimodale Extraktionsschicht
Für jede Seite werden mehrere Datenformen erzeugt:

- Bild (PNG/JPEG)  
- `extract_text()`  
- `extract_tables()`  
- OCR‑Text  

Diese Daten werden **nicht einzeln verwertet**, sondern dienen als Input für eine nachgelagerte KI‑Interpretation.

### 3.3 Seite‑zu‑JSON‑Interpretation (LLM)
Das LLM erhält:

- Bild  
- alle Textextrakte  
- alle Tabellenauszüge  
- ein Haushalts-Prompt, das Prioritäten und Regeln erklärt  

Beispielhafte Regeln (rein konzeptionell):

- Zahlen aus dem Bild haben Priorität  
- OCR‑Text dient der Bestätigung  
- Tabellenköpfe rekonstruieren, wenn sie fehlen  
- Seitenübergreifende Tabellen logisch zusammenführen  

### 3.4 Fallback-Mechanismen
Damit das System robust ist:

- Wenn Tabellen fehlen → LLM rekonstruiert Struktur aus Layout + OCR  
- Wenn OCR unklar → Bild hat Vorrang  
- Wenn Spaltenköpfe fehlen → semantische Interpretation  
- Wenn Farben schlecht lesbar → Vision‑Modell gleicht aus  

### 3.5 Vollständige Trennung:  
**Dokumenten-Pipeline ≠ Fachliche Haushaltslogik**

