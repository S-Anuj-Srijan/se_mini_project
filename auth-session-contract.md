# Authentication and Session Contract

**Related SRS requirements:** INS-F-001, INS-F-016, INS-SR-002,
INS-SR-003, INS-SR-006, INS-SR-007\
**Status:** Contract proposal for review; not an implementation claim.

## Scope

Define expected authentication, session, and role-administration
behaviour for provisioned demo accounts. Exact API paths and payloads
must match the implementation once the team agrees on the stack and API
conventions.

## Behaviour

### Sign-in

-   Authenticate provisioned accounts.
-   Reject invalid credentials without revealing whether the account
    exists.
-   Apply the SRS abuse-control policy: throttle after 5 failed attempts
    per account and source within a rolling 15-minute window.
-   Never log passwords, session secrets, or sensitive credential
    payloads.

### Session and sign-out

-   Protected requests require a valid authenticated session.
-   Sign-out invalidates the session; replaying it afterward must be
    denied.
-   Follow the SRS session controls: Secure, HttpOnly, SameSite session
    cookies, CSRF protection for state-changing browser requests, and
    idle expiry after 15 minutes.
-   Do not place secrets in URL query parameters.

### Authorization

-   Enforce role, ownership, and assignment checks server-side for each
    protected operation and document download.
-   Deny access by default.
-   Do not rely on caller-supplied role values.
-   Applicants may access only their own drafts, documents, status, and
    notices.
-   Verifiers and processors are restricted to their assigned work and
    permitted actions.
-   An approver must be distinct from the applicant and assigned
    processor for the record being decided.
-   Administrators can manage provisioned roles and assignments, but do
    not automatically gain approval rights or unrestricted document
    access.
-   Auditors can read authorized audit metadata but cannot mutate
    business records or delete audit entries.

### Role administration

-   Only an authorized administrator may grant or revoke roles on
    provisioned accounts.
-   A revoked permission must be denied on the next protected request.
-   Role changes must be audited.

## Expected error behaviour

Use the API's agreed error format consistently. Unauthorized or
unauthenticated requests must not mutate data. The SRS allows a `403` or
a non-disclosing `404` for access-denial cases; select and document the
convention used by the implementation.

## Verification checklist

-   [ ] Valid sign-in succeeds.
-   [ ] Invalid credentials fail without account-existence disclosure.
-   [ ] Sign-out invalidates the session.
-   [ ] Missing/expired session is rejected on protected routes.
-   [ ] Cross-owner and wrong-role requests are denied without mutation.
-   [ ] Unassigned staff cannot perform restricted actions.
-   [ ] Role grants/revocations are restricted and audited.
-   [ ] CSRF, idle expiry, cookie attributes, and rate limits are
    verified.

No item is considered passed until a test is run and its evidence is
recorded.
