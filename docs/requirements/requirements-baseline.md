# Insurance Workflow Automation System --- Requirements Baseline

**Team:** 07\
**Baseline source:** Software Requirements Specification (SRS), Version
1.1, 12 October 2026\
**Status:** Proposed; stakeholder approval pending.

## Purpose

This document identifies the requirements relevant to the first
demonstrable application workflow. The SRS remains the authoritative
requirements source; this file is a concise working baseline, not a
replacement for it.

## Minimum demonstrable workflow

1.  An applicant signs in and creates or updates their own application
    draft.
2.  The applicant supplies the required application fields and required
    supporting documents.
3.  The system validates the draft and allows submission only when
    required fields and documents meet the stated rules.
4.  An assigned verifier reviews clean documents and records
    verification or rejection with a reason.
5.  An assigned processor reviews the submitted application and records
    an assessment after mandatory documents are verified.
6.  An independent approver approves or rejects a record in
    `Pending approval`, with a decision reason.
7.  The system records status history and audit events for relevant
    actions.

The workflow follows the SRS lifecycle. Implementation and test
completion must be evidenced separately.

## Relevant functional requirements

  -----------------------------------------------------------------------
  Requirement             Summary                 Planned test references
  ----------------------- ----------------------- -----------------------
  INS-F-001               Authenticate registered TC-001
                          users, terminate        
                          sessions on logout, and 
                          show role-permitted     
                          actions                 

  INS-F-002               Applicants create,      TC-002
                          view, and update their  
                          own application drafts  

  INS-F-003               Validate required       TC-003, TC-004
                          fields and clean        
                          required documents      
                          before application      
                          submission              

  INS-F-004               Accept specified        TC-005, TC-006
                          document formats and    
                          limits; quarantine      
                          until clean scan        

  INS-F-005               Let verifiers verify or TC-007
                          reject clean documents  
                          and record rejection    
                          reasons                 

  INS-F-006               Request corrections and TC-008
                          preserve traceability   
                          of corrected versions   

  INS-F-009               Assign submitted        TC-012
                          applications/claims to  
                          eligible staff and      
                          retain assignment       
                          history                 

  INS-F-010               Process an application  TC-013
                          only after required     
                          documents are verified  
                          and assessment is       
                          recorded                

  INS-F-012               Allow an independent    TC-015, TC-016
                          approver to decide a    
                          pending record with a   
                          reason                  

  INS-F-013               Show applicants their   TC-017
                          current state and       
                          public history without  
                          internal notes          

  INS-F-015               Record relevant actions TC-020
                          in an auditable trail   

  INS-F-018               Prevent duplicate       TC-023, TC-024
                          submission/decisions    
                          and handle stale        
                          versions consistently   
  -----------------------------------------------------------------------

## Relevant security requirements

-   **INS-SR-002:** Enforce role, ownership, and assignment checks
    server-side on protected endpoints and document downloads; deny
    access by default.
-   **INS-SR-003:** Use salted adaptive password hashes, secure
    session-cookie controls, CSRF protection for state-changing browser
    requests, and the specified idle-session timeout.
-   **INS-SR-004:** Validate input server-side, use parameterized
    persistence queries, escape displayed text, and inspect file
    signatures and scan results.
-   **INS-SR-006:** Prevent business users from editing/deleting audit
    entries and enforce separation between processing and approval.
-   **INS-SR-007:** Apply the specified authentication and upload abuse
    controls.

## Required application fields and document rules

According to the SRS: - Application mandatory fields: applicant name,
contact email, and coverage selection. - Proposed application checklist:
identity and address evidence. - Accepted document formats: PDF, JPEG,
PNG. - Maximum file size: 10 MiB per file. - Maximum active documents:
10 per record. - Uploaded files must remain unavailable for review until
the scan adapter reports a clean result.

The SRS marks implementation details and some thresholds as proposals to
validate. Do not treat stakeholder-pending assumptions as approved
policy.

## Out of scope for this release

Policy issuance, premium collection, claim payout, actuarial pricing,
fraud adjudication, OCR-based decisions, and live insurer integrations
are outside the stated prototype scope.

## Status and evidence

This is a requirements planning document. It does not claim that any
feature has been implemented or tested. Planned tests remain unexecuted
until results and evidence are recorded. Stakeholder approval remains
pending.
