**Live `/health` failed three consecutive probes from GitHub at {{WHEN}}.**

Probed: `{{URL}}`
Last response: `{{DETAIL}}`

This is the external safety net (GL-15). It lives outside Supabase on purpose: if the Live Supabase project, its edge runtime or its database is down, the internal uptime probe cannot say so — this can.

**What to check, in order**
1. https://status.supabase.com — is it a platform incident?
2. Live project dashboard (`iejmitonpgmchfpzvqtm`): project paused? database unreachable? edge functions failing to boot?
3. Open https://pos.cibus.app and https://hi.cibus.app — are the apps themselves up? (static hosting is separate from Supabase)
4. Runbook: `docs/ops/observability.md` in Cibus-6-0.

This issue is sticky: later failed runs comment here instead of opening a new one, and the first healthy run closes it with a recovery note. Run: {{RUN_URL}}
