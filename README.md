## New login and protected dashboard source — 21 October 2026

These are **new independent showcase screens**, not the original/client product or a verified production release. The images below are **illustrative vector previews**, not live-session screenshots.

![MIS sign-in UI preview](assets/screenshots/login.svg)

![MIS dashboard UI preview](assets/screenshots/dashboard.svg)

**Implemented in this adaptation:** Protected operations dashboard, task search and statuses, scoped D1 persistence, user administration, server-verified Turnstile login, eight-hour hashed D1 sessions and admin account control.

**Not yet implemented:** Employee directory, payroll, accounting, native macOS parity and real service-ticket workflows are not implemented.

See [security and staging setup](docs/APP_SECURITY_AND_SETUP.md) and [D1 schema](schema.sql). Staging deployment and authenticated acceptance are required before production.

---

# MIS — public portfolio showcase

## Technical documentation (current audit)

**Audit date:** 20 October 2026 · **Release classification:** not a verified complete production application.

**Current GitHub state:** Documentation only; a separate operations dashboard is staged but not published to this repo.

**Source/stack evidence:** Reviewed sources describe native SwiftUI/macOS + Node/Postgres and a distinct React/Vite/Express workspace; parity is unverified.

**Cloudflare state:** The Pages project hosts an earlier documentation deployment. A site-specific Turnstile widget and a shared `AUTH_DB` D1 binding have been provisioned, but a working application deployment and admin sign-in have not been verified. Secret values must never be committed to this public repository.

**Engineering documentation:**

- **[Complete architecture, folder tree, languages, API contracts and backend connections](docs/TECHNICAL_REFERENCE.md)**
- **[Features, actual implementation status and acceptance requirements](docs/FEATURE_AND_RELEASE_MATRIX.md)**
- **[Authentication, Turnstile, security controls, deployment and operations runbook](docs/SECURITY_AND_OPERATIONS.md)**
- [Source verification and NDA boundaries](docs/SOURCE_VERIFICATION.md)
- [Existing platform/device support notes](docs/DEVICE_PREVIEW.md)

All projects use the portfolio credit **[Developed and Designed by Jelvan®](https://portfolio.jelvan.pro)** for independently authored public work. This does not transfer ownership of third-party/client deliverables.

---


**Management Information System with native macOS employee workflow**  
**Curated by Jelvan R. · Public documentation, not the original source repository.**

> [!IMPORTANT]
> **Independent public portfolio adaptation — confidentiality and attribution**
>
> This repository is a **revised, selectively documented portfolio presentation** independently prepared and maintained by **Jelvan R.** Certain past projects or engagements may be subject to confidentiality, nondisclosure, contractual, intellectual-property, or client-security obligations. To respect those obligations, this public presentation may anonymize, simplify, recreate, omit, or update parts of the original work. **It is not an exact copy, complete implementation, production configuration, or authoritative description of any client system.**
>
> This showcase is **not an official publication of, sponsored by, endorsed by, or affiliated with any current or former client, employer, company, or other development organization**. References to third-party products, technologies, or historical project terminology are for identification only. This notice does **not** claim exclusive ownership of client deliverables, third-party components, trademarks, or intellectual property.
>
> **No confidential source code, credentials, client data, internal hostnames, or production access are provided.** Features and deployment claims must be read with the project-specific verification notes below.


## Overview

A management information system case study covering employee tasks, personal notes, tickets, calendar, notifications and role-aware administrative interfaces.

## Current evidence and status

**Native macOS application source and documentation examined; web workspace is a separate, partially overlapping implementation and should not be presented as parity.**

This repository is **documentation-only**: it does not include an application build, genuine account access, production dependencies or a deployment artifact.

### What the source documentation supports

- Management-Information-System README documents macOS 13+, SwiftUI, Apple sign-in, Node backend and PostgreSQL.
- Source documents granular roles and separate sensitive workflow authorization.
- global-MIS README warns its React/Express implementation is more complete than Cloudflare Worker stub and Flutter shell.
- These are distinct implementations; feature parity, deployment state and data linkage have not been verified.

### Technology context

- SwiftUI (macOS) and Xcode project
- Node.js API and PostgreSQL backing service
- Sign in with Apple and Keychain session storage (source design)
- Separate React/Vite/Express workspace in distinct global-MIS repository

### Capabilities described or proposed

- Native macOS employee dashboard and authenticated navigation
- Employee tasks, notes, events, service tickets and notifications in source docs
- Role-scoped payroll and accounting areas in source design
- Separate browser-based workspace experimentation

> **Accuracy rule:** Any item identified as illustrative, proposed, unverified, or source-documented must not be marketed as a live, completed feature.

## Architecture at a glance

```text
Native macOS app → authenticated Node API → PostgreSQL; separate web workspace remains independently documented
```

For component boundaries, implementation caveats and verification: [Architecture](docs/ARCHITECTURE.md) and [Implementation Notes](docs/IMPLEMENTATION.md).

## Device previews

The portfolio can offer macOS, Desktop Web, iOS and Android **presentation modes**. That does not imply a native build exists on every platform.

| Viewer mode | Evidence-backed display type |
| --- | --- |
| macos | native-swiftui-source |
| web | separate-web-workspace-not-parity |
| ios | no-verified-native-client |
| android | no-verified-native-client |

Read the [device preview policy](docs/DEVICE_PREVIEW.md) before enabling live framing. Public demo assets are intentionally absent until permission and sanitization checks are passed.

## Known limitations

- No employee identity, pay information, finance ledger, production API, client private documentation or staff access published.
- Never imply all macOS features exist in the unrelated web or Flutter scaffolds.

## Repository contents

```text
README.md                       Project overview and verification status
DISCLAIMER.md                   Public-view / NDA and attribution notice
SECURITY.md                     Safe disclosure and content-handling policy
CONTRIBUTING.md                 Public contribution boundaries
portfolio.json                  Sanitized metadata for portfolio integration
docs/ARCHITECTURE.md            Architecture and boundaries
docs/IMPLEMENTATION.md          Evidence, components and non-goals
docs/DEVICE_PREVIEW.md          Frame behavior and security policy
docs/DEPLOYMENT.md              Safe showcase publication workflow
docs/TESTING.md                 QA and release gate checklist
docs/SOURCE_VERIFICATION.md     Evidence status without private repo details
docs/CHANGELOG.md               Public documentation changelog
assets/README.md                Sanitized images/screenshot instructions
```

## Start here

1. Review [the disclaimer](DISCLAIMER.md) and [implementation notes](docs/IMPLEMENTATION.md).
2. Replace placeholder screenshots only with approved, anonymized visuals.
3. Confirm platform support, and enable approved public demo links only after independent testing.
4. Publish as a distinct public repository; **never mirror, fork or reveal original private projects**.
5. Add the public showcase URL to the Projects section of [portfolio.jelvan.pro](https://portfolio.jelvan.pro) without making production URLs visible in the viewer.

## Licensing and use

This repository provides public-facing explanatory materials only. **Public visibility is not an open-source license or a grant of rights to confidential or third-party works.** Written permission and applicable rights are needed before reuse. No rights in third-party products, names, interfaces, libraries, or client materials are asserted.

## Contact

For portfolio discussion, use the contact route on [portfolio.jelvan.pro](https://portfolio.jelvan.pro). Do not post confidential information in public issues.
