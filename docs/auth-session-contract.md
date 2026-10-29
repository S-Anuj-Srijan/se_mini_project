# Authentication and Session Contract

**Project:** Insurance Workflow Automation System  
**Source:** Software Requirements Specification (SRS), Version 1.1  
**Status:** Proposed contract for implementation; stakeholder approval pending.

## Purpose
Define expected authentication, session, and authorization behaviour. This document describes requirements; it does not claim that features are implemented.

## Related requirements
- **INS-F-001:** Account access
- **INS-F-016:** Role administration
- **INS-SR-002:** Authorization at the server
- **INS-SR-003:** Credentials and sessions
- **INS-SR-006:** Audit integrity and separation
- **INS-SR-007:** Abuse control

## Sign-in
- Authenticate provisioned user accounts.
- Invalid credentials must fail without revealing whether an account exists.
- Throttle after 5 failed attempts per account and source within a rolling 15-minute window.
- Never log passwords or session secrets.

## Session management
- Protected operations require a valid authenticated session.
- Sign-out invalidates the active session.
- Session cookies use `Secure`, `HttpOnly`, and `SameSite` attributes.
- State-changing browser requests require CSRF protection.
- Idle sessions expire after 15 minutes.
- Sensitive data must not be placed in URL query parameters.

## Roles and authorization

| Role | Responsibilities |
|---|---|
| Applicant | Access own drafts, documents, status, and notices |
| Verifier | Review assigned clean documents and record verification/correction reasons |
| Processor | Assess assigned records and request corrections; cannot approve own assigned work |
| Approver | Decide eligible pending records independently of applicant and processor |
| Administrator | Manage provisioned roles, assignments, and operational delivery failures |
| Auditor | Read authorized audit metadata; cannot mutate business records or delete audit entries |

Enforce role, ownership, and assignment checks on every protected endpoint and document download. Deny access by default. Never trust a caller-supplied role or owner identifier as proof of permission. An administrator does not automatically gain approval rights or unrestricted document access. Role grants/revocations must be restricted and audited.

## Error behaviour
Use the error format agreed for the actual API. Unauthorized requests must not mutate data. For access-denial cases, the SRS allows `403` or a non-disclosing `404`; document the implementation's convention.

## Verification checklist
- [ ] Valid provisioned account can sign in.
- [ ] Invalid credentials fail without account-existence disclosure.
- [ ] Sign-out invalidates the session.
- [ ] Missing, invalid, or expired sessions are rejected on protected routes.
- [ ] Cross-owner, wrong-role, and unassigned-staff access is denied without mutation.
- [ ] Role grants/revocations are restricted and audited.
- [ ] Cookie attributes, CSRF protection, idle expiry, and rate limits are verified.
- [ ] Logs contain no passwords or session secrets.

Do not mark an item passed until a test has been run and evidence recorded.
