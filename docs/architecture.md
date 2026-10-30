# Architecture and engineering constraints

## Components

1. **PWA (Cloudflare Pages):** React/TypeScript/Vite, service worker/app shell cache, installable UI.
2. **Local data (IndexedDB / Dexie):** cached task/project snapshots, local time sessions, pending mutations/outbox, sync cursor/metadata, application preferences.
3. **Supabase:** Auth, PostgreSQL tables, RLS policies; per-user sessions and device metadata; authenticated Edge Function for Todoist gateway if secure credential handling can be implemented.
4. **Todoist official API:** active tasks and projects. Treat Todoist as canonical for task names/status, not time history.

## Data entities (logical)

- `time_sessions`: `id uuid`, `user_id uuid`, `todoist_task_id text`, `todoist_project_id text nullable`, `task_title_snapshot text`, `started_at timestamptz`, `ended_at timestamptz`, `duration_ms bigint`, `note text nullable`, `created_at timestamptz`, `updated_at timestamptz`, `deleted_at timestamptz nullable`, `revision integer`.
- `active_timer` locally: `task_id`, `session_id`, `started_at` (wall time), `accumulated_ms`, `running_since` nullable, `state` (running/paused), `device_id`. On device restart, reconcile based on timestamps; avoid double-running timers across devices.
- `sync_outbox`: `event_id uuid`, `entity_id`, `operation`, `payload`, `created_at`, `attempts`, `last_error`.
- cached `todoist_tasks`, `todoist_projects`: local snapshot with `fetched_at`; offline and stale states visibly marked.

Store all timestamps as ISO UTC / timestamptz; display user local time. Track duration in milliseconds, do not derive historical session duration from calendar-day difference. Daily summaries split sessions across local day boundaries using the user's selected timezone. Choose and document DST policy.

## Sync strategy

- Persist session changes to IndexedDB first, atomically with outbox entries.
- Send mutations when authenticated and online, retry with exponential backoff, deduplicate by immutable UUID.
- Download remote changes on app open, on reconnect, and periodically while visible; provide manual sync status/retry.
- No blind last-write-wins overwrites on concurrent edits. Use server-side version/revision checks (optimistic concurrency) and conflict UI or explicit deterministic merge rules.
- Deletion should use tombstones (`deleted_at`), not irreversible immediate deletion, to propagate across devices.
- A running timer is **device-local in MVP**. Other devices can display last-synced completed sessions, but cannot control or rely on a concurrently running timer. Show a warning when another device has a recent active timer if optional presence is implemented.
- Do not promise background sync when app is closed or offline; mobile browsers restrict it.

## Security

- Supabase Auth required for cloud features. Configure row-level security for all user-owned tables: authenticated user can only access rows whose `user_id = auth.uid()`.
- Publishable/anon key is client-visible by design; secret/service-role key must be server-side only.
- Todoist credential handling requires design validation before implementation. Option: official OAuth (if appropriate for the deployment) or server-side per-user token in encrypted storage with access restricted to authenticated functions. Never embed personal tokens in Vite environment variables, localStorage, IndexedDB, source or browser requests to unauthorized origins.
- Proxy must validate JWTs, rate-limit and restrict outbound API calls; no arbitrary URL proxy. Guard against token leaks in logs/error responses. Apply reasonable CSP and secure headers.
- Only request minimum privileges, ensure sign-out clears sensitive local cache (or isolates it per user), and document user data deletion/export.
- Free hosting is **not** a guaranteed SLA. Ensure offline time logs survive outages and give clear recovery instructions.

## Deploy

- Cloudflare Pages builds static site (`npm run build`, output `dist`), with HTTPS, SPA fallback as required.
- Supabase migration SQL is version controlled in `supabase/migrations/`; deployments must be explicitly approved.
- Env example exposes only non-secret client values; server secrets belong in the host's secret store.
- Verify real current limits/prices and API behaviors against official docs rather than assuming permanent free tiers.

## Quality gates

- Strict types, lint/format, automated unit tests for timer/timezone behavior, RLS policy tests, smoke test on desktop Chrome + Android Chrome + iOS Safari/Home Screen PWA.
- Keyboard navigable, accessible labels, light/dark themes, respectful motion, responsive mobile UI.
