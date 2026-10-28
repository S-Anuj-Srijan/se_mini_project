# Roles and Permissions Summary

**Source:** SRS v1.1, section 2.3 and security requirements\
**Status:** Proposed baseline; validate against stakeholder-approved
requirements.

  -----------------------------------------------------------------------
  Role                    Permitted               Important restriction
                          responsibilities        
                          described by the SRS    
  ----------------------- ----------------------- -----------------------
  Applicant               Access own drafts,      Must not access another
                          documents, status, and  applicant's records
                          notices                 

  Verifier                Review assigned clean   Must not review
                          documents; record       unassigned records or
                          verification or         bypass scan status
                          correction reasons      

  Processor               Assess assigned         Cannot approve their
                          applications or claims  own assigned work
                          and request corrections 

  Approver                Decide eligible records Must be independent of
                          in `Pending approval`   the applicant and
                                                  assigned processor

  Administrator           Manage provisioned      Administrator status
                          roles, assignment, and  does not automatically
                          operational delivery    grant approval rights
                          failures                or access to every
                                                  document

  Auditor                 Read authorized audit   Must not mutate
                          metadata                business records or
                                                  delete audit entries
  -----------------------------------------------------------------------

## Enforcement principles

1.  Enforce permissions on the server for every protected endpoint and
    document download.
2.  Deny access by default when role, ownership, or assignment checks
    fail.
3.  Do not trust a role or owner identifier supplied by the client as
    proof of permission.
4.  Record role changes and relevant security/workflow events in the
    audit trail.
5.  Keep internal assessment notes out of applicant-facing
    status/history responses.
6.  Separate document scan state (`Pending`, `Clean`, `Blocked`) from
    review state (`Unverified`, `Verified`, `Rejected`).

## Evidence needed

Permission tests should cover valid access, wrong-role access,
cross-applicant access, unassigned staff access, processor/approver
separation, and denied audit mutation. These are planned test areas, not
reported test results.
