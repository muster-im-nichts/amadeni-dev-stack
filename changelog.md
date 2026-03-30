# Changelog

Woche für Woche dokumentiert, was sich am Dev Stack verändert hat.

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
