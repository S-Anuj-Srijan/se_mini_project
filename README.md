# Insurance Workflow Automation System

**Team 07 \| SRS v1.1 \| Status: Proposed academic prototype**

## Overview

The Insurance Workflow Automation System is a proposed browser-based
prototype for managing insurance applications and claims from draft
creation through document verification, staff assessment, and an
approval or rejection decision. It is intended to demonstrate role-based
access, workflow state transitions, status history, notifications, and
auditability.

The SRS is a proposed specification and stakeholder approval is pending.
This README describes the intended scope; it does not claim the
application is implemented.

## Scope

The prototype scope includes provisioned user accounts, application and
claim drafts, private documents, verification, role-based queues,
assessments, decisions, notifications, and audit trails. Policy records
are intended to be seeded read-only reference data for claims.

Out of scope for this release: policy issuance, premium collection,
claim payout, actuarial pricing, fraud adjudication, OCR-based
decisions, and live insurer integrations.

## Roles

-   Applicant
-   Verifier
-   Processor
-   Approver
-   Administrator
-   Auditor

Access must be enforced server-side based on role, ownership, and
assignment. Administrator status does not automatically grant approval
rights or unrestricted access to documents.

## Requirements and design documents

-   `Insurance_Workflow_SRS.docx` --- requirements baseline.
-   `docs/requirements-baseline.md` --- requirements relevant to the
    first demonstrable workflow.
-   `docs/mvp-acceptance-criteria.md` --- proposed acceptance criteria.
-   `docs/roles-and-permissions.md` --- role responsibilities and
    restrictions.
-   `docs/auth-session-contract.md` --- proposed authentication/session
    contract.
-   `docs/application-validation-contract.md` --- proposed application
    validation contract.

## Technology stack and setup

The SRS and execution plan describe candidate technologies, not an
already verified implementation. Confirm the actual stack and versions
with the team and record the decision before adding installation
commands. Do not assume that proposed FastAPI, PostgreSQL, or frontend
components are already present.

Setup and test commands will be documented after the repository's actual
implementation and dependencies are verified.

## Test status

The SRS maps 31 requirements to 37 planned test cases. Those tests are
planned, not reported as executed. Add test commands, CI status,
coverage, and results here only after they have been run and verified.

## Development workflow

1.  Create or identify a Jira issue with acceptance criteria before
    starting work.
2.  Use a feature branch named for the Jira issue.
3.  Commit logical changes and push the branch.
4.  Open a pull request with a summary, issue link, and genuine test
    evidence.
5.  Require a passing CI check and another contributor's review before
    merging.
6.  Record unresolved requirements and defects rather than marking them
    complete without evidence.

## Data and security

Use synthetic personal data for demonstrations. Do not commit
credentials, session secrets, real policyholder data, or private
documents. The SRS requires protected transport, server-side
authorization, safe input handling, private document storage, and
auditable workflow transitions.

## Project status

Requirements documentation is under review. Stakeholder approvals,
implementation verification, and planned test execution remain pending
until supported by recorded evidence.
