# Codex: first run

Open this repository folder in VS Code with the Codex extension. Make sure Git is initialized and the folder is trusted.

## Suggested first prompt (copy into Codex)

> Read `AGENTS.md`, `docs/tz.md`, `docs/architecture.md`, `docs/roadmap.md` and `docs/decisions.md` completely. Implement **M0 only**, keeping the existing documents. Use React + TypeScript + Vite, npm, Tailwind, shadcn/ui, Lucide, Vitest and a maintained Vite PWA plugin. Select currently compatible versions, generate real runnable project files, lint/typecheck/build/test scripts, and a minimal beautiful responsive app shell. Do not attempt Supabase deployment or Todoist integration yet. Run checks, document results and update `docs/roadmap.md` only for actually verified items. Do not ask for credentials.

Then implement M1, M2, M3, M4, M5 one by one. Review diffs and commit after each milestone. Read docs before every milestone and ask Codex to test critical paths.

## Required human actions later

- Create Supabase project, save project URL and public publishable key in local `.env.local` (never commit). Configure authentication and allowlist redirect URLs.
- Review all Supabase SQL and RLS before applying migrations; use Supabase secrets/Edge Function secrets for privileged values.
- Choose and securely provision Todoist authorization credentials after the gateway design is validated. Never paste personal API tokens into a public repo or chat history.
- Connect GitHub to Cloudflare Pages, set build command `npm run build`, output `dist`, configure client env vars and deploy only after reviewing.

## Workflow

Ask Codex: “Summarize files changed, what tests ran, what is still incomplete, and any security considerations.” Do not allow one broad request to implement all milestones at once.
