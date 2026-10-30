# Architecture decision record (initial)

## Confirmed

- Personal, single-user Todoist time tracker with polished Todoist-inspired (not copied) design.
- Installable PWA for desktop and mobile, including Windows/macOS/Android/iOS.
- Local-first sessions with offline operation; IndexedDB as local storage.
- Supabase hosted PostgreSQL + Auth + RLS for cross-device synchronization; no always-on personal server.
- Cloudflare Pages as preferred static PWA hosting; free tiers preferred.
- Todoist used as **read-only** source of tasks/projects for MVP. Time logs are not written into Todoist.
- User owns/exportable data: JSON export/import; backups.
- React, TypeScript, Vite, Tailwind, shadcn/ui, Lucide, Recharts; simple maintainable architecture.

## Assumptions to validate in implementation

- Todoist personal-token handling: a token cannot be shipped in PWA source or localStorage. Preferred solution: authenticated server-side proxy (Supabase Edge Function) with encrypted per-user credential storage or another secure official OAuth strategy, if feasible. Implementation must validate security and current API usage; a one-time setup/secret entry path may be required. **Never put Todoist token in public Supabase table as plaintext or send it to other users.**
- On free Supabase tier, projects can have inactivity pauses and quotas; check current terms before deployment.
- Automatic background sync while PWA is closed is not guaranteed on iOS/Android; guarantee synchronization when the app is open and online, with manual retry.
- Offline task list is a cached snapshot and can be stale; time tracking should still work.

## Deferred

- Tauri desktop wrapper, tray integration, global shortcuts, widget, Pomodoro, teams, invoicing, push notifications, calendar integration.
- Full syncing Todoist tasks themselves into Supabase; cache locally instead unless needed.
- Custom domain, paid infrastructure, multiple accounts per user.
