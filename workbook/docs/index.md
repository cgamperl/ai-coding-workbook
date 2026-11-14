# AI Assisted Coding mit GitHub Copilot

Übungen zum Kurs „Einstieg in AI Assisted Coding mit GitHub Copilot“. Die Übungen laufen in IntelliJ IDEA mit dem Plugin GitHub Copilot.

## Projekte

| Projekt | Verwendung | Bezug |
|---|---|---|
| Rechner | Übungen 1 und 3–8: ein REST-Rechner, der Schritt für Schritt mit Copilot entsteht | wird in Übung 1 erzeugt; Ersatz: [calculator.zip](https://cgamperl.github.io/ai-coding-workbook/downloads/calculator.zip) |
| Spring PetClinic | Übung 2 und Zusatzübung D: bestehende Anwendung zum Erkunden | `https://github.com/cgamperl/spring-petclinic` |

## Arbeitsregeln

- **Eine neue Chat-Sitzung pro Übung.** Ein langer Verlauf wird bei jeder Anfrage erneut übertragen: Er kostet Credits und verschlechtert die Ergebnisse.
- **Standardmodell:** das Modell, das zu Kursbeginn genannt wird. Ein anderes Modell nur dort, wo die Übung es verlangt.
- **Freigaben lesen:** Im Agent-Modus fragt Copilot vor dem Ausführen von Befehlen nach. Der angezeigte Befehl wird vor der Freigabe gelesen.
- **Ergebnisse prüfen:** Copilot liefert bei jedem Lauf ein etwas anderes Ergebnis. Die Übungen nennen deshalb Abnahmekriterien statt einer exakten Ausgabe.
- **Zwischenstände committen:** Der Rechner ist ein Git-Repository. Nach jeder Übung wird der Stand committet; misslungene Änderungen lassen sich so verwerfen.

## AI Credits

- Für den Kurstag stehen jeder Person 1000 GitHub AI Credits zur Verfügung (1 Credit = 0,01 USD).
- Chat und Agent verbrauchen Credits nach Anzahl der verarbeiteten Token und nach dem Preis des gewählten Modells. Jede Runde eines Agenten überträgt den gesamten bisherigen Verlauf erneut.
- Inline-Vorschläge im Editor verbrauchen keine Credits.
- Sind die Credits aufgebraucht, antwortet der Chat nicht mehr.
- Verbrauch ablesen: Copilot-Symbol in der Statusleiste von IntelliJ → **View quota usage**. Die Bezeichnung kann je nach Version des Plugins abweichen.

## Bedienung in IntelliJ

| Aktion | Bedienung |
|---|---|
| Chat öffnen | Symbol **GitHub Copilot Chat** am rechten Fensterrand |
| Modus wählen | Auswahlliste unten im Chat: Agent, Ask, Plan, Edit |
| Datei als Kontext | Datei in das Eingabefeld ziehen, oder Rechtsklick auf die Datei → **GitHub Copilot** → **Reference File in Chat** |
| Befehle im Chat | `/` im Eingabefeld zeigt die verfügbaren Befehle |
| Inline-Vorschlag übernehmen | `Tab` |
| Inline-Vorschlag wortweise übernehmen | `Strg+→` |
| Nächster / vorheriger Vorschlag | `Alt+]` / `Alt+[`; auf deutscher Tastatur ggf. abweichend, Belegung unter **Settings → Keymap**, Suche „Copilot“ |
| Vorschlag verwerfen | `Esc` |

Die geöffnete Datei und markierter Code gehen automatisch als Kontext an Copilot.
