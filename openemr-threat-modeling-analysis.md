

## Team Members

- Seth Stutzman
- Mai Abdalla
- Trey Moore
- Jacob Linke
- Erik Osmera

---

# Part 1 – Threat Modeling

## Overview

For this assignment, the team developed Data Flow Diagrams (DFDs) representing critical data flows associated with the OpenEMR security scenarios examined in our previous Security Requirements and Assurance Case assignments.

The DFDs were developed and analyzed using the Microsoft Threat Modeling Tool. Automatically generated threats were reviewed using the STRIDE threat categories:

- Spoofing
- Tampering
- Repudiation
- Information Disclosure
- Denial of Service
- Elevation of Privilege

Particular attention was given to interactions crossing trust boundaries. Identified threats were reviewed to determine whether OpenEMR contains relevant mitigation mechanisms and whether sufficient evidence exists to consider those threats mitigated.

---

# DFD 1 – Authentication and Authorized Resource Access

## Scenarios Covered

This DFD supports the team's OpenEMR scenarios involving:

- Unauthorized access prevention
- User authentication
- Multi-factor authentication
- Authorization and privilege enforcement
- Patient and clinical resource access

The DFD relates to scenarios previously examined by:

- **Seth** – Unauthorized Access / Authentication and Authorization
- **Jacob** – Physician MFA
- **Trey** – Patient MFA
- **Mai** – Nurse Authorization / Patient Record Access

---

## DFD Description

The Authentication and Authorized Resource Access DFD models how an OpenEMR user authenticates to the application and subsequently requests access to protected OpenEMR resources.

The **OpenEMR User** exists outside the **Internet Trust Boundary** and communicates with the **OpenEMR Web Application** using HTTPS.

Authentication information is passed to the **Authentication and MFA** process. Authentication data needed to validate the user is retrieved from the **OpenEMR Patient and User Database**, and the resulting authentication status is returned to the web application.

After authentication, protected resource requests are sent to the **Authorization and Access Control** process. The authorization process determines whether the authenticated user is permitted to access the requested information before retrieving patient or clinical data from the database.

Authorized information is then returned through the OpenEMR Web Application to the user over HTTPS.

---

## DFD Components

### External Interactor

**OpenEMR User**

Represents a person attempting to authenticate to OpenEMR and access protected application resources.

### Processes

**OpenEMR Web Application**

Receives requests from the user and coordinates authentication and protected-resource access.

**Authentication and MFA**

Represents the authentication process, including credential validation and applicable multi-factor authentication.

**Authorization and Access Control**

Represents authorization decisions that determine whether an authenticated user is permitted to access a requested OpenEMR resource.

### Data Store

**OpenEMR Patient and User Database**

Represents stored authentication, user, patient, and clinical information required by the modeled processes.

### Trust Boundary

**Internet Trust Boundary**

Separates the external OpenEMR user from the OpenEMR application environment.

---

## Data Flows

The DFD contains the following data flows:

1. `HTTPS: Login and Resource Request`
2. `Credentials and MFA Response`
3. `Authentication Data Request`
4. `Authentication Data`
5. `Authentication Result`
6. `Authenticated Resource Request`
7. `Authorized Data Request`
8. `Patient and Clinical Data`
9. `Authorized Resource Response`
10. `HTTPS: OpenEMR Response`

The two HTTPS flows cross the Internet Trust Boundary.

---

## DFD Diagram

![OpenEMR Authentication and Authorized Resource Access DFD](OpenEMR_Authentication_DFD.PNG)

---

## Microsoft Threat Modeling Tool Analysis

The Microsoft Threat Modeling Tool generated **23 potential threats** for the Authentication and Authorized Resource Access DFD.

### Threat Summary

| Status | Count |
|---|---:|
| Not Started | 0 |
| Not Applicable | 0 |
| Needs Investigation | 23 |
| Mitigation Implemented | 0 |
| **Total** | **23** |

Each automatically generated threat was reviewed to determine whether OpenEMR provides a relevant security control and whether sufficient evidence exists to classify the threat as mitigated.

Although OpenEMR provides numerous security controls applicable to the identified threats, the analysis determined that additional implementation, configuration, or security-testing evidence would be necessary to demonstrate complete mitigation.

Therefore, all 23 threats were retained as **Needs Investigation**.

---

## Threat Review

The generated threats addressed risks involving:

