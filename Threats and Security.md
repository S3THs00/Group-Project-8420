# OpenEMR Threats and Security
## Threats 
OpenEMR is a world-leading open-source medical record software used by over 100,000
healthcare providers serving more than 200 million patients. 
The software stores sensitive data such as patient medical records, billing, lab results, and more, which makes it a valuable target for cyberattacks.
OpenEMR operates  in an environment that is susceptible to various security threats that healthcare organizations should encounter when they are conducting security risk assessments; 
examples of these threats are:

1. **Outdated software and vulnerabilities**
   - In a collaborated work between OpenEMR community and AISLE – autonomous , AI-native application security platform- the latest discovered 38 security vulnerabilities in the open-source software that if it exploited can lead to full database compromise, modification of the stored records, privilege escalation, and remote code execution on the server.  A discovered list of vulnerabilities included SQL injection, cross-site scripting, path traversal and session flaws.

2. **Weak or missing Access Controls**
   - One of the discoveries of AISLE that endpoints omitted Access Control List (ACL) which allowed authenticated users to reach functionalities intended for administrators.

3. **Insecure Network Configuration**
   - Missing or impropriate firewall configurations can allow an attacker to scan or directly access the OpenEMR server over the internet or local network.

4. **Insufficient Logging and Monitoring**
   - The administrator's inability to track who did what and when could lead to insider threats or outsiders making changes to the system without being detected. An example of this threat occurred in versions prior to 7.0.3.4 (CVE-2025-32967), in which changes to password events went undetected and were recorded in the client-side log viewer. The impact went beyond technical compromise to legal and operational consequences.

5. **Software supply chain threat**
   -  OpenEMR does not operate in isolation; rather, it is interconnected with system elements and other systems within the operational environment in order to achieve its tasks. Under a supply chain threat, an attacker can target the weakest link in the interconnected systems to compromise OpenEMR software or deploy techniques such as typosquatting and repo-jacking to inject malicious packages directly into the development pipeline, which can have cascading effects that can put the health organizations and patients at risk.

6. **Physical and environmental threats**
 - In an operational environment, it is possible to be under physical and environmental threats. If maintaining the OpenEMR servers locally in a data center, the servers could be subject to physical theft or events where environmental controls (HVAC, fire suppression, UPS) are not working properly. In the case of deploying the open-source software in the cloud, you do not have to worry about physical security; the cloud provider will take care of that, but you need to think about what happens if one of the cloud provider's regions goes out or is impacted by natural disasters, and how you can survive a region outage and still serve your patients.

## Security Features 
 - OpenEMR systems that generate, process, and maintain Health information must meet HIPAA/HITECH requirements and standards. The system is ONC (Office of the National Coordinator) Health IT certified and meets the same HIPAA standards to provide the same level of protection. Therefore, the security features of the system are compliant with HIPAA and align with ONC certification as follows:

1. **Role-Based Access Control**
    - The system implements the least-privilege security principle, in which you access only the minimum required information to perform tasks.
   The system defines roles for clinicians, billing, front desk, and admins; therefore, access to information is restricted to the role assigned to the user.

2. **Authentication**
  - The system enforces strong password settings
  - Integrates MFA. Both U2F and TOTP are supported by the system 
  - Supports Active Directory login 
  -  Provides Google OAuth login

3. **Encryption of Data**
  - Encryption in Transit
    - Use TLS 1.2 or 1.3 with modern ciphers for all traffic.
  - Encryption at Rest
     Use disk-level or database encryption
       - Activate MySQL/MariaDB data-at-rest encryption or operate the database on an encrypted disk
       - Has built-in encryption module to encrypt downloaded documents and file attachments.
       - Protects logs from tampering or disclosure by encrypting audit log tables.

4. **Audit logging**
- The OpenEMR aduit trails meets HIPSS logging requirements by tracking key events such as:
    a. Logins and logouts 
    b. Session timeouts
    c. Account lockouts 
    d. Patient record creation, view, update, and deletion
    e. Appointments 
    f. Authentication failures
The logs contain user ID, timestamp, patient ID, and status

5. **Session Management**
The system has an “Idle Session Timeout” that logs off users if they are inactive, thus preventing unauthorized access.

## References
+ OpenEMR Security and Compliance Guide for Healthcare[https://www.capminds.com/blog/a-definitive-guide-to-openemr-security-compliance-for-healthcare-organizations/]
+ AISLE Discovers 38 CVEs in Healthcare Software Used by 100,000 Medical Providers[https://aisle.com/blog/aisle-discovers-38-critical-security-vulnerabilities-in-healthcare-software-used-by-100000-providers]
+ OpenEMR Security Best Practices for Healthcare Providers[https://www.capminds.com/blog/5-openemr-security-best-practices-every-clinic-should-follow/]
+ Secure Electronic Health Record (EHR) System: EHR Security - UberEther[https://uberether.com/secure-ehr-system/]
+ AI Finds 38 Security Flaws in OpenEMR[https://www.darkreading.com/vulnerabilities-threats/ai-finds-38-security-flaws-openemr]
+ Healthcare Open Source Security: Risks, Compliance, and Best Practices[https://www.accountablehq.com/post/healthcare-open-source-security-risks-compliance-and-best-practices]
+ AI Finds 38 Vulnerabilities in OpenEMR Platform - Defensorum[https://www.defensorum.com/ai-vulnerabilities-openemr/]
+ Open Source Supply Chain Security Best Practices[https://www.veracode.com/blog/open-source-supply-chain-security-best-practices/]
+ CVE-2025-32967: CWE-778: Insufficient Logging in openemr openemr - Live Threat Intelligence - Threat Radar | OffSeq.com[https://radar.offseq.com/threat/cve-2025-32967-cwe-778-insufficient-logging-in-openemr-openemr-273fad]
+ OpenEMR Security and Compliance Guide for Healthcare[https://www.capminds.com/blog/a-definitive-guide-to-openemr-security-compliance-for-healthcare-organizations/]
+ OpenEMR HIPAA Compliance: Security Features, Hosting Requirements, and BAA Checklist[https://www.accountablehq.com/post/openemr-hipaa-compliance-security-features-hosting-requirements-and-baa-checklist]

 
       - 




