# Zusatzübungen

Für alle, die mit einer Übung früher fertig sind. Die Zusatzübungen sind unabhängig voneinander und setzen den Rechner mindestens auf dem Stand von Übung 6 voraus (Ausnahme: Zusatzübung D).

---

### Zusatz A: Security-Review mit Prüfliste

**Ziel:** Ein Review mit Rolle, konkreter Prüfliste und fester Ausgabeform durchführen und jeden Fund am Code prüfen.
**Projekt:** Rechner
**Dauer:** ca. 20 min

**Schritte:**
1. Neue Chat-Sitzung im **Ask**-Modus, `CalculatorController.java` und `CalculatorService.java` als Kontext anhängen:
   ```text
   Prüfe diesen Code als Security-Reviewer. Achte nur auf:
   - Eingaben, die zu sehr hohem Speicher- oder Rechenaufwand führen
   - Fehlermeldungen, die interne Details preisgeben (Stacktraces, Klassennamen)
   - fehlende Validierung von Eingaben
   - Abhängigkeiten mit bekannten Schwachstellen in build.gradle.kts
   Ausgabe: Tabelle mit Datei, Zeile, Risiko, Empfehlung. Keine Stilkommentare.
   ```
2. Jeden Fund im Code nachvollziehen. Wo möglich, den Fund mit einem Aufruf im Browser bestätigen.

**Abnahmekriterien:**
- Jeder Fund ist als bestätigt oder als nicht zutreffend markiert.
- Für mindestens einen bestätigten Fund gibt es einen Test, der ihn nachweist.

---

### Zusatz B: Dockerfile und CI-Pipeline

**Ziel:** Konfigurationsdateien erzeugen lassen und gegen eine Prüfliste lesen.
**Projekt:** Rechner
**Dauer:** ca. 25 min

**Schritte:**
1. Neue Chat-Sitzung im **Agent**-Modus:
   ```text
   Erstelle ein Dockerfile für diese Anwendung und eine compose.yaml.
   Anforderungen: Multi-Stage-Build mit Gradle, Laufzeit-Image nur mit JRE 21,
   Prozess läuft nicht als root, alle Image-Versionen gepinnt, keine Secrets im Image.
   ```
2. Neue Chat-Sitzung im **Agent**-Modus: eine CI-Pipeline für das im eigenen Unternehmen verwendete System erzeugen lassen (z. B. GitLab CI oder GitHub Actions), die baut und testet.
3. Beide Ergebnisse gegen die Prüfliste lesen:
   - Sind alle Versionen von Images und Actions gepinnt?
   - Läuft der Container als eigener Benutzer?
   - Enthält das Laufzeit-Image nur, was zur Laufzeit nötig ist?
   - Stehen Zugangsdaten im Klartext in einer Datei?

**Abnahmekriterien:**
- Jeder Punkt der Prüfliste ist für beide Dateien beantwortet.
- Ist Docker installiert: `docker compose up --build` startet die Anwendung, http://localhost:8080/api/add?a=3&b=4 antwortet.

---

### Zusatz C: Commit-Message nach Vorgabe

**Ziel:** Mit einem einzigen Beispiel (One-Shot) ein festes Ausgabeformat vorgeben.
**Projekt:** Rechner
**Dauer:** ca. 10 min

**Schritte:**
1. Eine kleine Änderung am Code vornehmen, ohne sie zu committen.
2. Neue Chat-Sitzung im **Ask**-Modus, den Diff einfügen (**Git → Commit**, Datei markieren, **Show Diff**):
   ```text
   Schreibe die Commit-Message zu diesem Diff, genau im Format des Beispiels.

   Beispiel:
   feat(auth): limit session timeout to 30 minutes

   Reason: support reported silent logouts.
   Risk: none, configuration only.

   Diff:
   <hier der Diff>
   ```

**Abnahmekriterien:**
- Die Commit-Message hat Präfix, Betreffzeile, „Reason“ und „Risk“ in dieser Reihenfolge.
- Der Inhalt beschreibt die tatsächliche Änderung.

---

### Zusatz D: Konflikte in der PetClinic auflösen

**Ziel:** Einen Merge-Konflikt mit Copilot analysieren und auflösen; das Ergebnis mit den Tests prüfen.
**Projekt:** Spring PetClinic
**Dauer:** ca. 25 min

**Schritte:**
1. Im Terminal der PetClinic:
   ```powershell
   git fetch origin
   git switch -c merge-test origin/exercise/merge-a
   git merge origin/exercise/merge-b
   ```
2. Neue Chat-Sitzung im **Ask**-Modus: die Datei mit Konflikt als Kontext anhängen und erklären lassen, was jede Seite ändern wollte.
3. Über die Auflösung selbst entscheiden, den Konflikt auflösen und die Tests ausführen:
   ```powershell
   .\mvnw.cmd test
   ```
4. Den Merge abschließen (`git commit`).
5. Den zweiten Fall auf dieselbe Weise zusammenführen, den Konflikt auflösen und die Tests ausführen:
   ```powershell
   git switch -c logic-test origin/exercise/logic-a
   git merge origin/exercise/logic-b
   ```
6. Das Ergebnis der Tests mit Copilot analysieren.

**Abnahmekriterien:**
- Für jede Konfliktstelle aus Schritt 1 ist begründet, welche Seite übernommen oder wie kombiniert wurde.
- Nach Schritt 4 sind alle Tests grün.
- Für Schritt 5 ist festgehalten, ob nach der Auflösung alle Tests grün sind, und für jeden roten Test, welche Anforderung er prüft.

---

### Zusatz E: Einen Skill anlegen (Bonus)

**Ziel:** Eine wiederkehrende Aufgabe als Skill beschreiben, den Copilot bei passenden Aufträgen selbst heranzieht.
**Projekt:** Rechner (Stand nach Übung 6)
**Dauer:** ca. 30 min

**Schritte:**
1. In IntelliJ **Settings → GitHub Copilot → Chat → Agent** öffnen und prüfen, ob Skills aktiviert sind. Fehlt die Einstellung, wird das dem Trainer gemeldet.
2. Die Datei `.github/skills/add-operation/SKILL.md` anlegen und die Schritte an das eigene Projekt anpassen:
   ```markdown
   ---
   name: add-operation
   description: Adds a new arithmetic operation to the calculator REST API following
     the project conventions. Use when asked to add an operation such as power,
     modulo or square root.
   ---

   # Add an operation

   1. Add the calculation as a method in CalculatorService.
   2. Add a GET endpoint /api/<operation> in CalculatorController that delegates
      to the service.
   3. Invalid input returns HTTP 400 with {"error": "<message>"}.
   4. Add the regular cases as rows in src/test/resources/calculations.csv.
      Add at least one error case as a controller test named
      operation_condition_expectedResult.
   5. Run all tests and report the result.
   ```
3. Den Skill committen.
4. Neue Chat-Sitzung im **Agent**-Modus, ohne den Skill zu erwähnen:
   ```text
   Füge eine Potenz-Operation hinzu.
   ```
5. Beobachten, ob der Agent `SKILL.md` liest, und das Ergebnis gegen die Schritte des Skills prüfen.
6. Den Stand committen.

**Abnahmekriterien:**
- Der Agent hat den Skill gelesen.
- Endpunkt, Service-Methode, neue Zeilen in `calculations.csv` und ein Test für einen Fehlerfall entsprechen den Schritten des Skills.
- Alle Tests sind grün.

**Erweiterung:** Mit dem Skill eine Wurzel-Operation hinzufügen. Welchen Fehlerfall wählt Copilot?
