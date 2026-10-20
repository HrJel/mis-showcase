# MIS — Security, operations and release runbook

> Public reference, last reviewed 2026-10-20. **Not a certificate of production readiness or a penetration-test report.** The current Cloudflare deployment is documentation, while the prepared identity Worker still requires complete configuration and release tests.

## A. Sensitive data inventory

Employee identities, schedules, HR requests, leave records, roles, tickets and potentially highly sensitive payroll/finance information.

**Current showcase rule:** use only synthetic content. No original client personnel, mail, financial, credentials or unapproved proprietary assets are to be committed. Review legal ownership/licensing and any NDA separately.

## B. Authentication and user lifecycle

The independently authored Pages Worker foundation (where published/deployed) provides **planned operational shape**, not a guaranteed live account system:

1. Client obtains Cloudflare Turnstile token from a widget registered to the exact site hostname.
2. `POST /api/login` validates origin, rate limits, invokes Cloudflare Siteverify using the **encrypted** `TURNSTILE_SECRET` and checks `success`, hostname and action.
3. Server verifies admin secret or D1-stored salted password hash, creates a random opaque session token and stores only its SHA-256 hash in `auth_sessions`.
4. Cookie `__Host-jelvan_session` is `Secure; HttpOnly; SameSite=None; Partitioned`; expiry eight hours. Cookie behavior in third-party frames requires testing; do not treat an iframe as an authentication boundary.
5. Each protected request validates the D1 session and user disabled status; logout revokes the session.
6. Admin route creates/disables scoped users, but **does not substitute** for business/domain-specific authorization, MFA, reset, passkeys, SSO, recovery or enterprise RBAC.

`ADMIN_USERNAME` and `ADMIN_PASSWORD` must be set **as encrypted Cloudflare production secrets per Pages project**, never in code. Passwords must be at least twelve characters for current worker startup; use unique 16+ character randomly generated passwords before exposure to public internet. Never use a known weak sample password. Do not include secret values in issues, pull requests, screenshots, test fixtures, code or documentation.

### Cloudflare resource inventory

- Cloudflare account: `Portfolio Apps - Jelvan`.
- Pages project: `mis-showcase`.
- Pages Turnstile site key is a public variable; Turnstile **secret** is encrypted.
- D1 binding: `AUTH_DB` (shared auth database); tables `app_users`, `auth_sessions`, `auth_attempts`, `app_workspace`.
- These resources were **provisioned**; their existence does not mean application login is deployed, tested, or production-ready.

### APIs to test after staging deployment

| Route | Required test |
| --- | --- |
| `GET /health` | minimal metadata only, no secret exposure; never infer app feature health |
| `GET /login` | displays correct site-specific Turnstile widget |
| `POST /api/login` | rejects missing/replayed/invalid token and wrong credentials, enforces limits |
| `GET /api/me` | returns 401 without session, scoped role with valid session |
| `POST /api/logout` | server revokes token and subsequent requests fail |
| `GET/PUT /api/workspace` | app+user-scoped reads and writes; rejects oversized/invalid requests |
| `/admin` | only admins access; disabled accounts lose privilege |

## C. Domain-specific threat model and controls

1. Enforce organization scope and employee/manager/HR roles on every request; clients cannot self-assign roles.
2. Step-up MFA, segregation of duties and additional verification for payroll, pay changes and exports.
3. No production employee, salary, finance or leave record in the public showcase.
4. Audit identity changes, approvals, exports and role changes; minimize HR PII in logs.
5. Regional data protection, employment-law retention and deletion must be established before launch.
6. macOS Keychain/Sign in with Apple constraints must be validated independently of web D1 login.

## D. Data persistence and backend connections

