# NorthStar Medical Group — Identity Lifecycle Management
<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-JML-Identity-Lifecycle/blob/b6a2af8c5737dc3a2b59c5ab18224b694dbca1de/Images/NorthStar%20Medical%20Identity%20Lifecycle.png">

**Joiner • Mover • Leaver | Active Directory • Microsoft Entra ID**

A hands-on home lab exploring how employee access is provisioned,
updated, and removed in a hybrid identity environment.

> NorthStar Medical Group is a fictional organization. All employees,
> business events, approvals, and service requests are simulated.

## Overview

NorthStar Medical Group uses the on-premises Active Directory domain
**NMGM.COM**, synchronized with Microsoft Entra ID through
**Microsoft Entra Connect Sync**.

This project builds on that foundation by introducing three employee
lifecycle scenarios: onboarding a new hire, transferring an employee
between departments, and offboarding a departing employee.

Acting as the IAM administrator, I review simulated requests, perform
approved changes in the lab, and document verification results.

## NorthStar Service Desk

The NorthStar Service Desk is an independent ticketing simulator
used to organize the project’s lifecycle requests.

### [Open the NorthStar Service Desk →](https://northstar-jml-desk-ousmane.royalrook4096.chatgpt.site)

The simulator supports:

- Reviewing and editing lifecycle requests.
- Recording simulated approvals and request statuses.
- Tracking fulfillment checklists.
- Adding work notes and closure details.
- Exporting ticket records for project documentation.

> The simulator does not connect to ServiceNow, Active Directory,
> or Entra ID. Identity changes are performed separately in the lab.
> Ticket progress is saved in the visitor’s browser.
> Access to the hosted simulator depends on its sharing settings.

## Ticket Dashboard

Three requests arrive in the IT service queue: a new hire, a department
transfer, and an employee departure.

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-JML-Identity-Lifecycle/blob/e4a44e66d6e8e7bfe219dd39e5bdfc630cda6047/Images/Northstar-JML-Ticket-Dashboard.png">


*The simulated service desk tracks Sarah Johnson’s onboarding,
James Whitfield’s transfer to Finance, and Lisa Park’s offboarding.
All three requests are open and awaiting simulated approval.
This dashboard supports tracking request status, documenting work,
and organizing verification evidence throughout the identity lifecycle.
automatically reflect changes made in the simulator.*

## Joiner — Sarah Johnson

### Business Request

Sarah Johnson is joining HR as a **Talent Acquisition Specialist**.
She will coordinate interviews, manage candidate records, and support
hiring managers.

She requires an employee account and approved access to HR and
recruiting resources before her first day.

**Ticket:** RITM0010048  
**Manager:** Sandra Torres — HR Manager

### Planned Actions

- Review the simulated onboarding request and approval.
- Check for an existing account to avoid duplicate identities.
- Create Sarah’s account in the HR OU within NMGM.COM.
- Set her department, job title, and manager.
- Assign HR-Users membership.
- Verify account and membership synchronization to Entra ID.
- Test approved access to configured lab resources.

### Verification Evidence

Document the AD account properties, HR-Users membership,
synchronized Entra ID account, and resource-access test results.

[View the Joiner walkthrough](docs/joiner.md)

## Mover — James Whitfield

### Business Request

James Whitfield is transferring from **HR Recruiter** to
**Finance Coordinator**, reporting to **David Chen, Finance Manager**.

His new responsibilities include coordinating invoice documentation,
maintaining financial records, and supporting Finance operations.

His access must reflect his new responsibilities. Previous HR access
must be removed unless a specific, time-limited exception is approved.

**Ticket:** RITM0010049  
**Department Change:** HR → Finance  
**Group Change:** HR-Users → Finance-Users

### Planned Actions

- Review the simulated transfer request and manager approvals.
- Record existing account attributes and group memberships.
- Update department to Finance.
- Update job title to Finance Coordinator.
- Update manager to David Chen.
- Move the account from the HR OU to the Finance OU.
- Remove HR-Users membership and add Finance-Users membership.
- Review any other access associated with the previous role.
- Verify synchronized attributes and memberships in Entra ID.
- Test Finance access and removal of previous HR access.

> Moving an account to another OU does not automatically change
> its security group memberships. These changes must be performed
> and verified separately.

### Verification Evidence

Capture account attributes and memberships before and after the
transfer. Document synchronization results and access checks.

[View the Mover walkthrough](docs/mover.md)

## Leaver — Lisa Park

### Business Request

In this scenario, Lisa Park is leaving the Operations department.
HR requests that her access end at the approved departure time.

Offboarding requires coordinated access removal across the
on-premises and cloud environments.

**Ticket:** RITM0010050  
**Requested By:** Sandra Torres — HR Manager

### Planned Actions

- Review HR authorization and the effective departure time.
- Verify Lisa’s account, department, and existing access.
- Record any retention or information-transfer requirements.
- Disable her AD account at the approved time.
- Verify the disabled account state in Entra ID after synchronization.
- Revoke cloud sign-in sessions.
- Review and remove remaining group and application access.
- Verify that new sign-ins are blocked.
- Document outstanding application-session limitations or follow-up work.

### Verification Evidence

Document disabled account states, session-revocation actions,
access-removal results, and sign-in checks.

[View the Leaver walkthrough](docs/leaver.md)

## Lab Environment

| Component | Purpose |
|---|---|
| Windows Server / Active Directory Domain Services | On-premises account and group administration |
| NMGM.COM | Active Directory domain |
| Microsoft Entra ID | Cloud identity management |
| Microsoft Entra Connect Sync | Synchronization between AD and Entra ID |
| Departmental Security Groups | Role-based access assignments |
| NorthStar Service Desk | Simulated requests, approvals, and work notes |

## Documentation and Evidence

| Location | Contents |
|---|---|
| `README.md` | Project overview, scenarios, and ticket dashboard |
| `docs/joiner.md` | Onboarding walkthrough and verification |
| `docs/mover.md` | Department-transfer walkthrough and verification |
| `docs/leaver.md` | Offboarding walkthrough and verification |
| `images/` | Project banner and lab screenshots |
| `tickets/` | Exported simulated ticket records |

Each walkthrough will document the request, actions performed,
verification results, and any troubleshooting or limitations.

Screenshots will include captions explaining what they demonstrate.
Planned actions will remain separate from completed and verified work.

## Project Progress

- [x] Define the fictional JML scenarios.
- [x] Prepare the NorthStar Service Desk simulator and scenario tickets.
- [ ] Complete and verify Sarah’s onboarding.
- [ ] Complete and verify James’s department transfer.
- [ ] Complete and verify Lisa’s offboarding.
- [ ] Add screenshots and detailed walkthroughs.
- [ ] Export completed ticket records.

## Learning Objectives

- Manage employee identities across AD and Entra ID.
- Apply least privilege during onboarding and role changes.
- Prevent unnecessary access from accumulating after transfers.
- Coordinate account disablement and access removal.
- Verify synchronization and distinguish it from resource-access testing.
- Maintain clear technical documentation and ticket records.

## Previous Projects

This project builds on two earlier home labs:

1. **[Basic Employee Onboarding — Active Directory and RBAC](https://github.com/otraore26/Basic-Employee-Onboarding-AD-RBAC-)**  
   Established departmental organizational units, employee accounts,
   and security groups.

2. **[NorthStar Hybrid Identity — AD to Entra ID Synchronization](https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync)**  
   Connected on-premises Active Directory to Microsoft Entra ID
   and verified synchronized users and groups.

## Author

**Ousmane Traore**


























































































































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
