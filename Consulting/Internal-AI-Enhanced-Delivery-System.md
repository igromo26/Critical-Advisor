# Internal AI-Enhanced Delivery System

Stand: 2026-05-13

## Ausgangslage

Mario arbeitet aktuell mit zwei Call-Formaten pro Kunde:

1. `Accountability Call`
   - Zahlen, Daten, Fakten
   - Projektmanagement
   - Roadmap-Stand
   - offene To-dos
   - Accountability
   - Wochenplan und schnelle Anpassungen

2. `Advisory Call`
   - Deep Dives
   - strategische Fragen
   - Hypothesen
   - Sparring
   - Entscheidungen mit groesserer Tiefe

Diese Trennung ist sinnvoll und sollte beibehalten werden.

Der kritische Punkt: Der Accountability Call darf nicht zum gemeinsamen Status-Suchen werden. Er sollte ein Entscheidungs- und Korrekturmeeting sein. Die Analyse muss vorher stark vorverdichtet sein.

## Grundthese

Ein AI-first internes Delivery-System soll Mario nicht ersetzen. Es soll ihn von wiederholbarer Analyse, Status-Synthese, Roadmap-Abgleich und Wochenplan-Erstellung entlasten.

Marios wertvoller Beitrag bleibt:

- Urteilskraft
- Priorisierung
- Interpretation
- Hypothesen-Qualitaet
- Trade-off-Entscheidungen
- klares Challenging des Kunden

AI soll vorbereiten, verdichten, Muster erkennen, Abweichungen markieren und erste Vorschlaege erzeugen. Mario entscheidet.

## Zielbild

Jeder Kunde hat ein eigenes Delivery Cockpit.

Dieses Cockpit sammelt laufend:

- KPI-Daten
- Roadmap-Status
- offene To-dos
- Entscheidungen
- Hypothesen
- Learnings
- Risiken
- Abhaengigkeiten
- letzte Call-Notizen
- naechste Commitments

Aus diesem Cockpit erzeugt das interne AI-System jede Woche automatisch oder halbautomatisch:

- Weekly Performance Brief
- Roadmap Drift Analysis
- Open Loops Summary
- Hypothesis Review
- Suggested Weekly Plan
- Accountability Call Agenda
- Advisory Call Themenvorschlaege

## Kernprinzip: AI Prepares, Mario Judges

AI darf nicht die Strategie final bestimmen.

AI darf:

- Daten zusammenfassen
- Veraenderungen erkennen
- Muster vorschlagen
- Abweichungen markieren
- Hypothesen formulieren
- Fragen vorbereiten
- Wochenplaene entwerfen
- Risiken sichtbar machen

Mario muss:

- Kontext bewerten
- Kausalitaet pruefen
- Prioritaeten setzen
- falsche Muster verwerfen
- mit dem Kunden entscheiden
- unbequeme Punkte ansprechen

## Woechentlicher Delivery Loop

### 1. Data Intake

Ziel: Alle relevanten Inputs fuer die Woche einsammeln.

Quellen:

- CRM
- Marketing Automation
- Analytics
- Ads
- Pipeline-Reports
- Sales-Feedback
- Customer-Feedback
- Projektmanagement-Tool
- Roadmap
- letzte Call-Notizen
- Slack/Email-Auszüge, falls relevant

Output:

- aktualisierte KPI-Snapshots
- offene Aufgaben
- neue Blocker
- relevante Kundenupdates

AI-Unterstuetzung:

- Daten normalisieren
- fehlende Daten markieren
- Aenderungen zur Vorwoche erkennen
- ungewoehnliche Ausschlaege markieren

### 2. Metric Movement Analysis

Ziel: Schnell verstehen, was rauf, runter oder gleich geblieben ist.

Fragen:

- Welche Metriken haben sich relevant bewegt?
- Ist die Bewegung positiv, negativ oder uneindeutig?
- Gibt es eine plausible Erklaerung?
- Ist es Signal oder Noise?
- Welche Metriken sind kritisch, aber fehlen?

Output:

- KPI Movement Summary
- Signal vs. Noise Einschätzung
- Fragen an den Kunden
- moegliche Ursachenhypothesen

AI-Unterstuetzung:

- Woche-zu-Woche-Vergleich
- Trendbeschreibung
- Anomalie-Erkennung
- erste Interpretation nach vorgegebenem KPI-Framework

Kritische Regel:

> AI darf Korrelationen markieren, aber Mario muss Kausalitaet pruefen.

### 3. Roadmap Drift Analysis

Ziel: Erkennen, ob der Kunde noch an den wichtigen Dingen arbeitet.

Fragen:

- Welche Roadmap-Initiativen sind on track?
- Welche sind verspätet?
- Welche wurden gestartet, obwohl sie nicht priorisiert waren?
- Welche wichtigen Aufgaben wurden nicht bewegt?
- Gibt es Scope Creep?
- Gibt es Aktionismus?

Output:

- Roadmap Status
- Drift Alerts
- Stop/Continue/Change Empfehlungen
- Eskalationspunkte

AI-Unterstuetzung:

- To-dos gegen Roadmap matchen
- offene Schleifen erkennen
- nicht eingehaltene Commitments markieren
- Themencluster bilden

### 4. Hypothesis Review

Ziel: Jede Woche pruefen, ob die zentralen Annahmen noch halten.

Fragen:

- Welche Hypothesen testen wir gerade?
- Welche neuen Signale haben wir?
- Was wurde bestaetigt?
- Was wurde geschwaecht?
- Welche Hypothese muss angepasst werden?
- Welche Hypothese ist tot?

Output:

- Hypothesis Status Board
- neue oder aktualisierte Annahmen
- Empfehlungen fuer naechste Tests

AI-Unterstuetzung:

- alte Hypothesen aus dem Kundenkontext ziehen
- neue Evidenz dagegenhalten
- Widersprueche markieren
- Fragen fuer Deep Dive vorbereiten

### 5. Impact Contract Review

Ziel: Sicherstellen, dass Initiativen nicht nur abgearbeitet werden, sondern Revenue-Wirkung erzeugen.

Fuer jeden aktiven Hebel pruefen:

- Problem
- Hypothese
- Zielmetrik
- Baseline
- Zielwert
- Zeithorizont
- Owner
- aktuelle Evidenz
- Blocker
- Stop-/Pivot-Kriterium

Output:

- Impact Contract Status
- naechste Entscheidung pro Hebel
- klare Empfehlung: Continue, Adjust, Stop, Escalate

AI-Unterstuetzung:

- Hebelstatus aus Daten und To-dos synthetisieren
- fehlende Evidenz markieren
- schwache Impact-Logik identifizieren

### 6. Weekly Plan Draft

Ziel: Aus Daten, Roadmap, Hypothesen und Blockern einen Vorschlag fuer die naechste Woche erzeugen.

Der Wochenplan sollte enthalten:

- 3 bis 5 Prioritaeten
- konkrete Outputs
- Owner
- Deadline
- Impact-Bezug
- Abhaengigkeiten
- Entscheidungen, die im Call gebraucht werden
- Dinge, die bewusst nicht gemacht werden

AI-Unterstuetzung:

- ersten Wochenplan generieren
- To-dos clustern
- Prioritaeten gegen Impact Contracts pruefen
- Vorschlag fuer Call-Agenda erstellen

Mario prueft:

- Ist das wirklich wichtig?
- Ist das zu viel?
- Ist es die richtige Reihenfolge?
- Ist der Owner realistisch?
- Ist der Revenue-Bezug klar?

## Accountability Call

Zweck:

> Gemeinsame Steuerung des Revenue-Impact-Systems.

Der Call sollte nicht laenger der Ort sein, an dem man erst herausfindet, was los ist.

Standardagenda:

1. Wichtigste KPI-Bewegungen
2. Roadmap-Abweichungen
3. Impact Contract Status
4. Blocker und Entscheidungen
5. Wochenplan finalisieren
6. Commitments bestaetigen

Nicht in diesen Call:

- lange strategische Grundsatzdiskussionen
- Tool-Detailarbeit
- kreative Deep Dives
- neue Ideen ohne Bezug zu aktuellen Hebeln

Kritische Frage:

> Was muessen wir diese Woche anders machen, weil die Daten oder der Roadmap-Status es verlangen?

## Advisory Call

Zweck:

> Tieferes Denken, bessere Entscheidungen und strategische Schaerfung.

Moegliche Themen:

- Positionierung
- Messaging
- ICP
- GTM Motion
- Revenue-Architektur
- AI Workflow Design
- Sales/Marketing Alignment
- Product- oder Customer-Insights
- groessere Richtungsentscheidungen

Input aus dem AI-System:

- Themenvorschlaege aus wiederkehrenden Blockern
- Muster aus Daten und Calls
- offene strategische Fragen
- Hypothesen mit hoher Unsicherheit
- Entscheidungen, die nicht im Accountability Call geloest werden sollten

Kritische Frage:

> Welche Annahme oder Entscheidung limitiert gerade den naechsten Revenue-Hebel?

## Kundencockpit

Jeder Kunde sollte eine strukturierte Arbeitsumgebung haben.

Minimalstruktur:

- `Context`
- `Goals`
- `KPI Snapshot`
- `Roadmap`
- `Impact Contracts`
- `Hypotheses`
- `Decision Log`
- `Open Loops`
- `Weekly Plans`
- `Call Notes`
- `AI Workflows`
- `Risks`