- User spoofing
- Authentication and identity impersonation
- Database spoofing
- Excessive resource consumption
- Cross-Site Request Forgery
- Modification of application execution flow
- Remote code execution
- Interruption of requests and responses
- Application availability
- Repudiation
- Weak access controls
- Authorization-related privilege escalation
- Protection of patient and clinical information

OpenEMR contains controls relevant to many of these threats. These include authentication and MFA capabilities, failed-login protections, session-management controls, access-control mechanisms, CSRF protections, auditing, and application-security controls.

However, the existence of a security mechanism does not by itself demonstrate that the mechanism is correctly configured and consistently enforced throughout every applicable OpenEMR workflow.

For this reason, the team avoided classifying threats as **Mitigation Implemented** solely because a corresponding security feature exists.

---

## Full TMT HTML Report

[OpenEMR Authentication and Authorized Resource Access – Full TMT Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/S3THs00/Group-Project-8420/refs/heads/main/OpenEMR_Authentication_Threat_Model_Report.htm)

---

# DFD 2 – External Pharmacy Prescription Exchange

## Scenario Covered

- ePrescription / External Pharmacy communication

**Primary contributor: Erik Osmera**

---

## DFD Description

The External Pharmacy Prescription Exchange DFD models prescription and refill transactions between an external pharmacy/ePrescribing service and OpenEMR.

A Pharmacy Technician initiates a prescription or refill action through the External Pharmacy/ePrescribing Service. The external service sends the prescription or refill request to the OpenEMR Web Interface over HTTPS, crossing the Internet Trust Boundary. The web interface passes the authenticated prescription transaction to the OpenEMR Prescription Processing Service.

The Prescription Processing Service reads from and writes to the OpenEMR Patient and Prescription Database and records relevant activity in the OpenEMR Audit Log Database. The resulting prescription or refill response is returned through the OpenEMR Web Interface to the external pharmacy/ePrescribing service over HTTPS.

---

## DFD Diagram

![OpenEMR External Pharmacy Prescription Exchange DFD](Erik_OpenEMR_Authentication_DFD.PNG)

---

## Microsoft Threat Modeling Tool Analysis

Erik's Microsoft Threat Modeling Tool analysis identified **21 potential threats**.

### Threat Summary

| Status | Count |
|---|---:|
| Not Started | 0 |
| Not Applicable | 3 |
| Needs Investigation | 16 |
| Mitigation Implemented | 2 |
| **Total** | **21** |

The threat model identified several important risks associated with the external pharmacy workflow. These included spoofing of the external pharmacy/ePrescribing service, unauthorized access to prescription data, repudiation of prescription transactions, interruption of prescription requests or responses, SQL injection, cross-site scripting, and excessive resource consumption.

Authentication and authorization of external pharmacy systems are important because an attacker impersonating a trusted pharmacy could attempt unauthorized prescription or refill transactions. OpenEMR should also validate trusted pharmacy endpoints and TLS certificates before returning prescription information. Audit logging should record the source or destination, timestamp, affected prescription or patient record, transaction identifier, and result to provide accountability for disputed transactions.

Two threats were classified as Mitigation Implemented. Cross-site scripting is addressed through OpenEMR secure-coding guidance requiring output encoding of user-controlled data, while SQL injection against the patient and prescription database is addressed through parameterized queries and bound parameters. Most remaining threats were classified as Needs Investigation because implementation, configuration, or testing evidence would still be required to verify the mitigation for this specific workflow.

Three automatically generated threats were classified as Not Applicable. Two involved operating-system-level impersonation between modeled processes, while the third involved shared process memory or executable references. These behaviors are not represented by this Level 1 OpenEMR model, which exchanges application data between the Web Interface and Prescription Processing Service.

---

## Full TMT HTML Report

[OpenEMR External Pharmacy Prescription Exchange – Full TMT Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/S3THs00/Group-Project-8420/refs/heads/main/Full.Report.Pharmacy.TMT.htm)

---

# Additional Team Threat-Modeling Analysis

The Authentication and Authorized Resource Access DFD covers several of the team's previously developed security scenarios. Team members should add findings from their individual analysis that are not already represented above.

# DFD 3 – Nurse Authorization / Patient Record Access

## Scenario Covered
- Nurse interaction with the OpenEMR portal to access patient records, encounter documents, and  prescriptions

**Primary contributor: Mai Abdalla**

---

## DFD Description

The threat model shows a level 2 diagram of the interaction between the nurse (external interactor/entity) and the OpenEMR Patient Portal. The data flow diagram is based on the use/misuse case scenario.


