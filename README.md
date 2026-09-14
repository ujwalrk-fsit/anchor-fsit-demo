# Anchor — Internal Identity Platform

Centralized identity for all internal apps, so teams stop rebuilding login, sessions, password storage, and access control per project.

Anchor owns **who a user is and when they may act**. Applications keep ownership of **what a user can do with their own resources**.

## Contents

- `index.html` — public landing page: hero with product snapshot, code samples, capability explorer, and pillar overview.
- `docs.html` — developer docs app: full pillar reference, guides, API/SDK pages, roadmap, and release notes.

Both are single static files. No build step, no dependencies — open either one in a browser. The landing brand and pillar cards link into the docs; the docs brand links back to the landing page.

## Landing page

- Hero with headline, docs CTAs, and a mock Anchor console window (tenant status, usage stats, live-style activity feed).
- "An identity platform for developers and agents": capability checklist beside a tabbed code panel (JavaScript / Python / cURL).
- "Explore by capability": a window-framed explorer with Auth, SSO, MFA, RBAC, and Webhooks tabs — each swaps its description and runnable-style sample.
- "Everything around the token": six pillar cards that open the docs.
- Multi-column footer (Learn, API Reference, Community, More) plus legal strip.
- Same design tokens and DM Sans / DM Mono type as the docs for a consistent scale.

## Docs site

- Three-column shell: collapsible sidebar nav, scrollable article column, "On this page" outline with scroll-spy. Sticky in-column footer with Privacy Policy, Terms of Use, Security, and © 2026 Fortunesoft IT Innovations.
- Top bar: brand, version picker (`v2026.09` current), search pill (`Ctrl + K` command palette with keyboard navigation), Anchor AI assistant button, and tabs for API Reference, SDKs, Roadmap, Release Notes, Status.
- Anchor AI assistant: sparkle-icon button docks a fourth column inside the layout — header, scrollable messages, input + send. Toggle from the top bar, close via X or Escape.
- Stability signals everywhere: Beta and Deprecated chips in titles, `(Beta)` / `(Deprecated)` suffixes across nav and lists, and a meta strip (area / stability / date) on every page. Deprecated pages carry a migration callout with sunset pointer.
- Article pages: breadcrumbs, in-this-section lists, related pages, prev/next pager, and a "Was this page helpful?" widget.
- Feedback system: per-page Report an issue / Suggest a feature dialog with rating, validation, file attach, and description preview.
- Roadmap (Phase 1 live Sept 2026, Phase 2 committed Q4 2026, Phase 3 sequenced H1 2027, Under evaluation) and chronological Release Notes back to the v1 release candidate.

## Platform coverage

### Authentication
- Hosted login page (redirect, centrally maintained)
- Embedded login SDK (Beta) for in-UI flows
- Passwordless / passkeys (Beta): magic links, passkey sign-in
- SSO: OIDC (default, auth code + PKCE), SAML 2.0, cross-app SSO
- MFA: TOTP (default), WebAuthn / passkeys (Beta), enforceable MFA policies; SMS fallback is Deprecated in favor of WebAuthn
- Sessions & tokens: access / ID / refresh tokens, automatic refresh-token rotation, revocation, device & session management (Beta)
- Protections: brute-force protection and login rate limiting at platform level

### User management
- User CRUD via API / admin console, self-service profile + password reset
- Soft-delete + scheduled anonymization (Beta)
- Multi-tenancy with data-layer isolation, org / team hierarchy, delegated admin (Beta)
- SCIM provisioning / de-provisioning (Beta)

### Roles & access control
- Roles and permissions carried in tokens
- Conditional policy engine (Beta, path to ABAC)
- Immutable audit logging of logins, role changes, admin actions
- Access review / recertification prompts (Beta)

### Compliance & security
- SOC 2 Type II and ISO 27001 status tracking (Beta)
- GDPR + DPDP handling: consent, subject requests, cross-border transfers
- Encryption at rest (platform-managed keys) and in transit (TLS everywhere), key rotation runbooks (Beta)
- Retention policies per data category (Beta), PII classification + log masking (Beta)
- Breach notification process, pen-testing + vuln scanning cadence (Beta)

### Integrations
- Connector framework: one adapter interface for all providers, custom-connector guide
- Enterprise IdP federation: SAML and OIDC brokering
- KYC/AML: Persona and Onfido hooks (Beta)
- Social login: Google, GitHub, Microsoft

### Reliability & operations
- 99.95% monthly target for login and token issuance
- Per-client / per-tenant rate limits, horizontal scaling of stateless auth services, multi-region active-passive failover (Beta)
- Metrics, distributed tracing, alerting subscriptions
- Versioned APIs, backup / restore with tested recovery for the user directory

### SDKs and developer tools
- Web (JS/React) and backend (Node, Java, Python, .NET) GA; mobile (iOS/Android) and CLI in Beta
- API reference from the same spec as the SDKs, sandbox tenants, request-level debugging logs, webhooks for lifecycle events (Beta)

### Governance
- Platform Charter with scope boundaries and build-vs-buy decision tree
- Release management: semver, cadence + changelog, deprecation / sunset policy, compat guarantees
- ADRs: immutable chronological log + proposal template
- Migration guides: Okta / Auth0, Azure Entra ID, Keycloak (Beta)
- Runbooks: incident playbooks, on-call escalation, common failure modes

## Use

```bash
# no install, no build
open index.html         # start here
open docs.html     # full reference
```

## Visit Docs

https://fsit-anchor-v1.vercel.app/

© 2026 Fortunesoft IT Innovations
