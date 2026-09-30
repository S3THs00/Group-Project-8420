# Part 1 – OpenEMR Use Case and Misuse Case Analysis

## Operational Environment

OpenEMR operates within a healthcare environment that includes human users, hosting infrastructure, network and security controls, patient-facing systems, external healthcare systems, and business services. These components interact with OpenEMR across different trust boundaries and may introduce security risks that must be considered when developing security requirements.

The following five use/misuse-case analyses examine essential interactions between OpenEMR and its operational environment.

---

## 1. Network and Security Environment

### Essential Interaction: Secure User Authentication and Access

The Network and Security Environment includes the Internet/LAN, firewall, TLS certificates, authentication, access control, and monitoring mechanisms that support secure communication with and access to OpenEMR.

This analysis focuses specifically on the interaction between OpenEMR and the authentication, access-control, session-security, and monitoring mechanisms within this environment. An essential interaction occurs when a user authenticates to OpenEMR and attempts to access system resources. OpenEMR verifies the user's identity, while access controls determine which functions and information the authenticated user is permitted to access.

The analysis separates security risks into two categories: **intentional/malicious misuse** and **unintentional user actions**.

### Intentional/Malicious Misuse

The primary legitimate actor is an **Authorized User** who authenticates to OpenEMR and accesses resources permitted by the user's assigned privileges.

Two intentional threat scenarios were identified:

- An **External Credential Attacker** does not possess legitimate OpenEMR access and attempts credential guessing or credential stuffing against the authentication mechanism to gain unauthorized access to an OpenEMR account.
- A **Malicious Authenticated User** represents an employee or other legitimate user who intentionally abuses authorized access by attempting to access patient information or system functions outside the privileges or legitimate purpose of the account.

#### Intentional/Malicious Use-Misuse Case Diagram

![Network and Security Environment Use-Misuse Case Diagram](OPENEMRdiagram.drawio.png)

The intentional misuse analysis identifies risks involving both external credential attacks and deliberate abuse of legitimate access. OpenEMR security functions relevant to these scenarios include multi-factor authentication, login-attempt protection, Access Control Lists (ACLs), and security audit logging.

### Unintentional User Security Risks

Authorized users may also create security risks without malicious intent. For example, an employee using a shared workstation or check-in terminal may leave an authenticated OpenEMR session unattended. Another person could then access the active session without having to authenticate independently.

This scenario differs from intentional misuse by the authorized user because the exposure results from user error rather than an attempt to circumvent OpenEMR security controls.

#### Unintentional Use-Misuse Case Diagram

**[Insert unintentional use-misuse case diagram here]**

The unintentional misuse analysis considers how OpenEMR security controls can reduce the risk created when an authenticated session is inadvertently left accessible.

### Derived Security Requirements

- **SR-1:** OpenEMR shall support multi-factor authentication for user authentication to reduce the risk of unauthorized access resulting from compromised or guessed credentials.
- **SR-2:** OpenEMR shall limit repeated failed authentication attempts by tracking failed logins and restricting further authentication attempts after a configured threshold is reached.
- **SR-3:** OpenEMR shall enforce access controls that restrict authenticated users to system functions and information permitted by their assigned roles and privileges.
- **SR-4:** OpenEMR shall record security-relevant user and authentication activity in audit logs to support monitoring, accountability, and investigation of unauthorized access.
- **SR-5:** OpenEMR shall automatically terminate an authenticated session after a configurable period of inactivity to reduce the risk of unauthorized access through an unattended workstation.

### OpenEMR Alignment

The intentional misuse analysis identified security requirements that align with functionality currently provided by OpenEMR:

- **SR-1 – Multi-Factor Authentication:** OpenEMR provides multi-factor authentication functionality, including TOTP and U2F authentication methods.
- **SR-2 – Login Attempt Protection:** OpenEMR provides brute-force login protections that can restrict repeated failed authentication attempts.
- **SR-3 – Access Control:** OpenEMR uses Access Control Lists (ACLs) to restrict access according to assigned roles and privileges.
- **SR-4 – Audit Logging:** OpenEMR provides security auditing functionality for recording security-relevant activity.
- **SR-5 – Idle Session Timeout:** OpenEMR provides a configurable idle session timeout that terminates an authenticated session after a period of inactivity, reducing the risk associated with unattended workstations.


### Sources

- [OpenEMR Multi-factor Authentication](https://www.open-emr.org/wiki/index.php/Multi-factor_Authentication)
- [OpenEMR Brute Force Login Prevention](https://www.open-emr.org/wiki/index.php/Brute_Force_Login_Prevention)
- [OpenEMR Access Controls Listing](https://www.open-emr.org/wiki/index.php/Access_Controls_Listing)
- [OpenEMR ACL Help Source Code](https://github.com/openemr/openemr/blob/master/Documentation/help_files/adminacl_help.php)
- [OpenEMR Auditing Documentation](https://www.open-emr.org/wiki/index.php/3.1_Auditing_in_OpenEMR)
- [OpenEMR Administration Globals](https://www.open-emr.org/wiki/index.php/Administration_Globals)


## 2. External Health System

**Assigned to: Erick**

### Essential Interaction

[Add completed analysis.]

### Actors and Misusers

[Add completed analysis.]

### Use/Misuse Case Diagram

[Insert final diagram.]

### Derived Security Requirements

[Add derived security requirements.]

### OpenEMR Alignment

[Add OpenEMR documentation/codebase findings.]

---

## 3. Human User

**Assigned to: Jacob**

### Essential Interaction

[Add completed analysis.]

### Actors and Misusers

[Add completed analysis.]

### Use/Misuse Case Diagram

[Insert final diagram.]

### Derived Security Requirements

[Add derived security requirements.]

### OpenEMR Alignment

[Add OpenEMR documentation/codebase findings.]

---

## 4. Hosting Environment

**Assigned to: Mai**

### Essential Interaction

[Add completed analysis.]

### Actors and Misusers

[Add completed analysis.]

### Use/Misuse Case Diagram

[Insert final diagram.]

### Derived Security Requirements

[Add derived security requirements.]

### OpenEMR Alignment

[Add OpenEMR documentation/codebase findings.]

---

## 5. Main OpenEMR Components

**Assigned to: Trey**

### Essential Interaction

[Add completed analysis.]

### Actors and Misusers

[Add completed analysis.]

### Use/Misuse Case Diagram

[Insert final diagram.]

### Derived Security Requirements

[Add derived security requirements.]

### OpenEMR Alignment

[Add OpenEMR documentation/codebase findings.]

---

## Security Requirements Summary

[Compile the security requirements derived from all five use/misuse-case analyses.]

## AI Prompt and Reflection

### AI Prompt

[Insert the prompt used to improve the use/misuse-case diagrams.]

### Reflection

[Describe how the AI response affected the diagrams and whether the suggestions were useful.]

## Team Reflection

[Compile the individual team-member reflections into the team's final reflection.]

## References

[Compile sources used by the team.]
