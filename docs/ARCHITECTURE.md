# Architecture — MIS

## Architecture status

**Native macOS application source and documentation examined; web workspace is a separate, partially overlapping implementation and should not be presented as parity.**

## Public high-level flow

```text
Native macOS app → authenticated Node API → PostgreSQL; separate web workspace remains independently documented
```

## Verified high-level design

A SwiftUI macOS client stores refresh credentials in Keychain and calls a server-authorized Node API backed by PostgreSQL. An additional web workspace repository contains React/Vite/Express code and unfinished Worker/Flutter experiments; it is not assumed to share the same backend.

## Technology references

- SwiftUI (macOS) and Xcode project
- Node.js API and PostgreSQL backing service
- Sign in with Apple and Keychain session storage (source design)
- Separate React/Vite/Express workspace in distinct global-MIS repository

## Trust boundaries

1. The public showcase is a separate documentation/presentation boundary. It is not authorized to access production accounts or protected datasets.
2. Authentication, authorization, storage operations and confidential business rules, if applicable, belong to private reviewed services—not public mock UI.
3. An iframe is a nested browser context, not a substitute for server authentication or entitlement checks.
4. Device frames alter dimensions and appearance, not actual native runtime behavior.

## Unverified or intentionally omitted

- No employee identity, pay information, finance ledger, production API, client private documentation or staff access published.
- Never imply all macOS features exist in the unrelated web or Flutter scaffolds.

## Security/design review before going live

- [ ] Confirm any referenced architecture is approved for public disclosure.
- [ ] Use invented demo identifiers, content and accounts.
- [ ] Verify no private URL or client organization names appear in HTML, CSS, JS, screenshots or history.
- [ ] Test browser permissions and iframe CSP on the actual demo host.
- [ ] Confirm accessibility and responsive behavior separately on representative devices.
