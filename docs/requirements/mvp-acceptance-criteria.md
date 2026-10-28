# MVP Workflow and Acceptance Criteria

**Source:** Insurance Workflow Automation System SRS v1.1\
**Status:** Proposed acceptance criteria; review and stakeholder
approval pending.

## Goal

Demonstrate one traceable application journey from draft creation
through staff review and an independent decision. The SRS is the source
of business rules; this document does not claim implementation is
complete.

## Acceptance criteria

### AC-01 --- Sign-in and session

-   A valid provisioned demo account can sign in.
-   Invalid credentials fail without revealing whether an account
    exists.
-   Sign-out invalidates the session.
-   Protected requests without a valid session are rejected.

Related requirements: INS-F-001, INS-SR-003.

### AC-02 --- Application draft and ownership

-   An applicant can create, view, and update their own draft.
-   A saved draft remains available after sign-out and sign-in.
-   Another applicant cannot retrieve or modify that draft.

Related requirement: INS-F-002.

### AC-03 --- Application validation and submission

-   Applicant name, contact email, and coverage selection are required.
-   Required documents must be present and have a clean scan result
    before submission.
-   A complete draft can be submitted once and receives a reference and
    `Submitted` status.
-   Missing required fields or documents prevent submission and leave
    the draft unchanged with a clear correction message.

Related requirement: INS-F-003.

### AC-04 --- Document handling

-   PDF, JPEG, and PNG files within the 10 MiB per-file and
    10-active-document limits are eligible for upload.
-   Oversized, disallowed, excess, or malicious files are rejected or
    quarantined and are not reviewable.
-   A verifier can mark a clean document `Verified` or `Rejected`.
-   Rejection requires a reason, and the reviewer and timestamp are
    recorded.

Related requirements: INS-F-004, INS-F-005.

### AC-05 --- Assignment and processing

-   An administrator can assign a record to eligible staff.
-   Assigned staff see the record in their queue; unauthorized or
    unassigned staff cannot perform restricted actions.
-   An assigned processor can progress a submitted application to
    `Under review`.
-   Progression to `Pending approval` is blocked until mandatory
    documents are verified and an assessment is recorded.

Related requirements: INS-F-009, INS-F-010, INS-SR-002.

### AC-06 --- Independent decision

-   Only an authorized approver can approve or reject a record in
    `Pending approval`.
-   The approver must be distinct from the applicant and the assigned
    processor for that record.
-   A non-empty decision reason is required.
-   Premature, unauthorized, and self-approved decisions are rejected.
-   Repeating an identical request with its original idempotency key
    returns the original outcome without a second mutation; a new
    decision on a terminal record returns a conflict.

Related requirements: INS-F-012, INS-F-018, INS-SR-006.

### AC-07 --- Status history and audit

-   Applicants can see their own current state and public dated history.
-   Internal assessment notes are not exposed to applicants.
-   Relevant access denials, assignment changes, document reviews, and
    workflow transitions create audit metadata.
-   Audit entries do not contain document contents, passwords, or
    session secrets.

Related requirements: INS-F-013, INS-F-015.

## Completion evidence

For each criterion, record: - Jira issue and acceptance result. -
Branch, pull request, and merged commit SHA if merged. - Exact test
command and actual result. - Screenshot or test output where useful. -
Open defects, assumptions, and untested criteria.

Do not mark a criterion complete solely because its documentation
exists. Full SRS acceptance also requires execution and evidence for the
planned test cases; that is not claimed here.
