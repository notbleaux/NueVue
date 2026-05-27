# NueVue

NueVue is a **PixelOffice-inspired AI Agent Visualization Platform** designed to make software project planning and onboarding more intuitive.

It combines:
- a Web App,
- a Browser Extension,
- and a Website/Platform Service,

to simulate a manager-style experience where users can collaborate with AI agents, plan projects, and learn development workflows in a social, game-like environment.

## Product Naming (Canonical)

- **NeXeZ**: the website + authenticated web app experience (premium UI + visualization + command center).
- **NuMuN platform services**: API + orchestration + realtime activity backbone powering NeXeZ and other clients.
- **NueVue**: this repo/workspace program name (PixelOffice-inspired).

## Product Intent

NueVue provides a pixel-sprite assistant that helps users:
- understand repository structure,
- learn development-to-production workflows,
- coordinate planner-style project management with AI agents,
- and onboard into coding through guided, personable interactions.

## Premier Grade Process & Standards

The repository follows these baseline standards:
- **Single source of truth documentation** for onboarding, architecture, and startup flow.
- **Service separation by concern** (Web App, Extension, Website Platform).
- **Scaffold-first development** so startup teams can begin quickly and scale later.
- **AI interaction safety** via explicit role boundaries (Planner, Builder, Reviewer, Operator).
- **Incremental delivery** with minimal, testable, reversible changes.

## Platform Components

### 1) Web App
- PixelOffice-style dashboard for agent activity visualization.
- Planner and project management interface.
- Chat + multi-agent conferencing view.

### 2) Browser Extension
- Lightweight AI interaction panel for in-browser workflow support.
- Context bridge to connect page tasks with project boards.

### 3) Public Website and Docs Portal
- Public landing and product education.
- Documentation and onboarding entry point.
- Roadmap/changelog surface.

## AI Interaction Model

Core interaction roles:
- **Planner Agent**: breaks goals into milestones and tasks.
- **Builder Agent**: executes scoped implementation tasks.
- **Reviewer Agent**: validates quality, risks, and completion criteria.
- **Operator Agent**: handles deployment, runtime checks, and status.

## Onboarding Flow

1. Create workspace and select startup template.
2. Configure app surfaces (Web App, Extension, Platform Service).
3. Initialize planner board and first milestone.
4. Assign tasks to AI agent roles.
5. Run build/review/deploy loop with visible agent activity.

## Suggested Repository Scaffold (Startup & Quickstart)

```text
/
├── apps/
│   ├── web/                # Web App UI (pixel agent visualization + planner)
│   ├── extension/          # Browser extension client
│   └── website/            # Marketing/site shell and docs surface
├── services/
│   ├── api/                # Platform API (projects, users, orchestration)
│   ├── orchestration/      # Agent workflow engine and task routing
│   └── realtime/           # Presence/events/activity streams
├── packages/
│   ├── ui/                 # Shared components/design tokens
│   ├── agent-sdk/          # Shared AI agent integration client
│   └── config/             # Shared lint/build/ts/format configs
├── infra/                  # Deployment/IaC and environment setup
└── docs/
    ├── onboarding/         # New developer onboarding guides
    ├── standards/          # Engineering and release standards
    └── architecture/       # System architecture and diagrams
```

## Development Principles

- Keep changes small and composable.
- Prefer explicit contracts between services.
- Preserve clear separation between product UI and agent orchestration logic.
- Ensure onboarding docs evolve with architecture changes.

## Technical Specs and PRDs

Single source of truth:

- [`docs/specs/INDEX.md`](docs/specs/INDEX.md)
- [`docs/standards/pixeloffice-premier-onboarding-standards.md`](docs/standards/pixeloffice-premier-onboarding-standards.md)
- [`docs/standards/planning-and-decision-artifacts.md`](docs/standards/planning-and-decision-artifacts.md)
