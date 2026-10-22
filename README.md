# NorthStar-JML-Identity-Lifecycle
A hands-on Joiner–Mover–Leaver (JML) homelab using Active Directory and Microsoft Entra ID to manage employee onboarding, role changes, and offboarding, with RBAC and simulated ServiceNow-style tickets.

# NorthStar Medical Group — Joiner–Mover–Leaver Identity Lifecycle

![NorthStar Medical Group JML Project](images/northstar-jml-banner.png)

**Active Directory | Microsoft Entra ID | RBAC | Identity Lifecycle Management**

> **Fictional homelab project:** NorthStar Medical Group is a fictional healthcare organization. The business events, approvals, and tickets in this project are simulated.
>
> **Project status:** Scenario design and implementation planning. Existing employee accounts have already synchronized to Microsoft Entra ID. The JML activities below must be performed and validated before being reported as completed.

---

## Project Overview

This project extends my previous Active Directory and hybrid identity labs by introducing a structured Joiner–Mover–Leaver (JML) process.

The existing environment contains employee accounts in on-premises Active Directory that have synchronized to Microsoft Entra ID through Microsoft Entra Connect Sync.

The next step is to manage access throughout the employee lifecycle:

- **Joiner:** Validate onboarding and approved access for existing synchronized employees.
- **Mover:** Update access when employees change departments or responsibilities.
- **Leaver:** Disable identities and remove access when employment ends.

This phase uses existing test accounts rather than creating duplicate identities.

## Previous Projects

This project builds on:

1. [Basic Employee Onboarding — Active Directory and RBAC](https://github.com/otraore26/Basic-Employee-Onboarding-AD-RBAC-)
2. [NorthStar Hybrid Identity — AD to Entra ID Synchronization](https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync)

The first project established departmental OUs and security groups. The second connected the directory to Microsoft Entra ID.

This project applies lifecycle processes to that foundation.

---

## Fictional Business Scenario

After completing its hybrid identity deployment, NorthStar Medical Group conducts a workforce access review.

Sandra Torres, HR Manager, and Marcus Johnson, IT Administrator, identify several requests requiring coordinated action:

- James Whitfield’s account is synchronized, but his onboarding validation is incomplete.
- Jane Cooper works as an Operations Coordinator but remains in the HR group.
- Karen Mills requires temporary Operations access for a reporting assignment.
- Robert Hayes is preparing to retire and requires scheduled offboarding.

In this scenario, Jane’s group mismatch represents an incomplete transfer from HR to Operations.

Acting as the IAM Engineer, I am responsible for reviewing approvals, implementing the authorized changes, verifying synchronization, and documenting the results.

Priya Patel, Security Analyst, performs a simulated review of the resulting evidence.

## Problem Statement

Directory synchronization does not automatically ensure appropriate access.

Without a documented lifecycle process:

- Employees may receive incorrect memberships during onboarding.
- Transferred employees may retain access from previous roles.
- Temporary permissions may remain indefinitely.
- Departing employees may retain usable accounts.
- Tickets may be closed without evidence that the changes worked.

This project addresses these risks through approval-based requests, least-privilege access, and evidence-based validation.

---

## Lab Environment

| Component | Configuration |
|---|---|
| Fictional organization | NorthStar Medical Group |
| Lab server | NMG-DC01 |
| Source directory | Active Directory Domain Services |
| AD domain | NMGM.com |
| Cloud directory | Microsoft Entra ID |
| Synchronization | Microsoft Entra Connect Sync |
| Virtualization | Oracle VirtualBox |
| Departments | HR, IT, Finance, Operations |
| Ticketing | Simulated ServiceNow-style records |

### Departmental Security Groups

- HR-Users
- IT-Users
- Finance-Users
- Operations-Users

For synchronized identities, relevant account attributes and departmental memberships are managed in on-premises AD and then verified in Entra ID.

Cloud session revocation and application-specific actions are recorded separately.

> OU placement, security-group membership, and actual resource access are separate checks. Moving an account into an OU does not automatically update its group memberships.

---

## Employee Roster

The lab contains 17 existing accounts. The following 15 employees have been documented for this scenario. Two additional employees remain to be added to the roster.

| Employee | Current role | Starting group |
|---|---|---|
| James Whitfield | HR Recruiter | HR-Users |
| Jane Cooper | Operations Coordinator | HR-Users |
| Michelle Grant | Benefits Coordinator | HR-Users |
| Sandra Torres | HR Manager | HR-Users |
| Aisha Coleman | Systems Engineer | IT-Users |
| Marcus Johnson | IT Administrator | IT-Users |
| Priya Patel | Security Analyst | IT-Users |
| Tyler Brooks | Help Desk Technician | IT-Users |
| David Chen | Finance Manager | Finance-Users |
| Karen Mills | Finance Analyst | Finance-Users |
| Lisa Park | Accounts Payable | Finance-Users |
| Robert Hayes | Payroll Specialist | Finance-Users |
| Brian Foster | Operations Manager | Operations-Users |
| Carlos Rivera | Facilities Supervisor | Operations-Users |
| Natalie Ross | Scheduling Coordinator | Operations-Users |

---

## JML Pilot Scenarios

### 1. Joiner — James Whitfield

James already has an AD account synchronized to Entra ID. HR requests validation before closing his onboarding record.

**Planned actions:**

1. Identify the existing account.
2. Review department, title, and approved manager information.
3. Confirm appropriate HR OU placement.
4. Verify HR-Users membership in AD.
5. Review unrelated memberships.
6. Verify the synchronized identity and HR membership in Entra ID.
7. Test approved resource access if a protected HR test resource exists.

**Acceptance criteria:**

- No duplicate identity is created.
- Approved HR membership is verified in both directories.
- Any resource-access claims are supported by actual tests.

### 2. Mover — Jane Cooper

Jane has transferred from HR into Operations, but her departmental membership has not been updated.

**Planned actions:**

1. Record approval from both departments.
2. Capture current attributes and memberships.
3. Update department and manager information.
4. Move the account to the Operations OU if appropriate.
5. Remove HR-Users membership.
6. Add Operations-Users membership.
7. Verify the synchronized changes.
8. Test new access and removal of old access where test resources exist.

**Acceptance criteria:**

- Jane retains her existing identity.
- Operations-Users membership is present.
- Obsolete HR-Users membership is removed.
- Updated attributes reflect the approved transfer.

### 3. Temporary Access — Karen Mills

Karen temporarily supports an Operations reporting project while retaining her Finance role.

**Planned actions:**

1. Document the business justification.
2. Obtain approval from Finance and Operations.
3. Define the start date and expiry time.
4. Confirm the minimum access required.
5. Grant the approved access.
6. Verify the resulting membership or resource permission.
7. Track a removal task.
8. Remove and verify temporary access at expiry.

**Acceptance criteria:**

- Existing approved Finance access remains intact.
- Temporary access has documented approval and an end date.
- Access removal is verified after the assignment.

> If Operations-Users provides broader access than required, use a narrower resource-specific permission instead. An expiry written in a ticket does not automatically remove a group membership.

### 4. Leaver — Robert Hayes

Robert is retiring after completing his payroll handover. HR specifies the departure time, and Finance identifies business-record retention requirements.

**Planned actions:**

1. Confirm the approved departure date and time.
2. Capture the original account status and memberships.
3. Identify additional application access configured in the lab.
4. Disable the AD account at the approved time.
5. Remove relevant access-granting memberships.
6. Verify the disabled state in Entra ID.
7. Revoke cloud sessions.
8. Verify applicable application access removal.
9. Document retention requirements separately.

**Acceptance criteria:**

- The identity is disabled in both directories.
- Relevant access is removed.
- Session-revocation actions are documented.
- Any remaining application or session limitations are recorded.
- Account deletion is deferred pending a separate retention decision.

---

## Mock ServiceNow-Style Tickets

These records are fictional templates. They do not represent requests submitted to a live ServiceNow instance.

### RITM0010001 — Validate HR Onboarding

| Field | Value |
|---|---|
| Requested for | James Whitfield |
| Requested by | Sandra Torres |
| Request type | Onboarding validation |
| Assignment group | Identity and Access Management |
| Assigned to | Ousmane Traore |
| Priority | 3 — Moderate |
| State | Open |
| Approval | Pending |

**Description:**  
Validate James’s existing synchronized identity and confirm approved HR access. Do not create a new account.

**Initial work note:**  
Existing identity selected for review. Account attributes and memberships will be compared against approved onboarding requirements.

**Required evidence:**  
AD attributes, AD membership, Entra ID membership, and any resource-test results.

### RITM0010002 — Transfer HR Access to Operations

| Field | Value |
|---|---|
| Requested for | Jane Cooper |
| Requested by | Sandra Torres |
| Approvers | Sandra Torres and Brian Foster |
| Request type | Department transfer |
| Assignment group | Identity and Access Management |
| Assigned to | Ousmane Traore |
| Priority | 3 — Moderate |
| State | Open |
| Approval | Pending |

**Description:**  
Update Jane’s existing identity for her Operations role and remove obsolete HR access.

**Initial work note:**  
Current roster shows an Operations title with HR membership. Transfer approval and effective time must be recorded before fulfillment.

**Required evidence:**  
Before-and-after attributes, HR membership removal, Operations membership addition, and synchronized results.

### RITM0010003 — Temporary Operations Access

| Field | Value |
|---|---|
| Requested for | Karen Mills |
| Requested by | David Chen |
| Approvers | David Chen and Brian Foster |
| Request type | Temporary access |
| Duration | Five business days from the approved start date |
| Assignment group | Identity and Access Management |
| Assigned to | Ousmane Traore |
| Priority | 3 — Moderate |
| State | Open |
| Approval | Pending |

**Description:**  
Provide the minimum approved access for a temporary Operations reporting assignment, with an explicit removal task.

**Initial work note:**  
Access scope and expiry are awaiting approval. Existing Finance membership will be documented before changes.

**Required evidence:**  
Approval, access grant, expiry record, and verified removal.

### RITM0010004 — Scheduled Payroll Offboarding

| Field | Value |
|---|---|
| Requested for | Robert Hayes |
| Requested by | Sandra Torres |
| Business approver | David Chen |
| Request type | Employee offboarding |
| Assignment group | Identity and Access Management |
| Assigned to | Ousmane Traore |
| Priority | 3 — Moderate |
| State | Open |
| Approval | Pending |
| Effective time | To be confirmed by HR |

**Description:**  
Disable Robert’s identity and remove access at the approved departure time. Handle business-data retention separately.

**Initial work note:**  
Planned retirement scenario prepared. No account deletion is included in this request.

**Required evidence:**  
Disablement timestamps, AD and Entra account status, membership changes, and session-revocation records.

### SCTASK0010005 — Review JML Evidence

| Field | Value |
|---|---|
| Requested by | Marcus Johnson |
| Assigned to | Priya Patel |
| Assignment group | Security Operations |
| Task type | Post-change validation |
| State | Pending related requests |
| Related records | RITM0010001–RITM0010004 |

**Description:**  
Review the evidence for onboarding, transfer, temporary access, and offboarding. Return incomplete requests for additional work.

**Acceptance criteria:**  
Each closure claim is supported by evidence, and untested features are clearly identified.

---

## Validation Checklist

- [ ] Record business approval and effective time.
- [ ] Capture the original account state.
- [ ] Record the exact changes performed.
- [ ] Verify relevant AD attributes and memberships.
- [ ] Verify corresponding Entra ID results.
- [ ] Test resource access where configured.
- [ ] Record cloud session actions separately.
- [ ] Track temporary access removal.
- [ ] Review screenshots for sensitive information.
- [ ] Close tickets only after acceptance criteria are met.

## Evidence Plan

| Scenario | Evidence to collect |
|---|---|
| Joiner | Existing account properties and approved memberships |
| Mover | Before-and-after attributes and departmental memberships |
| Temporary access | Approval, grant, expiry, and removal |
| Leaver | Disabled status, access removal, and session actions |
| Review | Completed checklist and documented limitations |

## Suggested Repository Structure

- README.md
- images/
  - northstar-jml-banner.png
- docs/
  - fictional-scenario.md
  - validation-checklist.md
- tickets/
  - RITM0010001-joiner.md
  - RITM0010002-mover.md
  - RITM0010003-temporary-access.md
  - RITM0010004-leaver.md
- screenshots/
  - joiner/
  - mover/
  - temporary-access/
  - leaver/

---

## Scope and Limitations

- Existing account synchronization is the foundation; JML execution is not yet documented as complete.
- Group visibility does not prove resource access.
- Departmental membership does not automatically grant administrative privileges.
- Application assignments, licensing, and application sessions may require separate actions.
- Session revocation should not be described as instantly ending every application session.
- MFA, Conditional Access, automated access reviews, and lifecycle automation are possible future extensions, not completed controls in this project.

## Security and Privacy

- Use test identities and fictional business data.
- Do not include real patient information.
- Never publish passwords, tokens, private keys, or recovery codes.
- Review screenshots before uploading them.
- Record original test-account settings so the lab can be restored.

## Learning Objectives

This project is designed to strengthen my ability to:

- Manage identity changes across AD and Entra ID.
- Apply least privilege and departmental RBAC.
- Prevent access accumulation during employee transfers.
- Track temporary access through removal.
- Perform structured employee offboarding.
- Document work using service-request records.
- Distinguish configuration changes from verified outcomes.

## Completion Criteria

The pilot is complete when each approved scenario has been performed, validated, and documented with evidence.

The final results will show how NorthStar manages existing synchronized identities throughout the employee lifecycle—not only how it synchronizes them.
