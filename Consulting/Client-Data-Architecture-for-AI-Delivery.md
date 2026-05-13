# Client Data Architecture for AI Delivery

Stand: 2026-05-13

## Ausgangsfrage

Mario braucht fuer sein internes AI-enhanced Delivery-System Kundendaten, die jede Woche analysiert werden koennen:

- unterschiedliche Kunden haben unterschiedliche KPI-Definitionen,
- relevante KPIs haengen vom jeweiligen GTM-Modell ab,
- Historie muss vergleichbar bleiben,
- Daten sollen nicht zu einer unkontrollierten Datenhalde werden,
- AI soll nicht jedes Mal riesige Rohdatenmengen als Input bekommen,
- CRM-Relationen wie Deals, Kontakte, Unternehmen und Associations muessen korrekt interpretierbar bleiben.

## Kurzempfehlung

Nicht:

> Alle Daten flach in Google Sheets werfen und AI direkt auf grosse Sheets schauen lassen.

Besser:

> Pro Kunde eine kleine, kontrollierte Revenue-Datenarchitektur aufbauen: Raw Data, relationales Core Model, KPI Definitions, Weekly Snapshots und AI-ready Briefing Tables.

Die AI sollte moeglichst nie direkt grosse Rohdaten interpretieren. Sie sollte verdichtete, validierte und kundenkontextualisierte Tabellen bekommen.

## Grundprinzip

> Daten in Datenbank/Sheets/Warehouse. Logik in KPI Definitions und SQL/Transformations. AI bekommt nur die verdichtete Entscheidungsvorlage.

Damit reduzierst du:

- Tokenkosten,
- Fehlinterpretationen,
- Kontextlaerm,
- Datenschutzrisiken,
- manuelle Analysezeit,
- Abhaengigkeit von riesigen Spreadsheet-Exports.

## Empfohlene Architektur

### Layer 1: Source Systems

Typische Quellen:

- HubSpot oder anderes CRM
- Marketing Automation
- GA4
- Google Ads, LinkedIn Ads, Meta Ads
- Product Analytics
- Customer Support Tools
- Spreadsheets des Kunden
- manuelle Roadmap- und Hypothesen-Logs

### Layer 2: Ingestion

Moegliche Tools:

- Coupler.io
- Dataslayer
- native Exporte
- direkte APIs
- spaeter eigene Skripte oder ELT-Flows

Bewertung:

- Dataslayer ist gut fuer Marketingdaten direkt in Google Sheets.
- Coupler.io ist breiter, wenn Daten in Sheets, BI-Tools, Warehouses oder AI-nahe Workflows gebracht werden sollen.
- Fuer CRM-Relationen, insbesondere HubSpot Deals, Contacts, Companies und Associations, ist ein reiner Flat-File-Sheet-Ansatz schnell fragil.

Arbeitsthese:

> Coupler oder Dataslayer duerfen als Ingestion- und Staging-Layer dienen. Sie sollten aber nicht die eigentliche semantische Datenarchitektur ersetzen.

### Layer 3: Storage

Kurzfristig pragmatisch:

- Google Sheets als Staging und Review Layer
- ein Sheet pro Source/Export
- feste Namenskonventionen
- keine manuelle Bearbeitung in Raw Tabs

Besser fuer Skalierung:

- BigQuery als kleines Warehouse
- alternativ Postgres, wenn du lieber relational und app-nah arbeitest
- fuer lokale Einzelanalysen optional DuckDB, aber nicht als dauerhaftes Multi-Kunden-System

Empfehlung:

> Wenn du ohnehin im Google-Oekosystem mit Sheets, Looker Studio und Exporttools arbeitest, ist BigQuery wahrscheinlich der sauberste naechste Schritt.

Warum:

- Historie kann append-only gespeichert werden.
- Tabellen koennen partitioniert werden.
- Relationen lassen sich sauber modellieren.
- Views koennen AI-ready Briefing Tables erzeugen.
- Query-Kosten lassen sich durch Aggregation und Partitionierung begrenzen.

