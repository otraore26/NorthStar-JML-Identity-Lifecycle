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
