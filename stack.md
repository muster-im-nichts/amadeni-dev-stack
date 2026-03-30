# Amadeni Dev Stack — Bestandsaufnahme

> Stand: 30. März 2026 · v0.3

---

## 1. Tech Stack

| Schicht | Technologie | Status |
|---------|------------|--------|
| **Frontend** | Next.js 15 (App Router) | ✅ Produktiv |
| **UI** | shadcn/ui + Tailwind CSS | ✅ Produktiv |
| **Backend** | Convex (BaaS) | ✅ Produktiv |
| **Auth** | Convex Auth | ✅ Produktiv |
| **Hosting** | Vercel (Frontend) + Convex Cloud (Backend) | ✅ Produktiv |
| **Monorepo** | Nein — ein Repo pro Projekt | ✅ Bewusste Entscheidung |

## 2. Shared Packages

| Package | Version | Zweck | Reifegrad |
|---------|---------|-------|-----------|
| `@amadeni/convex-lib` | 0.1.8 | Auth-Primitives, Capabilities, Permissions, Error-Handling, Zod-Helpers | 🟡 Aktiv entwickelt |
| `@amadeni/convex-e2e` | 0.1.4 | E2E-Test-Runner für Convex-Backends (config-driven) | 🟡 Aktiv entwickelt |
| `@amadeni/package-template` | 0.0.0 | Template für neue Packages (CI, TypeScript, Prettier, ESLint) | 🟢 Nutzbar |

## 3. Konventionen (AGENTS.md)

### Backend (Convex)

- **Module pro Domain-Entity**: `convex/clients/`, `convex/invoices/`, etc.
- **Datei-Split**: `queries.ts`, `mutations.ts`, `actions.ts`, `internal.ts`, `table.ts`, `helpers.ts`
- **Auth-Enforcement**: Alle öffentlichen Endpoints müssen Auth-Wrapper aus `@amadeni/convex-lib` nutzen
- **`@auth-bypass` Comment** für bewusst ungeschützte Endpoints
- **Keine Barrel-Exports** (`index.ts`) in Modul-Ordnern

### Frontend (React/Next.js)

- **Feature-Folders**: `src/features/invoices/components/`, `hooks/`, `lib/`
- **UI-Primitives**: `src/components/ui/` (shadcn-basiert, logikfrei, wiederverwendbar)
- **Shared Components**: `src/components/shared/` (app-spezifisch aber feature-übergreifend)
- **Ein Component pro Datei**, benannt nach dem Component

### Testing

- **Backend**: `@amadeni/convex-test` für E2E, Vitest für Unit-Tests
- **Frontend**: Vitest + Testing Library für Components, Playwright für Integration
- **Keine Snapshot-Tests** (brechen bei jeder visuellen Änderung, Agents verschwenden Zyklen damit)

## 4. Agent-Tooling

| Tool | Einsatz | Konfiguration |
|------|---------|---------------|
| **Claude Code** | Komplexe Multi-File-Arbeit, Plan-then-Execute | Pro flat rate, async via `claude-async.sh` |
| **Codex (GPT 5.4)** | Schnelle One-Shots, Reviews, Batch-Arbeit | `--yolo` für Repos unter `/home/claude-worker/repos/` |
| **Greptile** | Automatische PR-Reviews für Amadeni-Repos | GitHub Integration, unresolved Comments per GraphQL |
| **Echo (OpenClaw)** | Orchestrierung, Planning, Kommunikation | Opus 4, Heartbeat-basierter Wochenplan |

## 5. Git-Workflow

- **Amadeni-Repos**: Fork → Feature-Branch → PR → Greptile Review → Merge
- **Eigene Repos**: Direct Push auf `main`
- **Git-Identität**: `n-hallberg` für Amadeni, `echo-ex-void` für Muster-im-Nichts
- **Alle 4 ENV-Vars** setzen (Author + Committer Name + Email)

## 6. CI/CD

- **Vercel**: Auto-Deploy bei Push auf `main` (Preview bei PR)
- **Convex**: Auto-Deploy via `convex deploy` in Vercel Build
- **Package Publishing**: GitHub Actions bei Git Tags (`v*`)
- **Geplant**: Auth-Enforcement-CI-Check (grep für raw query/mutation imports)

---

## 7. Offene Baustellen

### Kurzfristig (diese/nächste Woche)
- [ ] Auth-Enforcement CI-Script schreiben und in Repos einbauen *(noch offen)*
- [ ] Backend-Refactoring: `api.ts` → `queries.ts` + `mutations.ts` Split *(impuls-kbb hat `testData/queries.ts`, aber kein vollständiger Split)*
- [ ] `docs/specs/` + `docs/plans/` Struktur in allen Amadeni-Repos anlegen *(noch offen)*
- [ ] AGENTS.md in fehlende Repos ausrollen: ki-at-obv, moritz-consulting, ama-hub, jos-ba, amadeni-ui, convex-e2e

### Offene PRs
- **agri-tools #45**: "Store contract and asset extraction results" — OPEN (Greptile: 3/5, 2 P1 Issues)
- **impuls-kbb #52**: "Add accounting dashboard detail dialogs" — OPEN (Greptile: 5/5, safe to merge)
- **impuls-kbb #46**: "Use convex lib over local primitive implementation" — OPEN
- **ki-at-obv #1**: "feat(admin): Add full admin page with user management" — OPEN
- **ki-at-obv #2**: "feat(ui): Sync components from moritz-consulting" — OPEN

### Mittelfristig
- [ ] `@amadeni/convex-lib` v0.2: Legacy-Aliases entfernen, Action-Ownership-Checks
- [ ] Frontend-Test-Coverage: Testing Library Setup in impuls-kbb
- [ ] Project-Scaffold-Template: `create-amadeni-app` Skill aktualisieren

### Langfristig / Vision
- [ ] Vollständig autonomer Projekt-Lifecycle: Scaffold → Develop → Test → Review → Deploy
- [ ] Selbst-optimierendes System: Agents erkennen Patterns und schlagen Conventions vor
- [ ] Shared Component Library als eigenes Package (`@amadeni/ui`?)

---

*Dieses Dokument wird wöchentlich aktualisiert. Änderungen werden in `changelog.md` dokumentiert.*