The way the nurse interacts with the portal is by requesting patient information (Over HTTPS); for example, the nurse could retrieve a patient record if that patient is assigned to the nurse. Retrieve encounter documents and display a list of encounter forms that can be added to the encounter document. Some of these encounters may have a sensitivity label, so an additional authorization check should be performed to ensure the nurse has the sensitivity label, in addition to the ability to enter prescription information.

## DFD Diagram 
![OpenEMR Nurse Authorization DFD](https://github.com/user-attachments/assets/997c30b4-9ced-45fd-9142-ecc3aef8d0e3)


## Microsoft Threat Modeling Tool Analysis

Mai's Microsoft Threat Modeling Tool analysis identified **26 potential threats**.

### Threat Summary

| Status | Count |
|---|---:|
| Not Started | 0 |
| Not Applicable | 4 |
| Needs Investigation | 0 |
| Mitigation Implemented | 22 |
| **Total** | **26** |


For each of the threats identified by the tool, I tried to provide suggested mitigation strategies by consulting documents such as CWE (Weaknesses in the 2025 CWE Top 25 Most Dangerous Software Weaknesses), which covers weaknesses such as improper input validation, incorrect Authorization, improper access control, and missing authentication, which are weaknesses that OpenEMR suffers from and that allow threats (identified by the tool) to take advantage. The other documentation I used is the OWASP Cheat Sheet Series, which covers good information about the cross-site request forgery identified by the tool.

Some of the threats related to elements interacting outside the trust boundary include cross-site request forgery and spoofing, in which the nurse can pretend to be someone else. In addition to these threats that can emerge outside the boundary, two were interesting: remote code execution and improper data that can be passed to change the flow of the program; both can come from an external entity. 

The CWE documentation provides possible mitigations in the phases of the SDLC: Architecture and Design, implementation, operation, and system configuration. For example, to mitigate remote code execution during the implementation phase, you apply input validation; during system configuration, you assign permissions that prevent the user from accessing or opening files.

Of course, additional mitigations mentioned in the OpenEMR documentation are role-based access control, audit logging, and MFA. Mentioning MFA, pointing to the security requirement we did, this security control needs improvement; what we suggest is to use WebAuthn/FIDO2 authentication methods and force it in the patient portal

---

## Full TMT HTML Report
[Nurse-Authorization-Full-Report](https://github.com/user-attachments/files/35190523/Nurse_Interaction_Threat_Modeling.htm)

---

# DFD 4 – Patient MFA Access

## Scenario Covered

- Patient access to a patient portal and the MFA authentication with it

**Primary contributor: Trey Moore**

---

## DFD Description

The Patient Multi-Factor Authentication (MFA) DFD models the authentication and identity verification process between a patient and the OpenEMR Patient Portal.

A patient initiates a login request through the OpenEMR Patient Portal by entering their username and password. The login credentials are transmitted to the OpenEMR Authentication Service over HTTPS, crossing the Internet Trust Boundary. The Authentication Service validates the credentials against the OpenEMR User Authentication Database before initiating an MFA verification request.

The MFA Authentication Service generates a verification challenge and communicates with the patient's registered authentication method, such as an authenticator application or one-time passcode service. The patient submits the required verification response through the OpenEMR Patient Portal, which forwards it to the MFA Authentication Service for validation.

Upon successful verification, the Authentication Service establishes an authenticated session and grants the patient access to authorized resources within the OpenEMR Patient Portal. Authentication attempts, MFA verification results, and relevant security events are recorded in the OpenEMR Audit Log Database. If authentication fails, access is denied and the unsuccessful attempt is logged.

---

## DFD Diagram

![OpenEMR Patient MFA DFD](https://github.com/user-attachments/assets/743ede30-daf8-47f9-86c0-b91f29850e51)


---

## Microsoft Threat Modeling Tool Analysis

The OpenEMR Patient Multi-Factor Authentication (MFA) threat analysis identified **18 potential threats** using the STRIDE threat modeling methodology.

### Threat Summary

| Status | Count |
|---|---:|
| Not Started | 0 |
| Not Applicable | 0 |
| Needs Investigation | 18 |
| Mitigation Implemented | 0 |
| **Total** | **18** |

The threat model identified several important risks associated with patient authentication and MFA verification. These included spoofing of patient identities, interception or replay of MFA verification codes, unauthorized modification of registered authentication methods, exposure of authentication credentials, denial-of-service attacks against authentication services, and elevation of privilege through MFA bypass or account recovery vulnerabilities.

Authentication and verification of patient identities are important because an attacker who compromises login credentials or intercepts MFA verification codes could gain unauthorized access to sensitive electronic protected health information (ePHI). To mitigate these risks, OpenEMR should implement secure authentication mechanisms such as WebAuthn/FIDO2, enforce rate limiting on authentication attempts, and use encrypted HTTPS connections for communication between the patient portal and authentication services. MFA enrollment and recovery processes should also require additional identity verification to prevent unauthorized changes to registered authentication methods.

The model also identified risks associated with session management, authentication logging, and service availability. OpenEMR should ensure that successful MFA verification is required before granting authenticated access and that authorization checks continue to restrict patients to their own medical records. Audit logs should record authentication attempts, MFA verification results, account recovery activities, timestamps, and relevant user identifiers to support accountability and security investigations.

All 18 threats were classified as **Needs Investigation** for reporting purposes because the proposed mitigations require additional implementation, configuration, or testing evidence before they can be considered effective. No threats were classified as Mitigation Implemented or Not Applicable at this stage. Further testing is necessary to verify that MFA enforcement, account recovery protections, session management, and access controls adequately protect patient information within the OpenEMR environment.

## Full TMT HTML Report

[OpenEMR Patient MFA – Full TMT Report](https://github.com/user-attachments/files/35186838/OpenEMR_Patient_MFA_Threat_Model.1.html)



# DFD 5 - Physician MFA

## Scenario Covered

- Physician utilizing MFA to access EHR portal to view and edit patient health information.

**Primary contributor: Jacob Linke**

---

## DFD Description

The physician outside the application trust boundary obtains authentication via credentials and multi-factor authentication (MFA) through an EHR portal and authentication service backed by a credential store. Once verified, the EHR portal crosses a data boundary to query and retrieve patient medical history records from a dedicated database.

---

## DFD Diagram

<img width="1249" height="694" alt="image" src="https://github.com/user-attachments/assets/c958fdcd-c76e-4b6c-b4a8-923bc750181e" />

---

## Microsoft Threat Modeling Tool Analysis

Jacob's Microsoft Threat Modeling Tool analysis identified **37 potential threats**.

### Threat Summary

| Status | Count |
|---|---:|
| Not Started | 0 |
| Not Applicable | 0 |
| Needs Investigation | 29 |
| Mitigation Implemented | 8 |
| **Total** | **37** |

The threat model identified key risks associated with a physician using multi-factor authentication (MFA) in OpenEMR to access patient medical history records. These included spoofing of users or internal/data components, session hijacking or replay attacks, SQL injection, web injection/defacement or phishing, exposure of sensitive credentials or configuration data, database tampering or anomalous activity, and repudiation of record accesses.

Strong authentication and MFA enforcement are essential so an attacker cannot impersonate a physician or bypass login controls to view sensitive patient records. OpenEMR and its surrounding web and database tiers should enforce valid TLS certificates, authenticated service/database connections, and boundary isolation so credentials, session tokens, and patient history data remain protected in transit and across trust boundaries. Audit logging should capture authentication events, MFA verification outcomes, and patient record queries to support accountability and traceability.

Verified controls such as active MFA enrollment and TLS/transport protection can be marked as mitigated where confirmed in the deployment, while most remaining threats are classified as needing investigation until version-specific code, web-server headers, session/cookie settings, and database configurations are verified.

---

## Full TMT HTML Report

[2026.11.20.Linke.-.Threat.Report.htm](https://github.com/user-attachments/files/35192529/2026.11.20.Linke.-.Threat.Report.htm)# OpenEMR Threat Modeling Analysis



---

# Part 2 – Observations

## OpenEMR Security Mitigation Review

The team reviewed OpenEMR to determine whether security controls expected from the DFD-based threat analysis were present.

OpenEMR provides numerous security mechanisms relevant to threats identified during the analysis, including authentication controls, multi-factor authentication, failed-login protections, session-management controls, role- and privilege-based access controls, CSRF protections, auditing capabilities, and API authentication and authorization controls.

However, the existence of a security mechanism does not by itself demonstrate that every applicable threat is completely mitigated. Some controls depend on deployment configuration, while others must be consistently enforced throughout the application.

For this reason, threats were not classified as fully mitigated without sufficient supporting evidence.

---

## Authentication and MFA

OpenEMR provides authentication mechanisms and supports MFA. It also contains protections associated with repeated failed authentication attempts.

These mechanisms help address spoofing and authentication-related threats identified in the DFD. However, MFA can depend on configuration and enrollment rather than necessarily being universally enforced for every OpenEMR user and deployment.

This demonstrates an important difference between a **security capability being available** and a **security requirement being consistently enforced**.

---

## Authorization and Patient Data Access

OpenEMR implements access-control mechanisms designed to restrict application functionality and access to protected clinical information according to user permissions.

These mechanisms are relevant to threats involving unauthorized access to patient and clinical data. However, access-control mechanisms must be correctly configured and consistently enforced at applicable application endpoints.

The team's analysis therefore determined that authorization-related threats require verification rather than assuming that the presence of an access-control framework completely mitigates unauthorized-access risks.

---

## Input Validation and Application Security

The threat model identified risks involving malicious input, modification of application execution, and potential remote code execution.

Although OpenEMR contains security mechanisms intended to reduce these risks, implementation-level vulnerabilities can still occur. OpenEMR security advisories demonstrate that security vulnerabilities can require remediation even when broader security frameworks and controls exist.

Input validation, secure coding practices, source-code review, vulnerability testing, and penetration testing therefore remain important methods of verifying these mitigations.

---

## CSRF and Session Security

OpenEMR includes mechanisms for protecting authenticated sessions and preventing Cross-Site Request Forgery (CSRF).

The effectiveness of these controls depends on their consistent implementation throughout applicable application functionality. The existence of a CSRF protection mechanism, for example, does not independently establish that every applicable state-changing operation properly enforces that protection.

The associated threats therefore require verification rather than automatically being considered fully mitigated.

---

## Auditing and Repudiation

OpenEMR provides auditing and logging capabilities for security-relevant activity.

These mechanisms can help provide accountability for authentication and protected-resource activity. However, the effectiveness of auditing depends on which events are recorded, the information contained in those records, system configuration, and protection of the audit information.

Audit-log verification would therefore be necessary to establish whether all modeled activities provide sufficient accountability to address repudiation threats.

---

## Availability and Resource Consumption

The threat model identified denial-of-service risks involving excessive authentication or database requests, application resource exhaustion, and interruption of HTTPS communications.

OpenEMR includes controls relevant to some of these threats, including protections associated with repeated failed authentication attempts. These mechanisms can reduce specific forms of abusive authentication activity but do not establish complete protection against application-level, database-level, network-level, or infrastructure-level denial-of-service attacks.

Deployment-specific protections such as server configuration, network controls, resource limits, monitoring, and availability architecture would need to be examined before these threats could be considered fully mitigated.

---

## Trust Boundary Observations

Particular attention was given to interactions crossing trust boundaries.

In the Authentication and Authorized Resource Access DFD, the user's login and resource request enters OpenEMR across the **Internet Trust Boundary**. The resulting OpenEMR response crosses the same boundary when information is returned to the user.

HTTPS/TLS provides important protection for information while it is transmitted. However, transport encryption alone does not eliminate threats involving:

- Compromised credentials
- User impersonation
- Malicious requests
- Session misuse
- Denial of service
- Application vulnerabilities

This demonstrates the importance of applying multiple complementary security controls to interactions crossing a trust boundary.

## External Pharmacy Trust-Boundary Observations

The most important trust-boundary interaction in the External Pharmacy DFD is the exchange between the External Pharmacy/ePrescribing Service and the OpenEMR Web Interface. Both the prescription/refill request entering OpenEMR and the response returning to the pharmacy cross the Internet Trust Boundary using HTTPS.

HTTPS/TLS protects prescription information while it is transmitted, but transport encryption alone does not establish that the external system is authorized to perform a requested prescription operation. OpenEMR must still authenticate the external pharmacy, enforce authorization after the request enters the trust boundary, and validate the destination before returning prescription information.

The boundary also makes auditing important because activity originating outside OpenEMR's direct control should be tied to an authenticated external identity and a specific transaction. Interrupted requests or responses should also be detected and logged so an incomplete prescription transaction is not treated as successfully completed.

---

## Identified Gaps

The primary gap identified during the review was not necessarily the absence of security mechanisms, but the difficulty of demonstrating that those mechanisms are **configured, consistently enforced, and effective for every applicable OpenEMR workflow**.

OpenEMR contains controls addressing many of the STRIDE threats generated by the Microsoft Threat Modeling Tool. However, additional evidence would be required before the team could confidently classify all applicable threats as fully mitigated.

Useful additional evidence could include:

- Authentication and MFA enforcement testing
- Authorization and access-control testing
- Configuration reviews
- Source-code review
- Penetration testing
- Audit-log verification
- Testing with malformed requests
- Testing with excessive requests
- Verification

## Contribution and Reflections

Erik

My main contribution was the External Pharmacy Prescription Exchange threat model. I built the Level 1 DFD showing how prescription and refill transactions move from an external pharmacy/ePrescribing service into OpenEMR, through the prescription processing service, and into the prescription and audit databases. I then analyzed the model in Microsoft Threat Modeling Tool, reviewed the 21 generated threats, documented mitigation or investigation notes for each one, and generated the final HTML report. I also reviewed the trust boundary between the external pharmacy and OpenEMR and documented the authentication, authorization, auditing, and transaction-integrity concerns that came out of that analysis.

The biggest thing I learned from this assignment was how much the way you build the DFD affects the threat analysis that comes out of it. Choosing a Web Service instead of a generic external entity, defining the correct data flows, and placing the trust boundary correctly all changed what TMT looked for. I also learned that the threats automatically generated by a tool still need to be reviewed in context. A few of the threats TMT generated involved things like shared process memory or operating-system impersonation that did not really apply to the OpenEMR workflow I was modeling.

---

Trey

My main contribution to this project was developing the Patient Multi-Factor Authentication (MFA) threat model for OpenEMR. I built the Level 1 DFD illustrating how a patient authenticates through the OpenEMR Patient Portal, including the initial login request, MFA verification process, communication with authentication services, and access to patient records following successful verification. I also analyzed the potential security threats associated with this process using the STRIDE methodology, focusing on risks such as identity spoofing, MFA bypass, unauthorized access, and exposure of sensitive patient information. Additionally, I reviewed Mai's DFD and provided feedback on the data flows, trust boundaries, and potential security concerns to help ensure the model accurately represented its intended workflow.

One of the biggest things I learned from this assignment was how important it is to accurately represent the interactions between different components of a system when developing a threat model. Even small decisions about where to place trust boundaries or how to define data flows can significantly impact the threats identified during analysis. I also gained a better understanding of the additional security considerations involved in implementing MFA, particularly around account recovery, authentication methods, and preventing attackers from bypassing verification requirements.

I also want to acknowledge the contributions and support of my group members throughout this project. They were extremely helpful in walking me through parts of the threat modeling process that I was less familiar with and helping me better understand how to use Microsoft Threat Modeling Tool effectively. I was also on vacation this past weekend, which limited the amount of time I was able to dedicate to the project during that period. My group members were understanding and helped pick up some of the additional work while I was unavailable. I appreciate their willingness to help me work through challenges, answer my questions, and keep the project moving forward. Overall, this assignment helped me develop a stronger understanding of threat modeling while also reinforcing the importance of communication, collaboration, and accountability when working on a team project.

---
Mai 

A fun fact about finding possible mitigations for identified threats: I would thank Dr. Hale for this, especially when he opened Modules 13, 14, and 15, which cover CWE. I was curious to open the module and see what it was about, which led me to the CWE website, which I found helpful for understanding different mitigations that can be implemented at different phases of software development. 

I liked the idea of understanding the main components of a system and how they communicate with each other, how the outside world interacts with them, how data flows among system components and external entities, and how security considerations change as trust levels change. 

I was curious to play around with the tool and understand how the configuration attributes of the elements can either mitigate a threat or generate a new one. For example, in my diagram I had a process called patient portal; this element had attributes I could set to yes or no, such as implementing authentication or implementing authorization. When I set them to yes and ran an analysis view, the tool showed more threats, including weak authentication, collision attacks, and replay attacks. I guess part of this assignment is evaluating whether such threats are relevant to your component; otherwise, you spend a great deal of time trying to mitigate threats that may not be relevant.

---
Jacob

One thing that I discovered was the full complexity of possible threats that are present in systems that look simple. Many of the threats that the Threat Summary tool identified were types of things that I had not heard of before, I had to look up what they were. 
I found the Getting started with the Threat Modeling Tool page useful as when I first went into analysis view, the program did not generate any threats, and I had to change the objects in my diagram manually, something that I would not have known to do. 
