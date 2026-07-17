# Changelog – ams.identityaccess

All notable changes to this product are documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

ams.identityaccess is the standalone identity provider for the ams products
(IdentityServer, AdminPortal, ClientHub, EmailSender).

## [3.3.2] – 2026-07-17

### Fixed
- **The session-lifetime fix now also applies to the normal login flow.** The
  `refresh_expires_in` emission added in 3.3.1 was gated on `offline_access` appearing
  in the requested scopes. IdentityServer4 does not surface that scope there, so the
  **authorization_code login flow** never received the hint and the BFF session still
  expired after ~1 hour. `refresh_expires_in` is now emitted for the
  **authorization_code** and **refresh_token** grants, guarded by the client's
  `AllowOfflineAccess` setting.
  **Effect:** signed-in users stay logged in for as long as their refresh token is valid
  (days instead of ~1 hour) — including via the regular sign-in flow.

## [3.3.1] – 2026-07-16

### Fixed
- **The BFF session now outlives the access-token lifetime.** Unlike Keycloak,
  IdentityServer4 does not report the refresh-token lifetime in its token response.
  The Web BFF uses that value to size its server-side token-vault TTL; without it the TTL
  collapsed to the short access-token lifetime, so the session died ~1 hour after login
  even though the refresh token was valid for days. A new `ICustomTokenRequestValidator`
  appends a Keycloak-compatible `refresh_expires_in` (derived from the client's configured
  refresh-token lifetime) whenever a refresh token is issued. Token-exchange responses are
  left unchanged.

## [3.3.0] – 2026-07-02

### Changed
- **IdentityAccess now runs self-contained in a single database by default.** The separate
  NServiceBus transport database has become **optional**. New variable
  **`DB_TRANSPORT_NAME` (optional)**:
  - **leave blank** → IdentityAccess uses its persistence database (`DB_NAME`) for queues
    and subscriptions as well (recommended for standalone operation);
  - **set** → only the shared `dbo.SubscriptionRouting` table lives in the transport
    catalog — for cross-context pub/sub (e.g. together with the ams.project stack).
- **Unified subscription-routing placement.** Migrator and runtime address
  `dbo.SubscriptionRouting` identically; the table is created **idempotently** in the
  correct catalog — by IdentityAccess or the platform stack, whichever runs first. No more
  orphaned duplicate tables.
- **`SERVICE_BUS_CATALOG` is gone.** The subscription catalog is now derived from
  `DB_TRANSPORT_NAME` (a single source of truth).

### Fixed
- **Cross-context pub/sub in the rc channel restored.** The host services read the catalog
  from `SERVICE_BUS_CATALOG`, but the rc deployment provided `DB_TRANSPORT_NAME` — leaving
  the catalog empty at runtime, so `SubscriptionRouting` fell back to each service's own
  database and pub/sub silently broke.
- **Missing grant added:** the runtime user now reliably receives `dbo.error` on the
  persistence database (previously a latent gap).
- Removed dead/duplicate transport queue tables and the orphaned default
  `IdentityAccess.SubscriptionRouting` table.

### Operator note
- Existing standalone deployments are unaffected (self-contained). If you previously set
  `SERVICE_BUS_CATALOG`, switch to `DB_TRANSPORT_NAME`.

## [3.2.0] – 2026-05-11

- Initial release of IdentityAccess as a standalone RSGO product
  (IdentityServer, AdminPortal, ClientHub, EmailSender). Earlier history is not
  captured in this changelog.