Das kann in Notion, Airtable, Linear, GitHub, Google Sheets oder einer Kombination liegen. Wichtig ist nicht das Tool, sondern die Struktur.

## Interne AI-Agenten oder Prompts

Ein AI-first Delivery-System koennte mit spezialisierten internen Agenten oder Prompt-Routinen arbeiten:

### KPI Analyst

Aufgabe:

- Metrikbewegungen zusammenfassen
- Auffaelligkeiten markieren
- fehlende Daten benennen

### Roadmap Auditor

Aufgabe:

- To-dos gegen Roadmap und Impact Contracts pruefen
- Drift, Scope Creep und offene Schleifen erkennen

### Hypothesis Challenger

Aufgabe:

- aktive Hypothesen mit neuer Evidenz abgleichen
- Gegenargumente und Alternativerklaerungen liefern

### Weekly Planner

Aufgabe:

- aus Roadmap, Blockern und Impact Contracts einen Wochenplan vorschlagen

### Advisory Briefing Agent

Aufgabe:

- Deep-Dive-Themen fuer den Advisory Call vorbereiten
- strategische Fragen zuspitzen
- Entscheidungsoptionen strukturieren

## Artefakte pro Woche

Jede Woche sollte fuer jeden aktiven Kunden mindestens entstehen:

- `Weekly Performance Brief`
- `Roadmap Drift Summary`
- `Impact Contract Review`
- `Weekly Plan`
- `Decision Log Update`
- `Advisory Topics Backlog`

Diese Artefakte duerfen kurz sein. Entscheidend ist ihre Wiederholbarkeit.

## Automatisierungsgrade

### Stufe 1: Manual plus AI

Mario exportiert oder kopiert Daten manuell und laesst AI die Briefings erzeugen.

Gut fuer Start.

### Stufe 2: Semi-Automated Cockpit

Daten liegen in festen Templates. AI kann jede Woche konsistent vergleichen.

Wahrscheinlich kurzfristig beste Stufe.

### Stufe 3: Integrated Delivery OS

API-Integrationen ziehen KPI-, Roadmap- und CRM-Daten automatisch.

Stark, aber nur sinnvoll, wenn Marios Delivery-System stabil genug ist.

Kritische Warnung:

> Nicht zu frueh automatisieren. Erst den Denkprozess standardisieren, dann die Technik.

## Was Mario nicht automatisieren sollte

Nicht automatisieren:

- finales Urteil
- kritisches Challenging
- Prioritaetenentscheidung
- schwierige Kundengespräche
- Trade-off-Entscheidungen
- Kontextinterpretation

Automatisieren oder stark unterstuetzen:

- Zusammenfassungen
- Vergleiche
- Statusabgleich
- Meeting-Vorbereitung
- Dokumentation
- erste Wochenplan-Entwuerfe
- offene Schleifen
- Follow-up-Entwuerfe

## Kritische Bewertung des aktuellen Prozesses

Was gut ist:

- klare Trennung zwischen Accountability und Advisory
- woechentlicher Zahlencheck
- Roadmap-Abgleich
- Wochenplan als wiederkehrendes Steuerungsinstrument
- Hypothesen werden nicht vergessen, sondern regelmaessig ueberprueft

Was verbessert werden muss:

- Der Prozess ist noch zu stark in Marios Kopf.
- Die Analyse dauert zu lange.
- Hypothesen, Roadmap und To-dos sind wahrscheinlich noch nicht ausreichend in einem System verbunden.
- Wochenplaene koennen nur dann wirklich gut sein, wenn sie explizit auf Impact Contracts verweisen.
- Advisory-Themen sollten aus wiederkehrenden Mustern und Blockern gespeist werden, nicht nur aus spontanen Anliegen.

## Zielmetrik fuer das interne Delivery-System

Das System ist erfolgreich, wenn:

- Mario weniger Zeit fuer Statussuche braucht.
- Mario schneller erkennt, was wirklich relevant ist.
- jeder Call mit klarer Voranalyse startet.
- jeder Wochenplan auf Impact Contracts verweist.
- weniger offene Schleifen liegen bleiben.
- Kunden besser verstehen, warum Prioritaeten gesetzt werden.
- Mario mehr Kunden betreuen kann, ohne in operative Hektik zu fallen.

## Naechste Systementscheidung

Die wichtigste naechste Entscheidung ist nicht das Tool.

Die wichtigste Entscheidung ist:

> Welche Standarddaten, Standardartefakte und Standardfragen braucht jeder Kunde jede Woche?

Erst danach sollte entschieden werden, ob das System in Notion, Airtable, Linear, GitHub, Sheets oder einer eigenen kleinen App abgebildet wird.
