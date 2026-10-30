# Emphasis

**A minimalist, local-first time tracker for Todoist.**

Emphasis is a personal project to make it easy to track time against Todoist tasks, review where your time goes, and keep your history available across devices. The goal is a polished, distraction-free progressive web app (PWA) that works offline and syncs when a connection returns.

> **Status: In development — specification-first repository.** The application is **not yet implemented or available to install**. The features below describe the product we plan to build, not features that are already working.

## Planned features

- **Todoist integration:** browse, search, and select tasks and projects without editing your Todoist data.
- **Simple time tracking:** start, pause, resume, and stop a session; preserve timer accuracy after a reload or device sleep.
- **Local-first experience:** keep tracking and reviewing locally stored sessions while offline.
- **Cross-device sync:** synchronize sessions through Supabase when online, with explicit sync status and conflict handling.
- **Useful insights:** see daily and weekly totals, task/project breakdowns, session history, and activity charts.
- **PWA support:** installable, responsive interface for desktop and mobile with light and dark themes.
- **Portable data:** export and import session history as JSON.

## Planned technology stack

| Area | Technology |
| --- | --- |
| Frontend | React, TypeScript, Vite |
| UI | Tailwind CSS, shadcn/ui, Lucide |
| Local persistence | IndexedDB (Dexie or equivalent) |
| Cloud persistence & authentication | Supabase (PostgreSQL, Auth, RLS) |
| Task source | Official Todoist API through an appropriately secured integration |
| Analytics | Recharts |
| Hosting | Cloudflare Pages |

The technology choices and security constraints are specified in the [technical specification](docs/tz.md) and [architecture notes](docs/architecture.md). Free-tier availability and integration details must be validated during implementation.

## Project status & roadmap

Development is organized into verifiable milestones:

| Stage | Scope |
| --- | --- |
| M0 | App foundation, developer tooling, installable PWA shell |
| M1 | Offline-first timer, local sessions, JSON import/export |
| M2 | Supabase authentication, database, secure sync |
| M3 | Todoist integration and offline task cache |
| M4 | Design polish, dashboards, accessibility, mobile QA |
| M5 | CI, production deployment, installation and sync verification |

See [docs/roadmap.md](docs/roadmap.md) for **the authoritative, up-to-date progress checklist**. No milestone is considered complete until its acceptance criteria have been verified.

## Getting started (developers)

**This repository currently contains documentation and setup files only.** There is no runnable React application or `package.json` yet. Milestone M0 will scaffold it; do not expect `npm install` or `npm run dev` to work before then.

1. Clone the repository and open it in VS Code.
2. Read [AGENTS.md](AGENTS.md), [docs/tz.md](docs/tz.md), and [docs/roadmap.md](docs/roadmap.md).
3. Use the [Codex onboarding prompt](docs/codex-start.md) to start with M0.
4. After M0 is complete, follow the newly documented installation and development commands here.
5. Supabase and Todoist credentials will be needed only for their respective integration milestones; use `.env.example` as a starting point and **never commit real secrets**.

## Documentation

- [Technical specification](docs/tz.md) (Russian) — product requirements and acceptance criteria.
- [Architecture](docs/architecture.md) — data model, offline sync, security, and key trade-offs.
- [Roadmap](docs/roadmap.md) — milestones and progress.
- [Project decisions](docs/decisions.md) — decisions and unresolved questions.
- [Codex quick start](docs/codex-start.md) — agent-oriented setup and initial task.
- [Agent instructions](AGENTS.md) — working conventions for coding agents.

## Security and privacy

Emphasis is designed to keep tracking data under the user's control. Credentials must never be committed to Git, exposed in client bundles, or stored in public documentation. Supabase access must be restricted with authentication and Row Level Security (RLS); Todoist credentials must be handled through a secure integration. Refer to [docs/architecture.md](docs/architecture.md) for the intended implementation.

## Contributing

The project is at an early, specification-first stage. If you would like to contribute, review the [specification](docs/tz.md), [roadmap](docs/roadmap.md), and [agent instructions](AGENTS.md) before proposing changes. Please don't present planned functionality as implemented.

## License

**No open-source license has been selected yet.** Public visibility does not, by itself, grant permission to reuse or redistribute the source code. A license may be added before general release.