- `AUTH_DB` is shared and scoped by `app` + `username` in the prepared implementation. Distinct tenant boundaries and separate databases may be required for production privacy and fault isolation.
- `app_workspace` is a JSON document store for demonstration/workspace state. **It is not a normalized or transactional domain data service**. Create explicit tables, migrations, indexes, ownership filters and optimistic concurrency controls for each feature.
- All third-party API credentials must live in Cloudflare encrypted secrets. Only public keys, approved URLs and non-sensitive metadata belong in public git. Avoid provider-specific secret names/hosts in screenshots.
- Do not send sensitive content to external AI or analytics providers without an approved retention/DPA policy.

## E. Observability and audit requirements

- Server request IDs, error rate/latency, denied logins, rate-limited clients, Turnstile validation failures, suspicious sessions and privileged mutations.
- Record safe actor ID, action, time and affected record identifier, **not** passwords, tokens, OTP seeds, mail content, payment card numbers, payroll figures or PII-rich request bodies.
- Establish log retention and access controls, monitors for sustained failures, and a documented on-call owner.
- Review dependency, SBOM, SAST/DAST, Cloudflare security advisories and source secret scanning on each release.

## F. Backup, disaster recovery and retention

Encrypted HR records with verified restore/retention schedules, restricted backup access and incident runbook.

Define RTO/RPO, automated backup frequency, export/restore ownership, deletion lifecycle, encryption, and rehearsal dates before serving real users.

## G. CI/CD and deployment method

1. **Preflight:** licensing/NDA review, secret scanning, no private repositories/history, review public `README.md` disclosure.
2. **Build and test:** install dependencies in isolated CI, lint/type-check, unit tests, E2E auth, RBAC, and API contract tests.
3. **Environment:** dedicated staging Pages project and database; configure `AUTH_DB`, `TURNSTILE_SITE_KEY`, `TURNSTILE_SECRET`, `ADMIN_USERNAME`, `ADMIN_PASSWORD`. Never put admin secrets in a shell command committed to git.
4. **Deploy:** direct-upload using Wrangler or approved Pages integration. For Pages advanced-mode applications, `_worker.js` is deployed alongside assets and reads `env.ASSETS` / other bindings.
5. **Smoke:** test site routes, 401/403, Turnstile Siteverify, D1 persistence, session cookies, CSP and `frame-ancestors` for `https://portfolio.jelvan.pro` if embedding is explicitly allowed.
6. **Promote:** only after sign-off and reversible release; observe Cloudflare logs and alerts.
7. **Rollback:** revert to known-good Pages deployment; invalidate relevant sessions and rotate compromised secrets if incident response demands. Verify data migrations are backward compatible or have restoration plan.

### Project-critical acceptance scenarios

1. [ ] Employee A cannot access Employee B's private notes/payroll.
2. [ ] Manager approval respects reporting chain and cannot self-approve privileged changes.
3. [ ] Role escalation and sensitive data export require independent approval/step-up auth.
4. [ ] Native macOS and web integrations have explicit parity and signing acceptance.

### Required before declaration of production readiness

- [ ] Complete the [feature acceptance matrix](FEATURE_AND_RELEASE_MATRIX.md) and release-relevant business integrations.
- [ ] Verify real browser, mobile responsiveness, accessibility, locale, keyboard and error states.
- [ ] Prove per-user and per-tenant object authorization with **negative** tests.
- [ ] Test recovery, backup restore, rollback, rate abuse and secret rotation.
- [ ] Document privacy, data residency, acceptable-use, customer consent and incident response.
- [ ] Audit the final deployed artifact against current source SHA and remove demo-only disclosures only when accuracy warrants.

## H. Change control and truthful labeling

Never label a feature `complete` based solely on a mock UI, docs presence, created Cloudflare resource, passing syntax check or HTTP 200. Record commit SHA, build/deployment ID, test output, feature owner and release decision before marking it shipped.

Documentation and NDA notice: [source verification](SOURCE_VERIFICATION.md) · [technical reference](TECHNICAL_REFERENCE.md) · [release matrix](FEATURE_AND_RELEASE_MATRIX.md) · [responsible disclosure](../SECURITY.md).

**Developed and Designed by Jelvan®** — https://portfolio.jelvan.pro
