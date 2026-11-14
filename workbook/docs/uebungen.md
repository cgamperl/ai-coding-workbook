# Übungen

Die Übungen 3 bis 7 bauen aufeinander auf: Der Rechner aus Übung 3 wird in den folgenden Übungen getestet, mit Regeln versehen, umgebaut und erweitert. Jede Übung beginnt mit einer neuen Chat-Sitzung.

---

### Übung 1: Setup

**Ziel:** Das Projekt für den Rechner erzeugen, Copilot in Betrieb nehmen und die Bedienelemente finden.
**Projekt:** Rechner
**Dauer:** ca. 15 min

**Schritte:**
1. In IntelliJ **File → New → Project** öffnen und links **Spring Boot** wählen.
2. Folgende Werte eintragen:

   | Feld | Wert |
   |---|---|
   | Name | `calculator` |
   | Language | Java |
   | Type | Gradle - Kotlin |
   | Group | `at.tectrain.training` |
   | Artifact | `calculator` |
   | Package name | `at.tectrain.training.calculator` |
   | JDK / Java | 21 |
   | Packaging | Jar |
   | Create Git repository | aktiviert, falls angeboten |

3. Mit **Next** weiter. Spring Boot **4.1.2** wählen und **keine** Abhängigkeiten auswählen. Mit **Create** abschließen.
4. Warten, bis IntelliJ das Gradle-Projekt geladen hat. Im Terminal von IntelliJ den Build starten:
   ```powershell
   .\gradlew.bat build
   ```
5. In der Statusleiste das Copilot-Symbol prüfen: Copilot ist angemeldet.
6. Den Chat über das Symbol **GitHub Copilot Chat** am rechten Fensterrand öffnen. Die Auswahlliste der Modi unten im Chat öffnen und die verfügbaren Modi notieren.
7. Die Modellauswahl im Chat öffnen und das zu Kursbeginn genannte Standardmodell einstellen.
8. Copilot-Symbol in der Statusleiste → **View quota usage**: den aktuellen Verbrauch notieren.
9. Fehlt in der Menüleiste der Eintrag **Git**, das Repository über **VCS → Create Git Repository** anlegen. Den Ausgangsstand committen (**Git → Commit**).
10. Die PetClinic für Übung 2 klonen: **File → New → Project from Version Control**, URL `https://github.com/cgamperl/spring-petclinic`, in einem neuen Fenster öffnen. Fragt IntelliJ nach dem Build-Werkzeug, Maven wählen. IntelliJ lädt die Abhängigkeiten im Hintergrund.

