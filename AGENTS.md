# Instructions for coding agents — Emphasis

Read **docs/tz.md**, **docs/architecture.md**, **docs/roadmap.md**, and **docs/decisions.md** before changing code. These documents are the source of truth. The repository starts as a specification-first scaffold; implement the app in small verified increments.

## Working agreement

1. Start each task with a short plan and note assumptions. Work autonomously on clearly specified items; ask only when a choice changes product scope, cost, credentials, or security model.
2. Work through `docs/roadmap.md` in order. Make minimal, coherent changes; update checkboxes only after verification. Keep documentation aligned with implementation, including the public-facing README.
3. Run available formatter, lint, typecheck and tests after each milestone. Report commands and results honestly; do not claim tests passed if not run.
4. No secrets in repository, logs, client bundles, tests or screenshots. Never expose Supabase secret/service_role keys or Todoist personal tokens in browser code. Do not bypass RLS.
5. Confirm Todoist API endpoints and Supabase/Cloudflare configuration against current official documentation before implementation. Do not invent endpoint paths or assume browser CORS support.
6. Prefer React + TypeScript + Vite, Tailwind, shadcn/ui, Lucide, Recharts, Dexie/IndexedDB, Supabase JS; avoid unnecessary dependencies.
7. Use strict TypeScript, explicit validation of external payloads, accessible UI, reliable loading/empty/error states and responsive layout.
8. Timer correctness is essential: use timestamps and accumulated durations, not interval ticks as the source of truth; test pause/resume, reload, sleep/wake, time zones and clock changes.
9. Local-first: writes succeed locally first, use durable outbox, idempotent cloud writes, stable UUIDs and per-user RLS; do not silently discard conflicts or records.
10. Auth and RLS must be completed and tested before exposing cloud functionality. For a single-user app, still segregate data by authenticated `user_id`.
11. Avoid scope creep: no team mode, billing, mobile-native wrapper, always-on background tracking or multi-provider sync in MVP.
12. Never deploy, run destructive migrations, make paid purchases, or modify production data without explicit user approval.

## Public README maintenance (required)

- Treat `README.md` as the public project landing page, written in clear English; preserve links to the Russian technical specification.
- For every milestone or user-visible change, assess whether the README needs updating **in the same task/PR**. Update it whenever features, actual project status, setup commands, prerequisites, environment variables, screenshots, deployment steps, or security guidance change.
- Distinguish **implemented and verified** behavior from **planned** behavior. Do not imply that a feature, deployment, platform compatibility, or test is working until verified. Keep the roadmap checklist as the detailed source of progress; reflect meaningful changes briefly in the README.
- Once M0 creates a runnable app, replace the scaffold-only getting-started note with **tested** commands for install, development, lint, typecheck, test, and build, as available. Keep commands accurate as the project evolves.
- Never add tokens, keys, personal data, real `.env` contents, private URLs, or sensitive screenshots to README; show only safe placeholders. Do not add unverified badges, promotional claims, or a license that has not been explicitly chosen.
- At the end of each task, report whether README was changed and why (or why it did not need a change).

## Deliverables per milestone

- Working code with clear run commands and `.env.example` updates.
- Tests for new critical behavior.
- Brief documentation of decisions/trade-offs.
- Progress updated in `docs/roadmap.md` and public-facing `README.md` updated when relevant.

## Stop and flag

Stop before implementing if API restrictions make the agreed secure authentication flow impossible, if an operation needs a secret in the browser, or if free-tier availability is materially different from assumptions. Propose alternatives with costs/tradeoffs.
