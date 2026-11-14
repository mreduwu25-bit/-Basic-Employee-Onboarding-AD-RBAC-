# Basic Employee Onboarding (AD)(RBAC)

## Problem Statement
Northstar Medical Group (NMG) had been left with a poorly managed network by its previous managed service provider (MSP), which never built a proper Active Directory environment. There was no organizational structure, so employee accounts weren't grouped by department and nobody could say who had access to what. Onboarding was a manual, ad hoc process, which made it easy to put a new hire in the wrong place or give them the wrong access. For a healthcare organization this is a HIPAA risk: without role-based, least-privilege access, staff can reach patient data their job doesn't require, and there is no clean way to audit it.

## Solution Overview
I rebuilt NMG's identity environment from scratch in a VirtualBox lab. I created the `NMG.com` domain and promoted a Windows Server to domain controller (`WIN-ADMHU4BNNFE`), then verified its health with `dcdiag`. I designed a department-based Organizational Unit (OU) structure with four OUs: Finance, HR, IT and Operations. Each OU has its own security group (`Finance-Users`, `HR-Users`, `IT-Users`, `Operations-Users`), and access is granted through group membership instead of per-user permissions. This is a flat RBAC model: one role per department, with no nested groups. I then provisioned 15 user accounts with a consistent naming convention, placed each in its department OU and added it to the matching group. When ticket NMG-0047 exposed an access problem, I traced it to its causes, fixed it and documented the resolution.

## Video Walkthrough
Video walkthrough: _link coming soon_

## Tools Used
* Windows Server
* Active Directory Domain Services (AD DS)
* VirtualBox
* Group Policy
* GitHub

## Project Timeline
* **Day 1:** Domain creation and domain controller promotion
* **Day 2:** Organizational unit and security group design
* **Day 3:** User provisioning and RBAC implementation
* **Day 4:** Incident response and resolution (NMG-0047)
* **Day 5:** Documentation and case study packaging

## Key Accomplishments
* Built the NMG.com domain from scratch
* Designed a department-based OU structure (Finance, HR, IT, Operations)
* Implemented RBAC with security groups mapped to each department
* Provisioned 15 user accounts with consistent naming conventions and attribute standards
* Diagnosed and resolved a multi-cause access issue (wrong OU + missing group membership)
* Documented the full incident resolution with root cause analysis

## RBAC Model at a Glance

| Department | OU | Security Group | Users |
|---|---|---|---|
| Finance | `OU=Finance,DC=NMG,DC=com` | `Finance-Users` | 4 |
| HR | `OU=HR,DC=NMG,DC=com` | `HR-Users` | 4 |
| IT | `OU=IT,DC=NMG,DC=com` | `IT-Users` | 4 |
| Operations | `OU=Operations,DC=NMG,DC=com` | `Operations-Users` | 3 |

The full table, with usernames and access levels, is in [`Documentation/RBAC-Structure.md`](Documentation/RBAC-Structure.md).

## Repository Structure

| Folder | Contents |
|---|---|
| [`Documentation/`](Documentation) | Design documentation: RBAC structure, domain configuration, security group design and user list |
| [`Incident-Reports/`](Incident-Reports) | Write-up of ticket NMG-0047, including root cause analysis |
| [`Screenshots/`](Screenshots) | Lab evidence for Days 1 to 4, named by day (e.g. `Day1_Dcdiag_Results.jpg`, `Day4_JCooper_Wrong_OU.jpeg`) |
