# Changelog

Woche für Woche dokumentiert, was sich am Dev Stack verändert hat.

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
