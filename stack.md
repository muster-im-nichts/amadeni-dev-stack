# Amadeni Dev Stack — Bestandsaufnahme

> Stand: 4. Mai 2026 · v0.7

---

## 1. Tech Stack

| Schicht | Technologie | Status |
|---------|------------|--------|
| **Frontend** | Next.js 15 (App Router) | ✅ Produktiv |
| **UI** | shadcn/ui + Tailwind CSS | ✅ Produktiv |
| **Backend** | Convex (BaaS) | ✅ Produktiv |
| **Auth** | Convex Auth | ✅ Produktiv |
| **Hosting** | Vercel (Frontend) + Convex Cloud (Backend) | ✅ Produktiv |
| **Hosting (Self)** | Convex Self-Hosted (Mynd) | 🟡 Produktiv-Pilotbetrieb |
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
- [ ] Backend-Refactoring: `api.ts` → `queries.ts` + `mutations.ts` Split *(amadeni-crm hat noch `api.ts` Pattern, impuls-kbb teilweise)*
- [ ] `docs/specs/` + `docs/plans/` Struktur in allen Amadeni-Repos anlegen *(noch offen)*
- [ ] AGENTS.md in fehlende Repos ausrollen *(4/10 erledigt)*
- [ ] **amadeni-crm**: `@amadeni/convex-lib` integrieren (Auth-Wrapper, Permissions)
- [ ] **Mynd**: Patterns dokumentieren — neues Referenzprojekt für Convex Self-Hosted + Better Auth + Telegram-Bridge

### Offene PRs
- **agri-tools #72**: "Add asset registry feedback, admin workflows, and schema migrations" — OPEN (seit 28. Apr) — 6 Tage
- **impuls-kbb #80**: "Allow authorized edits on locked documentation" — OPEN (seit 28. Apr) — 6 Tage
- **ki-at-obv #1**: "feat(admin): Add full admin page with user management" — OPEN (seit 9. Feb!) ⚠️ **12+ Wochen** — sollte geschlossen werden
- **ki-at-obv #2**: "feat(ui): Sync components from moritz-consulting" — OPEN (seit 9. Feb!) ⚠️ **12+ Wochen** — sollte geschlossen werden

### Mittelfristig
- [ ] `@amadeni/convex-lib` v0.2: Legacy-Aliases entfernen, Action-Ownership-Checks
- [ ] Frontend-Test-Coverage: Testing Library Setup in impuls-kbb
- [ ] Project-Scaffold-Template: `create-amadeni-app` Skill aktualisieren
- [ ] Mynd-Patterns (Telegram Bot, Voice Tools, Image Upload) als wiederverwendbare Referenz extrahieren

### Langfristig / Vision
- [ ] Vollständig autonomer Projekt-Lifecycle: Scaffold → Develop → Test → Review → Deploy
- [ ] Selbst-optimierendes System: Agents erkennen Patterns und schlagen Conventions vor
- [ ] Shared Component Library als eigenes Package (`@amadeni/ui`?)
- [ ] Convex Self-Hosted als Standard-Deployment-Option neben Convex Cloud

---

*Dieses Dokument wird wöchentlich aktualisiert. Änderungen werden in `changelog.md` dokumentiert.*
