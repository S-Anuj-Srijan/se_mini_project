# Application Validation Contract

**Related SRS requirements:** INS-F-002, INS-F-003, INS-F-004,
INS-F-006, INS-F-010, INS-F-012, INS-F-018, INS-SR-002, INS-SR-004\
**Status:** Contract proposal for review; exact API routes and schema
depend on the agreed implementation.

## Required application fields

The SRS identifies these mandatory application fields: - Applicant
name - Contact email - Coverage selection

The SRS also proposes an application document checklist of identity
evidence and address evidence. Required documents must have a clean scan
result before submission.

## Draft behaviour

-   An authenticated applicant can create, view, and update their own
    draft.
-   A draft must persist across sign-out and sign-in.
-   An applicant cannot retrieve or modify another applicant's draft.
-   Server-side validation is authoritative; client-side validation is
    only a usability aid.
-   Use record versioning to detect stale updates. The SRS requires
    stale updates to return a conflict.

## Submission behaviour

-   Submission is allowed only when required fields are valid and
    required documents are clean.
-   A successful submission assigns an application reference and changes
    the state to `Submitted`.
-   An incomplete submission is rejected with actionable correction
    information and leaves the draft unchanged.
-   Submission must use an idempotency key and current record version.
-   Retrying an identical request must not create a duplicate
    submission.

## Document validation

-   Accepted formats: PDF, JPEG, PNG.
-   Maximum size: 10 MiB per file.
-   Maximum active documents: 10 per record.
-   Uploads are quarantined until a clean scan result is available.
-   A blocked, oversized, disallowed, or excess upload must not become
    reviewable.
-   A replacement document version invalidates prior verification for
    that checklist item.
-   Document rejection requires a reason.

## Correction and processing rules

-   A verifier or processor can return a record to `Needs information`
    with specific corrections.
-   The applicant can resubmit corrected fields or document versions.
-   Original versions remain traceable and corrected documents require
    fresh verification.
-   A record cannot progress to `Pending approval` until mandatory
    documents are verified and an assessment is recorded.

## Error and security rules

-   Use a consistent API error structure agreed by the team.
-   Reject malformed or missing required values without partially
    mutating the record.
-   Validate input on the server, use parameterized persistence queries,
    and escape displayed text.
-   Enforce owner, role, and assignment checks server-side.
-   Do not expose internal assessment notes or sensitive data in
    applicant-facing responses.

## Fields requiring confirmation

Do not invent additional application fields, coverage options,
email-format policy beyond what the team agrees, or extra size/length
limits. Confirm them against the SRS and stakeholder decisions before
implementation.

## Verification checklist

-   [ ] Required fields are enforced.
-   [ ] Invalid/incomplete submissions leave the draft unchanged.
-   [ ] Draft persists across sessions.
-   [ ] Cross-owner access is denied.
-   [ ] Upload format, size, count, and scan-state rules are enforced.
-   [ ] Duplicate submission is prevented.
-   [ ] Stale-version updates return a conflict.
-   [ ] Corrections preserve version history and require fresh document
    verification.

These are planned checks, not claims of passing tests.
