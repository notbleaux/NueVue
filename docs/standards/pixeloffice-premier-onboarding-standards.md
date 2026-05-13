# Premier Repository Onboarding Standards for PixelOffice AI Workspace

## Purpose

This standard defines premier-grade repository onboarding, scaffolding, and operating expectations for the PixelOffice ecosystem. It is designed to keep repositories professional, scalable, teachable, and ready for staged delivery from foundation to live operations.

PixelOffice combines practical software-development tooling with a manager-simulation interface where AI agents are represented by pixel sprites with visible roles, tasks, and progress states.

## Naming Alignment

- **Platform concept name:** PixelOffice
- **Repository/program name in this workspace:** NueVue
- **Operational command-center surface:** Nexus (web app module)

These names describe the same ecosystem from product, repository, and module viewpoints.

## Product Definition

PixelOffice is a website app service platform for learning, managing, and shipping software with AI agents through a professional workspace and lightweight simulation layer.

### Core Product Surfaces

- **Website:** Public landing, docs, onboarding, quickstart, product education, and showcase
- **Web app:** Authenticated workspace for planning, AI management, onboarding, task flow, metrics, and learning quests
- **Browser extension:** Contextual assistance, codebase navigation, enhancement overlays, and quick actions

## Design Philosophy

Pixel visuals must map directly to real delivery concepts and never reduce the workspace to a decorative toy.

### Experience Principles

- Personable, not childish
- Simulation as pedagogy
- Visible work across agent and project state
- Progressive complexity from guided onboarding to advanced operations
- Human authority over product decisions, releases, credentials, and irreversible actions

## Repository Portfolio Model

Use a multi-repository portfolio by default.

| Repository | Purpose | Primary owner | Stage |
|---|---|---|---|
| `pixeloffice-site` | Public website, docs, landing, changelog, marketing pages | Frontend/Web | Foundation |
| `pixeloffice-app` | Authenticated web app, dashboard, agent views, project management | Product App | Foundation |
| `pixeloffice-extension` | Browser extension companion, contextual overlays, quick actions | Extension | Alpha |
| `pixeloffice-api` | Backend API, auth, project services, agent state, integrations | Platform | Foundation |
| `pixeloffice-wiki` | ADRs, PRDs, CRIT reviews, standards, prompts, schemas | Product Ops | Recovery/Foundation |
| `pixeloffice-design-system` | Design tokens, sprite standards, UI components, motion rules | Design Platform | Foundation |
| `pixeloffice-infra` | Deployment, environments, secrets policy, monitoring, IaC | DevOps | Later Foundation |

### Alternative Early-Stage Monorepo

For a very small team, use one monorepo while preserving boundaries:

```text
pixeloffice/
├── apps/
│   ├── site/
│   ├── web/
│   └── extension/
├── services/
│   ├── api/
│   ├── agent-broker/
│   └── telemetry/
├── packages/
│   ├── ui/
│   ├── design-tokens/
│   ├── pixel-sprites/
│   ├── schemas/
│   ├── config/
│   └── testing/
├── docs/
├── adr/
├── prd/
├── crit/
├── prompts/
├── scripts/
├── .github/
└── README.md
```

## Premier-Grade Repository Outfit

Every production-intended repository should include at least:

```text
repo-root/
├── README.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── LICENSE
├── CHANGELOG.md
├── ROADMAP.md
├── .env.example
├── .gitignore
├── .editorconfig
├── .nvmrc
├── package.json
├── tsconfig.json
├── eslint.config.js
├── prettier.config.js
├── playwright.config.ts
├── vitest.config.ts
├── docs/
│   ├── onboarding/
│   ├── architecture/
│   ├── operations/
│   ├── testing/
│   └── release/
├── adr/
│   └── ADR-000-template.md
├── prd/
│   └── PRD-000-template.md
├── crit/
│   └── CRIT-000-template.md
├── prompts/
│   ├── claude-opus.md
│   ├── kimi.md
│   ├── sonnet.md
│   ├── deepseek.md
│   └── copilot.md
├── src/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── e2e/
│   └── accessibility/
├── scripts/
│   ├── setup.sh
│   ├── check.sh
│   ├── validate-env.sh
│   └── release.sh
└── .github/
    ├── ISSUE_TEMPLATE/
    ├── PULL_REQUEST_TEMPLATE.md
    ├── CODEOWNERS
    └── workflows/
        ├── ci.yml
        ├── security.yml
        ├── preview.yml
        └── release.yml
```

