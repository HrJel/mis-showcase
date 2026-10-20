# Implementation notes — MIS

## Evidence ledger

- Management-Information-System README documents macOS 13+, SwiftUI, Apple sign-in, Node backend and PostgreSQL.
- Source documents granular roles and separate sensitive workflow authorization.
- global-MIS README warns its React/Express implementation is more complete than Cloudflare Worker stub and Flutter shell.
- These are distinct implementations; feature parity, deployment state and data linkage have not been verified.

## Functional narrative

A management information system case study covering employee tasks, personal notes, tickets, calendar, notifications and role-aware administrative interfaces.

### Functional areas

- Native macOS employee dashboard and authenticated navigation
- Employee tasks, notes, events, service tickets and notifications in source docs
- Role-scoped payroll and accounting areas in source design
- Separate browser-based workspace experimentation

## Implementation constraints

- No employee identity, pay information, finance ledger, production API, client private documentation or staff access published.
- Never imply all macOS features exist in the unrelated web or Flutter scaffolds.

## What this repository implements

- Markdown documentation, project-level metadata, safe viewer mode classification and release checklists.
- **No actual application runtime**, private source tree, database schema, email transport, credentials or deployment wiring.
- **No real live preview** is wired without an approved separate demo endpoint.

## Mapping from source to public presentation

The source references have been read for high-level technical accuracy, but private repositories and URLs are intentionally **not** disclosed in this publication. Documentation is paraphrased and stripped of confidential configuration. Technical assumptions requiring full source review remain marked as unverified.

## Upgrade path

1. Verify exact product and canonical source/version with the rights holder.
2. Inventory features that may safely be demonstrated.
3. Capture anonymized screenshots and create fake-data demo fixtures.
4. Independently test each indicated platform.
5. Update `portfolio.json` only after a reviewer approves the published claim.