**Rückfallebenen:**
- Fehlt der Eintrag **Spring Boot** im Dialog: https://start.spring.io im Browser öffnen, dieselben Werte eintragen, **Generate** wählen, das ZIP entpacken und den Ordner in IntelliJ mit **File → Open** öffnen.
- Ist start.spring.io nicht erreichbar: [calculator.zip](https://cgamperl.github.io/ai-coding-workbook/downloads/calculator.zip) herunterladen, entpacken und öffnen.

**Abnahmekriterien:**
- Der Build endet mit `BUILD SUCCESSFUL`.
- Copilot ist angemeldet, der Chat lässt sich öffnen.
- Die Modi Ask, Agent und Plan sind vorhanden. Fehlt einer davon, wird das dem Trainer gemeldet.
- Der Ausgangswert des Credit-Verbrauchs ist notiert.

---

### Übung 2: Bestehenden Code erkunden

**Ziel:** Eine unbekannte Anwendung mit Copilot erkunden, den Unterschied zwischen Ask- und Agent-Modus beobachten und Antworten am Code prüfen.
**Projekt:** Spring PetClinic
**Dauer:** ca. 25 min

**Schritte:**
1. Das in Übung 1 geklonte Projekt PetClinic öffnen.
2. Neue Chat-Sitzung im **Ask**-Modus:
   ```text
   Erkläre den Aufbau dieses Projekts: Schichten, wichtigste Klassen und den Weg
   einer Anfrage, wenn nach einem Besitzer (Owner) gesucht wird.
   ```
   Eine Klasse oder Methode aus der Antwort im Code aufsuchen und prüfen, ob die Beschreibung zutrifft.
3. Alle Editor-Tabs schließen und im **Ask**-Modus fragen:
   ```text
   Wie viele Besitzer zeigt die Suchergebnisliste pro Seite an?
   ```
   Danach `OwnerController.java` öffnen, dieselbe Frage in einer neuen Sitzung stellen und beide Antworten vergleichen.
4. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Welche Spring-Boot-Version verwendet das Projekt, und laufen alle Tests?
   ```
   Beobachten: Welche Dateien liest der Agent? Welche Befehle möchte er ausführen? Jeden Befehl vor der Freigabe lesen. Die Zahl der Runden bis zur Antwort notieren.
5. Neue Chat-Sitzung im **Ask**-Modus:
   ```text
   Wie erzeugt die Anwendung Rechnungen für Tierarztbesuche als PDF?
   ```
   Die Antwort am Code prüfen.

**Abnahmekriterien:**
- Mindestens eine Aussage aus Schritt 2 ist am Code bestätigt oder widerlegt.
- Für Schritt 3 ist festgehalten, ob die Antwort ohne geöffnete Datei auf dem Code beruht oder geraten ist.
- In Schritt 4 stammt die Version aus einer gelesenen Datei und das Testergebnis aus einem ausgeführten Befehl. Übersprungene Tests sind mit Grund festgehalten.
- Für Schritt 5 ist festgehalten, ob Copilot das Fehlen der Funktion erkennt oder eine Umsetzung beschreibt, die es im Code nicht gibt.

**Zusatz:** Die Frage aus Schritt 4 im Ask-Modus stellen. Worin unterscheidet sich die Antwort, und worauf beruht sie?

---

### Übung 3: Der erste Controller

**Ziel:** Einen REST-Controller mit Inline-Vorschlägen schreiben und einen fehlschlagenden Build mit Copilot analysieren.
**Projekt:** Rechner
**Dauer:** ca. 25 min

**Schritte:**
1. Im Paket `at.tectrain.training.calculator` die Klasse `CalculatorController` anlegen.
2. Über der Klasse die Annotation `@RestController` schreiben. Danach einen Javadoc-Kommentar für die erste Methode schreiben und Copilot die Methode ergänzen lassen:
   ```java
   /**
    * Adds two numbers.
    * Example: GET /api/add?a=3&b=4 returns 7.
    */
   ```
   Vorschläge mit `Tab` übernehmen, mit `Alt+]` und `Alt+[` Alternativen ansehen, mit `Strg+→` wortweise übernehmen.
3. Auf dieselbe Weise Subtraktion, Multiplikation und Division ergänzen (`/api/subtract`, `/api/multiply`, `/api/divide`). Die Berechnung steht jeweils direkt in der Controller-Methode.
4. Den Build starten:
   ```powershell
   .\gradlew.bat build
   ```
5. Neue Chat-Sitzung im **Ask**-Modus. Die Fehlermeldung aus dem Terminal einfügen:
   ```text
   Warum schlägt dieser Build fehl? Erkläre die Ursache. Ändere noch nichts.
   ```
6. Neue Chat-Sitzung im **Agent**-Modus: die Ursache beheben lassen. Den Diff prüfen, bevor er übernommen wird.
7. Die Anwendung starten (`CalculatorApplication` → Run) und im Browser http://localhost:8080/api/add?a=3&b=4 aufrufen.
8. Den Stand committen.

**Abnahmekriterien:**
- Die Analyse in Schritt 5 nennt die Ursache, ohne Code zu ändern.
- Die Korrektur ändert nur `build.gradle.kts`.
- Der Build endet mit `BUILD SUCCESSFUL`, alle vier Endpunkte liefern im Browser das erwartete Ergebnis.

**Zusatz:** Welchen Starter hat Copilot in `build.gradle.kts` eingetragen? Auf https://start.spring.io die Abhängigkeit „Spring Web“ wählen, mit **Explore** die erzeugte `build.gradle.kts` ansehen und vergleichen.

---

### Übung 4: Tests – vager und gegliederter Prompt

**Ziel:** Erleben, welche Entscheidungen ein vager Prompt Copilot überlässt, und sie mit einem gegliederten Prompt selbst treffen.
**Projekt:** Rechner
**Dauer:** ca. 25 min

**Schritte:**
1. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Schreibe Tests für den CalculatorController.
   ```
2. Die erzeugten Tests ausführen und in einer Tabelle festhalten:

   | Frage | Antwort aus den Tests |
   |---|---|
   | Was erwarten die Tests bei Division durch 0? | |
   | Werden fehlende oder nicht numerische Parameter geprüft? | |
   | Werden Dezimalzahlen geprüft? | |
   | Welche Testart wird verwendet (Unit-Test, `@WebMvcTest`, `@SpringBootTest`)? | |

3. Die Änderungen verwerfen (**Git → Rollback**).
4. Neue Chat-Sitzung im **Agent**-Modus mit gegliedertem Prompt:
   ```text
   <aufgabe>
   Schreibe Tests für den CalculatorController.
   </aufgabe>
   <dateien>
   src/main/java/at/tectrain/training/calculator/CalculatorController.java
   build.gradle.kts
   </dateien>
   <regeln>
   - Spring Boot 4.1, JUnit 5, @WebMvcTest mit MockMvc.
   - Keine neuen Abhängigkeiten außer dem passenden Test-Starter.
   - Testnamen nach dem Schema operation_condition_expectedResult,
     z. B. divide_byZero_returnsBadRequest.
   - Gewünschtes Verhalten, auch wo der Code es noch nicht umsetzt:
     - Division durch 0 liefert HTTP 400 mit {"error": "Division by zero"}.
     - Fehlender oder nicht numerischer Parameter liefert HTTP 400.
     - Dezimalzahlen sind erlaubt: /api/add?a=0.1&b=0.2 liefert 0.3.
   - Tests, die am aktuellen Code scheitern, werden nicht an den Code angepasst.
   </regeln>
   <ausgabe>
   Eine Testklasse CalculatorControllerTest. Danach eine Liste der
   fehlschlagenden Tests mit Begründung.
   </ausgabe>
   ```
5. Die Tests ausführen und die Tabelle aus Schritt 2 für dieses Ergebnis ausfüllen.
6. In derselben Sitzung:
   ```text
   Passe den CalculatorController an, bis alle Tests grün sind. Ändere die Tests nicht.
   ```
7. Den Stand committen.

**Abnahmekriterien:**
- Die Tabelle zeigt für beide Prompts, welche Entscheidungen Copilot selbst getroffen hat.
- Die Tests aus Schritt 4 folgen dem Namensschema und prüfen das vorgegebene Verhalten.
- Nach Schritt 6 sind alle Tests grün, und der Diff von `CalculatorControllerTest` zeigt keine Änderung durch Schritt 6.

**Zusatz:** Prüfen, ob die Tests aus Schritt 1 das gewünschte Verhalten prüfen oder das Verhalten, das der Code zu diesem Zeitpunkt hatte.

---

### Übung 5: Projekt-Regeln

**Ziel:** Projektwissen dauerhaft in `.github/copilot-instructions.md` festhalten und die Wirkung prüfen.
**Projekt:** Rechner
**Dauer:** ca. 25 min

**Schritte:**
1. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Erstelle .github/copilot-instructions.md für dieses Projekt. Höchstens 30 Zeilen.
   Abschnitte: Tech-Stack, Architektur, Konventionen, No-Gos.
   ```
2. Die Datei lesen und so überarbeiten, dass mindestens folgende Regeln enthalten sind:
   - Java 21, Spring Boot 4.1, Gradle mit Kotlin-DSL, JUnit 5, `@WebMvcTest` mit MockMvc.
   - Controller enthalten keine Fachlogik; Berechnungen liegen in Service-Klassen.
   - Fehler liefern HTTP 400 mit `{"error": "<Meldung>"}`.
   - Testnamen nach dem Schema `operation_condition_expectedResult`.
   - Keine neuen Abhängigkeiten ohne Rückfrage.
   - Code, Kommentare und Testnamen auf Englisch.
3. Die Datei committen.
4. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Füge eine Modulo-Operation hinzu.
   ```
5. Das Ergebnis gegen die Regeln aus Schritt 2 prüfen.
6. Die Änderungen aus Schritt 4 verwerfen (**Git → Rollback**). Die Regeln bleiben.

**Abnahmekriterien:**
- `.github/copilot-instructions.md` enthält die Regeln aus Schritt 2 und ist committet.
- Für jede Regel ist festgehalten, ob das Ergebnis aus Schritt 4 sie einhält.
- Für die Regel zur Fachlogik ist festgehalten, wie Copilot mit dem Widerspruch zwischen Regel und bestehendem Controller umgegangen ist.

**Zusatz:** Wo zeigt Copilot an, dass die Regeldatei in die Antwort eingeflossen ist?

---

### Übung 6: Refactoring

**Ziel:** Die Tests auf datengetriebene Tests umstellen und danach die Fachlogik aus dem Controller in eine Service-Klasse verschieben, abgesichert durch diese Tests.
**Projekt:** Rechner
**Dauer:** ca. 35 min

**Teil A – Datengetriebene Tests**

1. Alle Tests ausführen: Sie sind grün.
   ```powershell
   .\gradlew.bat test
   ```
2. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Stelle die Tests in CalculatorControllerTest, die sich nur in den Eingabewerten
   und im erwarteten Ergebnis unterscheiden, auf @ParameterizedTest mit @CsvSource um.
   Die geprüften Fälle und Erwartungswerte bleiben unverändert. Führe danach alle
   Tests aus.
   ```
3. Den Diff prüfen: Jeder bisherige Fall ist als Zeile in einer Datenquelle wiederzufinden.
4. In derselben Sitzung die Daten in eine Datei auslagern lassen:
   ```text
   Lagere die Testdaten der Rechenfälle in die Datei
   src/test/resources/calculations.csv aus und lies sie mit @CsvFileSource.
   ```
5. In `calculations.csv` eine weitere Zeile für einen neuen Rechenfall ergänzen, ohne den Testcode zu ändern, und die Tests ausführen.
6. Den Stand committen.

**Teil B – Service extrahieren**

7. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Verschiebe die Rechenlogik aus CalculatorController in eine neue Klasse
   CalculatorService. Das Verhalten der API bleibt unverändert. In den Testklassen
   dürfen nur Testkonfiguration und Setup angepasst werden, keine Aufrufe,
   Testdaten, Erwartungswerte oder Assertions. Führe danach alle Tests aus.
   ```
8. Den Diff prüfen, bevor er übernommen wird: **Git → Commit** zeigt alle geänderten Dateien.
9. Alle Tests erneut selbst ausführen und den Stand committen.

**Abnahmekriterien:**
- Die Rechenfälle stehen in `calculations.csv`; die neue Zeile aus Schritt 5 wird als eigener Testfall ausgeführt.
- Kein Fall aus den Tests von Übung 4 ist bei der Umstellung verloren gegangen.
- `CalculatorController` enthält keine Berechnungen mehr, sondern ruft `CalculatorService` auf.
- Alle Tests sind grün; im Diff von Teil B sind Testdaten, Erwartungswerte und Assertions unverändert.
- Die Controller-Tests verwenden den echten `CalculatorService`, keinen Mock. Andernfalls prüfen sie die Rechenlogik nicht mehr.

**Zusatz:** Unit-Tests für `CalculatorService` ohne Spring-Kontext erzeugen lassen, die dieselbe Datei `calculations.csv` verwenden.

---

### Übung 7: Planen, dann ausführen

**Ziel:** Eine unvollständige Anforderung erst planen lassen, den Plan prüfen und ihn dann umsetzen. Die Kosten von Planung und Umsetzung mit unterschiedlichen Modellen vergleichen.
**Projekt:** Rechner
**Dauer:** ca. 40 min

**Ticket:**

> **CALC-7 Rechenverlauf**
> Die letzten Berechnungen sollen über die API abrufbar sein, damit Anwender ihre Ergebnisse nachvollziehen können.

**Schritte:**
1. Den aktuellen Credit-Verbrauch notieren.
2. Neue Chat-Sitzung im **Plan**-Modus. Das zu Kursbeginn genannte leistungsstärkere Modell wählen.
   ```text
   Erstelle einen Umsetzungsplan für dieses Ticket. Stelle offene Fragen,
   statt Annahmen zu treffen.

   CALC-7 Rechenverlauf: Die letzten Berechnungen sollen über die API abrufbar
   sein, damit Anwender ihre Ergebnisse nachvollziehen können.
   ```
3. Den Plan prüfen:
   - Welche Lücken im Ticket hat Copilot benannt, welche hat es still entschieden?
   - Sind Tests Teil des Plans?
   - Werden nur Dateien geändert, die für das Ticket nötig sind?
   - Hält der Plan die Projekt-Regeln aus Übung 5 ein?
4. Offene Fragen beantworten und den Plan korrigieren, bis er vollständig ist.
5. Den Credit-Verbrauch notieren.
6. Auf das Standardmodell wechseln und die Umsetzung starten: in den **Agent**-Modus wechseln und den Plan umsetzen lassen.
7. Alle Tests ausführen und den Credit-Verbrauch notieren.
8. Den Stand committen.

**Ohne Plan-Modus:** Im **Agent**-Modus mit dem Zusatz „Erstelle nur einen Plan. Ändere keine Dateien.“ arbeiten.

**Abnahmekriterien:**
- Der Plan enthält offene Fragen oder ausdrücklich benannte Annahmen zu den Lücken des Tickets.
- Die Umsetzung entspricht den beantworteten Fragen.
- Für den Rechenverlauf gibt es Tests, alle Tests sind grün.
- Der Verbrauch von Planung und Umsetzung ist getrennt notiert.

**Zusatz:** Den Plan in einer neuen Sitzung mit dem Standardmodell erstellen lassen und mit dem ersten Plan vergleichen.