## Warum Sheets allein nicht reichen

Sheets sind gut fuer:

- schnelle Sichtpruefung,
- einfache Exporte,
- Kundenreview,
- manuelle Inputs,
- kleine KPI-Tabellen,
- MVP.

Sheets sind schlecht als dauerhaftes System of Record fuer:

- wachsende Historie,
- viele Kunden,
- komplexe Relationen,
- reproduzierbare Transformationen,
- saubere Versionierung,
- Berechtigungen,
- Performance,
- Kostenkontrolle beim AI-Kontext.

Kritische Regel:

> Sheets sind Interface, nicht Gehirn.

## KPI Definition pro Kunde

Jeder Kunde braucht eine eigene `KPI Definition`.

Diese Definition ist nicht nur Dokumentation. Sie ist der Vertrag zwischen Kunde, Datenmodell und AI.

Beispielstruktur:

```yaml
client_id: acme
kpis:
  - id: qualified_pipeline
    name: Qualified Pipeline
    business_question: How much qualified pipeline did marketing influence?
    owner: revenue_ops
    source_systems:
      - hubspot
    source_tables:
      - deals
      - deal_company_associations
      - deal_contact_associations
    grain: weekly
    calculation: sum(deal_amount) where deal_stage in qualified_stages and create_date in period
    filters:
      pipeline: new_business
      excluded_stages:
        - closed_lost
    leading_or_lagging: lagging
    interpretation_rules:
      - Compare against previous 4 weeks and same period last quarter if available.
      - Treat one large enterprise deal as potential outlier.
    caveats:
      - Amount quality depends on sales discipline.
      - Marketing influence requires association logic.
```

Diese Definition beantwortet:

- Welche KPI ist relevant?
- Warum ist sie relevant?
- Aus welchen Tabellen kommt sie?
- Wie wird sie berechnet?
- Welche Filter gelten?
- Welche Caveats muss AI kennen?
- Welche Interpretation ist erlaubt?

Ohne diese Definition wird AI raten.

## Historie ohne Datenhalde

Nicht jede Woche komplette Exporte in immer groessere Sheets kippen.

Besser:

### Raw Snapshots

Append-only Speicherung der Rohdaten, z.B.:

- `raw_hubspot_deals`
- `raw_hubspot_contacts`
- `raw_hubspot_companies`
- `raw_hubspot_associations`
- `raw_ads_campaigns`
- `raw_ga4_events`

Jeweils mit:

- `client_id`
- `source_system`
- `extracted_at`
- `source_updated_at`
- `record_id`
- Originalfeldern

### Core Model

Bereinigte Tabellen:

- `core_companies`
- `core_contacts`
- `core_deals`
- `core_activities`
- `core_campaigns`
- `core_accounts`
- `core_lifecycle_events`

### Association Tables

CRM-Relationen nicht in ein flaches Sheet pressen.

Stattdessen:

- `assoc_contact_company`
- `assoc_deal_contact`
- `assoc_deal_company`
- `assoc_ticket_company`
- `assoc_activity_contact`

Mit:

- `from_object_id`
- `to_object_id`
- `association_type`
- `association_label`
- `is_primary`
- `valid_from`
- `valid_to` falls historisiert

### KPI Snapshot Tables

Fuer AI und Weekly Reviews brauchst du nicht Rohdaten, sondern verdichtete Snapshots:

- `weekly_kpi_snapshot`
- `weekly_funnel_snapshot`
- `weekly_pipeline_snapshot`
- `weekly_roadmap_snapshot`
- `weekly_impact_contract_status`

Diese Tabellen sind klein und AI-ready.

## Relationen: Flat File vs. relationales Modell

HubSpot und aehnliche CRMs sind relational genug, dass ein reiner Flat-File-Ansatz gefaehrlich wird.

Beispiele:

- ein Deal kann mehrere Kontakte haben,
- ein Kontakt kann mehreren Unternehmen zugeordnet sein,
- ein Unternehmen kann mehrere Deals haben,
- Association Labels koennen Rollen wie Decision Maker, Billing Contact oder Primary Company beschreiben,
- Attribution und Marketing Influence haengen oft genau an diesen Beziehungen.

Wenn du das alles in ein flaches Sheet drueckst, bekommst du:

- Duplikate,
- falsche Summen,
- falsche Attribution,
- verlorene Beziehungskontexte,
- schwer erklaerbare Abweichungen.

Empfehlung:

> Raw darf flach exportiert werden. Core und AI-ready Models sollten relational gedacht werden.

## Tokenkosten und AI-Kontext

Das Tokenproblem loest du nicht durch ein anderes Exporttool.

Du loest es durch Architektur:

1. Rohdaten bleiben ausserhalb des LLM-Kontexts.
2. SQL oder deterministische Transformationen berechnen Kennzahlen.
3. AI bekommt nur:
   - KPI Definition
   - aktuelle Weekly Snapshots
   - Veraenderung zur Vorwoche
   - Veraenderung zum 4-Wochen-Schnitt
   - relevante Roadmap-Items
   - aktive Impact Contracts
   - offene Entscheidungen
4. AI erzeugt daraus den Weekly Brief.
5. Der fertige Brief wird gespeichert und nicht jedes Mal neu aus Rohdaten generiert.

Kritische Regel:

> Das LLM ist nicht dein Data Warehouse und nicht deine BI Engine.

## AI-ready Weekly Brief Table

Fuer jeden Kunden koennte jede Woche eine kompakte Tabelle erzeugt werden:

```text
client_id
week_start
kpi_id
kpi_name
current_value
previous_value
four_week_average
target_value
movement
movement_pct
status
interpretation_note
related_impact_contract_id
owner
```

Dazu eine kleine Kontextdatei:

```text
active_hypotheses
active_impact_contracts
roadmap_changes
blocked_items
decisions_needed
```

Das ist der Input fuer AI, nicht der komplette HubSpot-Export.

## Kundenspezifische Struktur

Pro Kunde:

```text
clients/
  acme/
    kpi_definitions.yml
    metric_caveats.md
    source_mapping.yml
    impact_contracts.yml
    weekly_briefs/
      2026-05-11.md
```

Im Warehouse:

```text
raw_acme_*
core_acme_*
mart_acme_weekly_*
```

Oder alternativ mit `client_id` in geteilten Tabellen:

```text
raw_hubspot_deals
core_deals
mart_weekly_kpis
```

Fuer den Anfang ist pro Kunde getrennt einfacher zu denken. Fuer Skalierung sind geteilte Tabellen mit `client_id` sauberer.

## Zugriff und Datenschutz

Kritische Empfehlung:

- Keine API Tokens ins Git-Repo.
- Keine sensiblen Rohdaten ins Git-Repo.
- Kundendaten nicht dauerhaft in Codex-Projektdateien speichern.
- In Git nur Definitionen, Schemas, Templates und anonymisierte Beispiele speichern.
- Kundendaten in Kunden-Sheets, BigQuery, Cloud Storage oder einem gesicherten Warehouse halten.
- Zugriff pro Kunde trennen.
- PII fuer AI-Briefings minimieren oder pseudonymisieren, wo moeglich.

Codex/GitHub ist gut fuer:

- Templates,
- Prompts,
- KPI Definition Schemas,
- Delivery-Dokumentation,
- anonymisierte Beispiele,
- interne Tools.

Codex/GitHub ist nicht der richtige Ort fuer:

- komplette CRM-Exports,
- personenbezogene Daten,
- Kundengeheimnisse,
- API Keys.

## MVP-Architektur

Wenn du schnell starten willst:

1. Pro Kunde ein Google Sheet als Staging.
2. Dataslayer/Coupler schreibt Rohdaten in feste Tabs.
3. Ein separates `KPI Definition` Sheet oder YAML definiert relevante KPIs.
4. Ein `Weekly Snapshot` Tab enthaelt nur verdichtete Kennzahlen.
5. AI bekommt nur:
   - KPI Definition,
   - Weekly Snapshot,
   - Roadmap Status,
   - Impact Contracts.
