# Application Validation Contract

**Project:** Insurance Workflow Automation System  
**Source:** Software Requirements Specification (SRS), Version 1.1  
**Status:** Proposed contract for implementation; stakeholder approval pending.

## Purpose
Define expected validation for application drafts, document uploads, and submission. This contract follows the SRS and does not claim implementation or test completion.

## Related requirements
- **INS-F-002:** Application drafts
- **INS-F-003:** Application submission
- **INS-F-004:** Document upload
- **INS-F-006:** Correction requests
- **INS-F-010:** Application processing
- **INS-F-018:** Concurrency and retries
- **INS-SR-002:** Authorization at the server
- **INS-SR-004:** Safe input and files

## Mandatory application fields
The SRS lists:
- Applicant name
- Contact email
- Coverage selection

The proposed application document checklist includes identity evidence and address evidence. Confirm additional field-level formats or limits with the team/stakeholders rather than inventing them.

## Draft rules
- An authenticated applicant can create, view, and update their own draft.
- A saved draft remains available after sign-out and sign-in.
- Another applicant cannot retrieve or edit the draft.
- Validation is enforced server-side; browser validation alone is insufficient.
- Updates use the current record version. A stale update returns a conflict.

## Submission rules
- Required application fields must be valid.
- Required documents must be present and have a clean scan result before submission.
- Successful submission assigns an application reference and changes state to `Submitted`.
- Missing required fields or documents cause submission to fail, identify the correction, and leave the draft unchanged.
- Submission commands use an `Idempotency-Key` and current record version.
- Retrying an identical request must not create a duplicate submission.

## Document upload rules
- Accepted formats: PDF, JPEG, PNG.
- Maximum file size: 10 MiB per file.
- Maximum active documents: 10 per record.
- Uploads remain quarantined and not reviewable until scan state is `Clean`.
- Oversized, disallowed, excess, or malicious files are rejected or quarantined.
- A new document version invalidates prior verification for that checklist item.
- A verifier's rejection requires a reason.

## Correction and processing rules
- A verifier or processor can return a record to `Needs information` with specific corrections.
- Applicants can resubmit corrected fields or document versions.
- Original versions remain traceable; corrected documents require fresh verification.
- An application can progress to `Pending approval` only after mandatory documents are verified and an assessment is recorded.

## Error and security behaviour
Use the API error response format agreed for the implementation. Invalid or incomplete submissions must not partially mutate a record. Validate fields server-side, use parameterized persistence queries, escape displayed text, enforce ownership/role/assignment checks, and do not expose internal assessment notes in applicant-facing history.

## Verification checklist
- [ ] Mandatory fields are enforced.
- [ ] Missing fields/documents prevent submission without changing the draft.
- [ ] Draft persistence and cross-owner isolation are checked.
- [ ] File type, size, count, quarantine, and scan-state rules are checked.
- [ ] Duplicate submissions are prevented by idempotency.
- [ ] Stale record versions return a conflict.
- [ ] Corrections preserve version traceability and require fresh verification.

These are planned checks. Record actual test commands and results before reporting a check as passed.
