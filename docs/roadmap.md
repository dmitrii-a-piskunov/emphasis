# Milestones / acceptance checklist

Codex: complete one milestone at a time, run checks, update checkboxes with evidence. Do not mark a milestone complete based only on generated code.

## M0 — Initialize project

- [ ] Create Vite React TypeScript app and lockfile (choose npm unless user directs otherwise).
- [ ] Configure Tailwind, shadcn/ui, Lucide, lint, formatter, test runner, strict TS.
- [ ] Configure PWA manifest, service worker, installable shell and offline fallback.
- [ ] `npm run dev`, `npm run build`, typecheck and tests work.

**Done when:** dev server starts, app shell opens without network after first load; CI passes.

## M1 — Local timer MVP

- [ ] Task picker works with fixture data before API hookup.
- [ ] One active timer per device, start/pause/resume/stop; clear UX states.
- [ ] Timestamp-based correct duration after reload, sleep/wake and tab backgrounding.
- [ ] IndexedDB persists completed sessions and active timer state.
- [ ] Session history view, edit/delete with confirmation, today/week totals.
- [ ] Export/import JSON including schema version, validation and duplicate handling.
- [ ] Unit tests for timer, rollover, timezone edge cases.

**Done when:** core tracking works fully offline after initial PWA install and persists across restart.

## M2 — Supabase and secure sync

- [ ] Configure Supabase Auth and sign-in/out flows.
- [ ] Add versioned database migration(s), RLS, indexes and server-side constraints.
- [ ] Test cross-user isolation; no service-role key in client bundle.
- [ ] Implement durable outbox, idempotent writes, recovery, conflict detection.
- [ ] Sync completed sessions across two browser profiles; visible sync state.
- [ ] Document first-time setup, backup, account deletion and recovery.

**Done when:** two devices reconcile sessions safely with intermittent offline connectivity.

## M3 — Todoist integration

- [ ] Verify current official API docs, credential strategy, and permissions/CORS.
- [ ] Implement secure authenticated Todoist gateway (or vetted alternative).
- [ ] Fetch active tasks and projects, support search/filter, cache for offline use.
- [ ] Handle token invalidation, rate limits, errors, no-task state and archived/completed task references in history.
- [ ] Do not modify Todoist task records in MVP.

**Done when:** live Todoist tasks can be selected and tracked without exposing credentials.

## M4 — Visual polish and analytics

- [ ] Todoist-inspired polished responsive light/dark design, not a pixel-level copy.
- [ ] Dashboard: today, week, task/project totals, activity chart, session list.
- [ ] Timezone-correct reporting including midnight boundaries and DST.
- [ ] Loading, errors, empty states, accessibility and keyboard support.
- [ ] Manual QA on Windows/macOS browser and Android/iOS PWA.

**Done when:** useable daily on desktop/mobile; reports match session data.

## M5 — Deployment

- [ ] Set up CI checks (lint, typecheck, test, build), protect secrets.
- [ ] Deploy to Cloudflare Pages free plan with HTTPS, SPA/PWA settings.
- [ ] Configure Supabase environment and redirect URLs; confirm RLS on production.
- [ ] Verify reinstall, offline/online reconnect, multi-device sync, JSON backup.
- [ ] Write maintenance and free-tier pause/quotas notes.

**Done when:** installation and syncing are tested on desktop and phone; no PC server required.