6. Weekly Brief wird als Markdown gespeichert.

Das ist gut fuer die ersten Kunden.

Aber:

> Sobald Relationen, Historie oder mehrere Kunden komplexer werden, solltest du auf BigQuery/Postgres wechseln.

## Zielarchitektur

1. Ingestion ueber Coupler, APIs oder Exporte.
2. Raw Data landet in Warehouse oder sauberem Staging.
3. Relationales Core Model stellt Kontakte, Unternehmen, Deals und Associations korrekt dar.
4. KPI Definitions definieren kundenspezifische Metriken.
5. SQL/Transformations erzeugen Weekly Snapshots.
6. AI liest nur Snapshots, KPI Definitions, Impact Contracts und Roadmap-Kontext.
7. Weekly Briefs werden gespeichert und versioniert.
8. Mario reviewed, korrigiert und nutzt den Brief fuer Accountability und Advisory.

## Entscheidungsempfehlung

Kurzfristig:

> Starte mit Google Sheets als Staging und Review-Layer, aber designe das System bereits so, als wuerde spaeter BigQuery/Postgres darunterliegen.

Mittelfristig:

> Baue BigQuery als zentrales, kosteneffizientes Revenue Data Mart auf.

Langfristig:

> Entwickle ein kleines internes Delivery OS, das KPI Definitions, Impact Contracts, Roadmap, Weekly Snapshots und AI Briefings verbindet.

## Wichtigste technische Design-Regeln

- Kundenspezifische KPI Definitions sind Pflicht.
- Raw Data und AI-Kontext strikt trennen.
- Historie append-only speichern, aber AI nur verdichtete Snapshots geben.
- CRM-Relationen als Association Tables modellieren.
- Weekly Briefs speichern, nicht jedes Mal neu aus Rohdaten generieren.
- Sheets als Interface nutzen, nicht als langfristiges Datenmodell.
- Keine Secrets oder Kundendaten ins Git-Repo.
- Erst Denkmodell und Tabellenstruktur stabilisieren, dann automatisieren.

## Quellen und technische Signale

- Coupler.io unterstuetzt Ziele wie Google Sheets, BigQuery, PostgreSQL, BI-Tools und AI-Integrationen; damit ist Coupler eher ein breiter Ingestion-/Automation-Layer als nur ein Sheet-Exporter. https://www.coupler.io/
- Dataslayer for Google Sheets ist stark fuer Marketingdaten und automatisierte Reports direkt in Google Sheets. https://www.dataslayer.ai/google-sheets
- HubSpot beschreibt CRM Associations als Beziehungen zwischen Records, z.B. Kontakte zu Unternehmen oder Deals zu Kontakten; die Associations APIs unterscheiden zwischen Details und Schema/Labels. https://developers.hubspot.com/docs/api-reference/latest/crm/associations/overview
- HubSpot Associations v4 unterstuetzt Association Labels und Beziehungen zwischen Kontakten, Unternehmen, Deals, Tickets und Custom Objects. https://developers.hubspot.com/docs/guides/api/crm/associations/associations-v4
- BigQuery External Tables koennen Daten aus externen Quellen wie Cloud Storage, Bigtable und Google Drive abfragen, auch Google Sheets ueber Drive. https://cloud.google.com/bigquery/docs/external-tables
- BigQuery Partitioned Tables helfen, Query-Performance und Kosten zu kontrollieren, weil nur passende Partitionen gescannt werden muessen. https://cloud.google.com/bigquery/docs/partitioned-tables
- BigQuery Materialized Views speichern vorab berechnete Query-Ergebnisse und koennen Rechenzeit und Query-Kosten reduzieren, wenn dieselben Aggregationen haeufig gebraucht werden. https://cloud.google.com/bigquery/docs/materialized-views-intro
