# Secrets handling

Never commit real credentials. Copy `apps/api/.env.example` to `apps/api/.env` for the backend.

Client config (injected at build time):
- Android: set `SENTRY_DSN`, `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `MAPS_API_KEY` in `~/.gradle/gradle.properties` or pass with `-P`.
- iOS: create git-ignored `iosApp/Configuration/Secrets.xcconfig` with the same variables (Info.plist reads `$(VAR)`).
- Backend-only secrets (`SUPABASE_JWT_SECRET`, `SUPABASE_SERVICE_ROLE_KEY`, DB URLs) must never be in client files.
- `apps/api/task-def.json` uses `${VAR}` placeholders; substitute in CI.

## Rotate after merge (values remain in git history)
Supabase JWT secret and service-role key, Supabase anon key, Google Maps key (restrict by bundle ID/package + API), Sentry DSNs, staging DB credentials. Then purge history if desired and invalidate sessions.