This baseline is Node.js/TypeScript-first. If additional runtimes are used, add equivalent runtime-version files and setup instructions (for example, Python, Ruby, or JVM tooling) in the same repository standard.

## Startup Quickstart Foundation

Target: a new developer reaches a working local environment in under one hour.

### Required Quickstart Flow

1. Clone repository
2. Install runtime versions
3. Copy `.env.example` to `.env.local`
4. Run setup command
5. Run checks
6. Start local development server
7. Open first guided task
8. Create first branch
9. Run tests
10. Open first PR

### README Must Include

- Product purpose
- Current development stage
- Repo ownership and CODEOWNERS
- Local setup
- Environment variables
- Development commands
- Test commands
- Architecture overview
- Project conventions
- Contribution process
- Agent usage policy
- Release process
- Support and escalation paths

### Prompt Files Policy

`prompts/` files define reusable role-aligned prompt baselines for supported model families. Repositories should document when each prompt is allowed, which role owns it, and where approval is required before changing production-facing prompts.

### Command Standard

```text
npm run setup
npm run dev
npm run build
npm run test
npm run test:e2e
npm run lint
npm run typecheck
npm run format
npm run check
```

`npm run check` is the single local confidence command before PR.

## Application Architecture Standards

### Website (Public Surface)

Sections should cover hero/promise, concept, visible agents, onboarding flow, simulation metaphor, quickstart, docs, roadmap, changelog, and security/privacy.

```text
apps/site/
├── src/
│   ├── app/
│   ├── components/
│   ├── content/
│   ├── docs/
│   ├── styles/
│   └── assets/
├── public/
├── tests/
└── README.md
```

### Web App (Operational Core)

```text
apps/web/
├── src/
│   ├── app/
│   ├── features/
│   │   ├── dashboard/
│   │   ├── agents/
│   │   ├── projects/
│   │   ├── tasks/
│   │   ├── codebase-onboarding/
│   │   ├── learning-quests/
│   │   ├── repo-health/
│   │   ├── releases/
│   │   └── settings/
│   ├── components/
│   ├── lib/
│   ├── styles/
│   └── routes/
├── tests/
└── README.md
```

### Browser Extension (Safe, Lightweight, Permission-Minimal)

```text
apps/extension/
├── src/
│   ├── manifest/
│   ├── popup/
│   ├── sidebar/
│   ├── content-scripts/
│   ├── background/
│   ├── options/
│   ├── lib/
│   └── styles/
├── tests/
│   ├── unit/
│   ├── extension/
│   └── e2e/
└── README.md
```

Extension rules:

- Request minimal permissions
- Do not manipulate sensitive internals without explicit review
- Keep overlays extension-controlled
- Make data collection visible and configurable
- Keep advanced overlays disabled until CRIT approval

## PixelOffice Agent Visualization System

### Agent Sprite Model

```text
Agent
├── id
├── display_name
├── vendor
├── model_family
├── role
├── permissions
├── current_task
├── current_state
├── confidence_state
├── cost_risk_tier
├── sprite_profile
└── handoff_protocol
```

### Sprite States

| State | Meaning | Example visual |
|---|---|---|
| Idle | Available for task | Standing/blinking |
| Reading | Inspecting files/context | Holding document |
| Planning | Creating plan or PRD | Whiteboard pose |
| Coding | Implementing changes | Typing animation |
| Testing | Running checks | Magnifier/tool pose |
| Blocked | Needs input | Paused motion/question mark |
| Reviewing | Validating work | Clipboard pose |
| Ready | Awaiting human action | Raised hand/highlighted desk |
| Error | Failed task or check | Alert frame/red pulse |

## Governance Rule

Documentation standards and architecture contracts must be updated in the same cycle as relevant service, API, or workflow behavior changes.
