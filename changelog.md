# Changelog

Woche für Woche dokumentiert, was sich am Dev Stack verändert hat.

---

## KW 17 (21.–27. April 2026) — Billing-Offensive & Factorial-Cockpit

**impuls-kbb (10 gemergte PRs! #70–#79):**
- 🔍 **Factorial Sync Overhaul**: Relink-Suche (#70, #71), Status-Cockpit (#72), Retry & Auto-Link Actions (#74) — Factorial-Integration massiv stabilisiert und sichtbarer gemacht
- 💶 **Yearly Flat Billing** (#73): Jahrespauschalen als neues Abrechnungsmodell
- 🧾 **Invoice Catalog Items** (#77): Abrechnungskatalog-Items direkt auf Rechnungen
- 📎 **Proof & Attribution** (#75, #76): Nachweisdokumente an Services & Rechnungen
- 🏷️ **Multi-Program Billing** (#78): Mehrere Programme pro Abrechnung + Korrekturentwürfe
- ✅ **Proof Status vereinfacht** (#79): Übersichtlichere Nachweiszählung
- ❌ **Echo-PRs #66, #67, #69 geschlossen** — Nicos Richtung: Factorial-Sync verbessern statt durch native Time Entries ersetzen

**agri-tools (2 gemergte PRs #68, #69):**
- 💰 **CashFlow Pagination** (#68): Paginierte Vorschläge + gefilterte Dokumente
- 📊 **VAT State Drilldown** (#69): Detaillierte Steuer-Status-Panels
- 📋 **PR #67** (VAT transaction drill-down): Weiterhin OPEN (10 Tage)

**amadeni-crm:** Keine Aktivität.

**AGENTS.md-Rollout:** 4/10 — amadeni-crm hat jetzt AGENTS.md! (neu seit letzter Woche)

**Package-Versionen:** Unverändert (`convex-lib` 0.1.8, `convex-e2e` 0.1.4)

**Beobachtungen:**
- impuls-kbb hatte eine **Mega-Woche** mit 10 gemergten PRs — Billing-System wird richtig erwachsen
- Nico hat entschieden: Factorial bleibt, wird aber besser gemanagt (Cockpit, Retry, Relink). Die native-Time-Entries-Richtung ist vom Tisch
- agri-tools VAT/CashFlow-Bereich reift weiter
- ki-at-obv PRs jetzt **11 Wochen** offen — wird langsam zum toten Code
- AGENTS.md-Fortschritt: amadeni-crm war Neuzugang, noch 6 Repos offen

**Empfehlung:**
1. ki-at-obv PRs #1/#2: Nach 11 Wochen sollten sie geschlossen werden — Code ist vermutlich veraltet
2. agri-tools PR #67: Noch relevant? 10 Tage ohne Review
3. impuls-kbb Billing-Features testen lassen — viel Neues in kurzer Zeit

---

## KW 16 (13.–20. April 2026) — Mega-Sprint: KMZ-Maps, VAT, Billing, Factorial-Ablösung

**agri-tools (65+ Commits!):**
- 🗺️ **KMZ Boundary Maps**: Vollständige Kartenintegration — KMZ-Upload mit Feature-Auswahl, Mixed-Geometry-Support, Basemap-Fehlerbehandlung, Zuordnung auf Objekten und Flurstücken
- 📝 **Field Notes**: Neues Feature — Feldnotizen auf Objektformularen mit Status-Aggregation, Thread-Aktionen, Sync und Document-Ref-Verknüpfung
- 💰 **VAT Settlement**: Umfangreiche Überarbeitung — Scope-Berechnungen, Validierung auf Rechnungszeilen, partielle Abrechnung, Vorzeichennormalisierung
- 🏢 **Company Management**: Firmen-Archivierung für gemergte Datensätze, Eigentumsverhältnisse und gewichtete Konsolidierung
- 📊 **Investments & Operations**: Asset-verknüpfter Investment-Lifecycle, Operations-Management-Module, Parcel-Sale-Workflow
- 🔒 **Auth**: Diagnostics-Endpoint und Cookie-Flow-Fix
- 📋 **PR #67** (VAT transaction drill-down): OPEN

**impuls-kbb (35+ Commits!):**
- ⏱️ **Native Convex Time Entries (PR #69)**: Strategisch — Zeiterfassung von Factorial nach Convex verlagern! Ersetzt externe Abhängigkeit durch eigenes Domain-Modul
- 💶 **Billing Overhaul**: Abrechnungskatalog mit Stundensätzen, Merge-Workflow, Template-basierte Service-Erstellung, konfigurierbare Default-Stundensätze
- 🧾 **Invoice PDF Refresh**: Neues Template, Branding-Felder, Organisation/Settings aufgetrennt
- 🔄 **Factorial Sync**: Relinking, Operation-Tracing, sichere Refetches — parallel zur Ablösung nochmal stabilisiert
- 📋 **PRs #66, #67, #69**: OPEN (3 aktive PRs!)

**Beobachtungen:**
- Extrem aktive Woche in beiden Haupt-Repos — Nico baut massiv Features
- agri-tools bekommt eine richtige GIS-Komponente (KMZ-Maps!) — neues Terrain
- impuls-kbb PR #69 ist ein architektureller Meilenstein: Factorial als externe Abhängigkeit wird optional/ersetzbar
- ki-at-obv PRs jetzt **10 Wochen** offen — brauchen dringend Entscheidung (mergen, schließen, oder überarbeiten?)
- amadeni-crm: Weiterhin keine Aktivität seit Erstellung
- Package-Versionen: Unverändert (`convex-lib` 0.1.8, `convex-e2e` 0.1.4)
- AGENTS.md-Rollout: Weiterhin 3/10

**Empfehlung:**
1. ki-at-obv PRs #1 und #2 — nach 10 Wochen sollte Nico entscheiden: Merge, Close, oder Rebase?
2. impuls-kbb hat 3 offene PRs zum selben Themenfeld (Factorial) — Review-Priorisierung sinnvoll
3. amadeni-crm wäre ein guter Kandidat für AGENTS.md + `@amadeni/convex-lib` Integration als nächstes

---

## KW 15 (6. April 2026) — Neues Repo: amadeni-crm, aktive Merge-Woche

**Neues Repo: amadeni-crm**
- Next.js 16 + Convex 1.34 + shadcn/ui + Zod 4 — neuester Stack!
- Domain-Module: contacts, companies, offers, tags, statuses, timeline
- Business-Card-Scanner mit AI-Extraktion (`convex/contacts/scan.ts`)
- Many-to-Many: `contact_companies` Join-Table
- ⚠️ Nutzt **nicht** `@amadeni/convex-lib` — rohe Convex query/mutation statt Auth-Wrapper
- ⚠️ Backend-Dateien heißen `api.ts` statt queries/mutations Split
- ⚠️ AGENTS.md fehlt (nur Next.js auto-generated Rules)

**Gemergte PRs:**
- **agri-tools #47** "Asset-prefill" — MERGED (31. März)
- **agri-tools #48** "Asset prefill 2" — MERGED (2. April)
- **impuls-kbb #57** "Enhance program assignment dialog workflow" — MERGED (31. März)
- **impuls-kbb #58** "Upload resync" — MERGED (2. April)
- **impuls-kbb #59** "Documentation reassign" — MERGED (2. April)

**Geschlossene PRs:**
- **agri-tools #45** (ersetzt durch #47/#48)
- **impuls-kbb #55, #56** (ersetzt durch #57)

**Package-Versionen:** Unverändert (`convex-lib` 0.1.8, `convex-e2e` 0.1.4)

**AGENTS.md-Rollout:** 3/10 (agri-tools, impuls-kbb, convex-lib) — amadeni-crm als neues Ziel

**Einschätzung:**
Sehr aktive Woche! Amadeni-crm ist ein frisches Projekt — guter Moment, Konventionen von Anfang an richtig einzuführen. Die asset-prefill Story in agri-tools ist abgeschlossen (P1-Issues aus #45 offenbar adressiert). impuls-kbb bekommt regelmäßig PRs. ki-at-obv PRs sind jetzt seit fast 2 Monaten offen — könnte Review brauchen.

---

## KW 14 (30. März 2026) — Zwei große PRs, aktive Feature-Arbeit

**Neue PRs:**
- **agri-tools #45** — "Store contract and asset extraction results" (+3818/-102)
  - Neues `entityExtractions` Domain-Modul (Tabelle, Mutations, Queries)
  - `assetPrefill` Domain für OCR-basierte Asset-Extraktion (Mistral OCR)
  - Greptile Score: 3/5 — zwei P1 Issues offen:
    1. Reapply-Buttons nach Stored-Extraction sind no-ops (fehlende Prefill-Daten)
    2. `upsertExtraction` Lookup ohne `objectId`-Scope → Cross-Object-Overwrite möglich
  - Pattern: Shared `LightweightDocumentRefValidator` eingeführt (Loans + Valuations refactored)
- **impuls-kbb #52** — "Add accounting dashboard detail dialogs" (+1043/-51)
  - Drill-down Detail-Layer für Accounting Dashboard
  - Neues `getAccountingOpenItemDetails` authQuery
  - 4 Detail-Panel-Components + Shared Dialog
  - Greptile Score: 5/5 — safe to merge
  - Greptile P2: Duplizierter `AccountingOpenItemType` → `shared.ts` eingeführt

**Package-Versionen:** Unverändert (`convex-lib` 0.1.8, `convex-e2e` 0.1.4)

**AGENTS.md-Rollout:** Weiterhin 3/9 (agri-tools, impuls-kbb, convex-lib)

**Offene Baustellen (unverändert):**
- Auth-Enforcement CI, api.ts-Split, docs-Struktur — noch offen
- AGENTS.md-Rollout in 6 Repos ausstehend

**Einschätzung:**
Aktive Woche mit Feature-Arbeit in den Kunden-Repos. agri-tools #45 zeigt ein interessantes neues Pattern (entityExtractions als persistente OCR-Layer). impuls-kbb #52 ist sauber genug zum Mergen. Die kurzfristigen Infrastruktur-Baustellen bleiben auf der Wartebank.

---

## KW 13 (23. März 2026) — Stille Woche, Bestandsaufnahme v0.2

**Beobachtungen:**
- Keine neuen Commits in Amadeni-Repos seit KW 12
- Package-Versionen unverändert: `convex-lib` 0.1.8, `convex-e2e` 0.1.4
- 3 PRs weiterhin offen (impuls-kbb #46, ki-at-obv #1 + #2)
- AGENTS.md nur in 3/9 Repos vorhanden (impuls-kbb, agri-tools, convex-lib)
- Kurzfrist-Baustellen (Auth-CI, api.ts-Split, docs-Struktur) noch unberührt

**Aktualisiert:**
- `stack.md` v0.2: Offene PRs dokumentiert, AGENTS.md-Rollout als neue Baustelle
- Tracking welche Repos AGENTS.md haben und welche nicht

**Einschätzung:**
Ruhige Woche — vermutlich Kundenprojekte im Fokus. Die kurzfristigen Baustellen schieben sich. AGENTS.md-Rollout wäre ein guter low-effort Einstieg um Konventionen zu verbreiten.

---

## KW 12 (16. März 2026) — Initiale Bestandsaufnahme

**Erstellt:**
- `stack.md` — Erste vollständige Dokumentation des Amadeni Dev Stacks
- Backend- und Frontend-Konventionen für AGENTS.md definiert
- Test-Regime festgelegt (E2E + Unit + Component, keine Snapshots)
- Dev-Skill erweitert: Codex-Integration mit `--yolo`, Agent-Selection-Logik
- Heartbeat-basierter Wochenplan statt täglicher Cron-Jobs

**Kontext:**
- `@amadeni/convex-lib` bei v0.1.8, Refactoring-PR #2 offen
- `@amadeni/convex-e2e` bei v0.1.4
- Konventionen existieren als Ideen, aber noch nicht in allen Repos als AGENTS.md
