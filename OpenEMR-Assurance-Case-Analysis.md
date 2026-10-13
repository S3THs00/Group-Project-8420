# OpenEMR Security Assurance Case Analysis

## Part 1 – Assurance Case

### Unauthorized Access Assurance Case

**Top-Level Claim C1:** OpenEMR sufficiently prevents unauthorized access to protected system resources.

This assurance case provides an argument and supporting evidence that OpenEMR sufficiently prevents unauthorized access to protected system resources. The argument addresses three primary concerns: repeated credential-guessing and credential-stuffing attempts, compromised user passwords, and authenticated users accessing resources beyond their assigned privileges.

### Assurance Case Diagram

![OpenEMR Unauthorized Access Assurance Case](Assurance%20Case.png)

### Argument Summary

The top-level claim is supported by two sub-claims. The first addresses unauthorized users attempting to gain access through protected user accounts. The second addresses authenticated users attempting to access resources outside their authorized privileges.

The assurance case considers three rebutting defeaters:

- **R1:** Unless an attacker succeeds through repeated credential-guessing or credential-stuffing attempts.
- **R2:** Unless an attacker obtains valid credentials for a protected user account.
- **R3:** Unless an authenticated user can access resources beyond their assigned privileges.

These rebuttals are addressed through counterclaims concerning restrictions on repeated authentication attempts, multi-factor authentication, and role- and privilege-based access controls. Planned evidence E1 through E9 provides the basis for evaluating these counterclaims.

---

# Part 2 – OpenEMR Evidence Assessment

## Top-Level Claim

**C1:** OpenEMR sufficiently prevents unauthorized access to protected system resources.

## Evidence Assessment Overview

The purpose of this evidence assessment is to determine how well the evidence identified in the assurance case aligns with evidence currently available or capable of being produced for OpenEMR.

The assurance case focuses on three areas related to unauthorized access:

- Protection against repeated credential-guessing and credential-stuffing attempts
- Protection against the use of compromised passwords through multi-factor authentication (MFA)
- Restriction of authenticated users to resources permitted by their assigned privileges

Nine evidence artifacts (E1–E9) were identified in the assurance case. Each artifact is assessed using the following classifications:

- **Available:** Relevant evidence is currently available from the OpenEMR project.
- **Partially Available:** Relevant functionality or supporting information exists, but additional evidence is needed to fully support the assurance claim.
- **Not Yet Verified:** The required evidence has not been established from the materials examined and would need to be located or generated.

The existence of a security mechanism is not necessarily evidence that the mechanism is correctly configured or effective. For this reason, documentation and source code demonstrating that a feature exists are distinguished from test results demonstrating that the feature provides the intended security protection.

---

## Authentication Protection

### E1 – Authentication Rate-Limiting Configuration

**Assessment:** Partially Available

OpenEMR provides configurable protections against repeated failed authentication attempts. OpenEMR authentication documentation describes mechanisms for tracking failed authentication attempts and applying restrictions based on configured settings.

These mechanisms support the argument that OpenEMR can restrict repeated authentication attempts and reduce exposure to credential-guessing attacks.

However, the existence of these mechanisms does not establish that appropriate restrictions are enabled in a particular OpenEMR deployment. The effectiveness of these protections depends on their configuration.

**Evidence Gap:** Verification that authentication restrictions are enabled and appropriately configured in a representative OpenEMR deployment.

**Additional Evidence Needed:** Configuration records or screenshots demonstrating the enabled authentication restrictions and their settings.

---

### E2 – Failed-Login Protection Test Results

**Assessment:** Not Yet Verified

OpenEMR provides mechanisms intended to restrict repeated unsuccessful authentication attempts. Documentation and source code can demonstrate that these mechanisms exist, but they do not independently demonstrate that the protections function correctly when executed.

Testing should verify that repeated unsuccessful authentication attempts trigger the expected restriction after the configured threshold is reached.

**Evidence Gap:** Executed failed-login protection tests demonstrating that the implemented controls behave as expected.

**Additional Evidence Needed:** Test procedures, execution logs, screenshots, and documented pass/fail results.

---

### E3 – Credential-Stuffing Penetration-Test Report

**Assessment:** Not Yet Verified

Credential stuffing involves attempting authentication using username and password combinations obtained from previous compromises. OpenEMR's authentication protections may help limit these attacks, but the existence of those protections does not demonstrate their effectiveness against a credential-stuffing scenario.

A controlled penetration test would provide stronger evidence by evaluating OpenEMR's authentication protections against repeated attempts using synthetic credentials and test accounts.

**Evidence Gap:** A documented security assessment demonstrating the effectiveness of OpenEMR's protections against credential-stuffing attacks.

**Additional Evidence Needed:** An authorized credential-stuffing penetration test conducted in an isolated OpenEMR test environment.

---

## Multi-Factor Authentication

### E4 – Multi-Factor Authentication Configuration

**Assessment:** Partially Available

OpenEMR supports multi-factor authentication as an additional protection for user accounts. This provides a mechanism for requiring an additional authentication factor beyond possession of a password.

However, the availability of MFA functionality does not establish that it is enabled or required for all accounts within the scope of the assurance case.

**Evidence Gap:** Verification that MFA is enabled and appropriately enforced for protected user accounts.

**Additional Evidence Needed:** MFA configuration records, enrollment information, or screenshots demonstrating applicable MFA settings.

---

### E5 – Multi-Factor Authentication Test Results

**Assessment:** Not Yet Verified

Documentation and implementation evidence can establish that OpenEMR provides MFA functionality, but this does not replace testing that demonstrates the mechanism works correctly in a representative deployment.

Testing should verify that an MFA-protected account cannot complete authentication using only a username and password. Testing should also verify that valid MFA responses permit authentication while invalid responses are rejected.

**Evidence Gap:** Documented MFA test results demonstrating successful enforcement of the secondary authentication requirement.

**Additional Evidence Needed:** MFA functional test procedures, authentication logs, screenshots, and documented pass/fail results.

---

### E6 – Compromised-Credential Authentication Test Results

**Assessment:** Not Yet Verified

A compromised password presents a significant security risk because an attacker may possess a legitimate user's primary authentication credentials.

When MFA is enabled and enforced, possession of a password alone should be insufficient to complete authentication. However, this security property should be demonstrated through testing rather than inferred solely from the existence of MFA functionality.

A controlled test should attempt authentication using a valid password for an MFA-protected test account without supplying the required secondary factor.

**Evidence Gap:** Executed authentication testing confirming that possession of a valid password alone does not provide access to an MFA-protected account.

**Additional Evidence Needed:** Controlled compromised-credential authentication test results, logs, and screenshots showing that the additional authentication factor prevents access.

---

## Authorization and Access Control

### E7 – Role and Privilege Configuration

**Assessment:** Partially Available

OpenEMR provides access-control mechanisms for restricting application functionality based on assigned permissions and privileges. These mechanisms provide the foundation for restricting authenticated users to authorized resources.

However, the existence of access-control functionality does not establish that a particular OpenEMR deployment follows the principle of least privilege. Permission assignments can vary depending on the organization and configuration.

**Evidence Gap:** Verification that roles and privileges are appropriately configured for the operational environment represented by the assurance case.

**Additional Evidence Needed:** Role-permission mappings, access-control configuration records, or screenshots demonstrating the privileges assigned to representative users.

---

### E8 – Access-Control Test Results

**Assessment:** Not Yet Verified

OpenEMR's access-control mechanisms are intended to restrict authenticated users to authorized functionality and resources. However, documentation showing that access controls exist does not independently demonstrate that permissions are consistently enforced.

Testing should evaluate accounts with different assigned privileges and verify that authorized operations succeed while unauthorized operations are denied.

**Evidence Gap:** Documented access-control testing demonstrating consistent enforcement of assigned permissions.

**Additional Evidence Needed:** Role-based functional test cases, test execution records, screenshots, and documented pass/fail results.

---

### E9 – Unauthorized-Resource Access Penetration-Test Report

**Assessment:** Not Yet Verified

Authorization vulnerabilities may allow authenticated users to access resources or perform operations outside their assigned privileges.

Although OpenEMR provides access-control mechanisms, security testing is necessary to determine whether those restrictions can be bypassed.

A penetration test could attempt to access restricted functionality, manipulate resource identifiers, or invoke protected operations using an account with insufficient privileges.

**Evidence Gap:** Documented security-testing results demonstrating resistance to unauthorized-resource access and privilege escalation.

**Additional Evidence Needed:** An authorized penetration-test report evaluating role-based authorization, restricted-resource access, and privilege-escalation scenarios.

---

## Evidence Availability Summary

| Evidence | Description | Assessment |
|---|---|---|
| **E1** | Authentication rate-limiting configuration | Partially Available |
| **E2** | Failed-login protection test results | Not Yet Verified |
| **E3** | Credential-stuffing penetration-test report | Not Yet Verified |
| **E4** | Multi-factor authentication configuration | Partially Available |
| **E5** | Multi-factor authentication test results | Not Yet Verified |
| **E6** | Compromised-credential authentication test results | Not Yet Verified |
| **E7** | Role and privilege configuration | Partially Available |
| **E8** | Access-control test results | Not Yet Verified |
| **E9** | Unauthorized-resource access penetration-test report | Not Yet Verified |

---

## Evidence-Gap Analysis

The assessment identified three evidence artifacts that are partially supported by OpenEMR's existing functionality and project materials: E1, E4, and E7. These artifacts relate to authentication restrictions, multi-factor authentication, and access-control mechanisms.

The remaining six evidence artifacts require additional verification because they concern the demonstrated effectiveness of those security mechanisms. The primary gaps involve test results and penetration-testing evidence specifically addressing the security properties represented in the assurance case.

These gaps do not necessarily indicate that OpenEMR lacks the relevant security protections. Instead, they indicate that the evidence examined is insufficient to fully support the assurance argument.

To strengthen the assurance case, additional evidence should be collected in three areas:

1. **Authentication protection:** Verify that repeated unsuccessful authentication attempts trigger the intended restrictions and evaluate resistance to credential-stuffing attempts.
2. **Multi-factor authentication:** Verify that MFA-protected accounts cannot be accessed using compromised passwords alone.
3. **Authorization enforcement:** Verify that authenticated users cannot access resources or perform operations outside their assigned privileges.

Collecting these results would allow the assurance case to rely on measurable evidence demonstrating the effectiveness of the security mechanisms rather than relying primarily on evidence that the mechanisms exist.

---

## Conclusion

The evidence assessment indicates that OpenEMR provides security mechanisms relevant to preventing unauthorized access, including authentication protections, multi-factor authentication, and access controls.

However, the existence of these mechanisms does not independently establish that they are appropriately configured and effective in every deployment.

Of the nine planned evidence artifacts, three are partially supported by the materials examined, while six require additional verification. The primary evidence gap is the need for testing that directly demonstrates the effectiveness of the security mechanisms represented in the assurance case.

Additional configuration verification, functional testing, and authorized security testing would strengthen the argument that OpenEMR sufficiently prevents unauthorized access to protected system resources.

---

## References

1. **OpenEMR Authentication Documentation**  
   `https://github.com/openemr/openemr/blob/master/Documentation/api/AUTHENTICATION.md`

2. **OpenEMR AuthUtils.php**  
   `https://github.com/openemr/openemr/blob/master/src/Common/Auth/AuthUtils.php`

3. **OpenEMR Installation Help**  
   `https://github.com/openemr/openemr/blob/master/Documentation/help_files/openemr_installation_help.php`

4. **OpenEMR Access Control List Help**  
   `https://github.com/openemr/openemr/blob/master/Documentation/help_files/adminacl_help.php`

5. **OpenEMR Authorization and Scopes**  
   `https://github.com/openemr/openemr/blob/master/Documentation/api/AUTHORIZATION.md`

6. **OpenEMR Developer Guide**  
   `https://github.com/openemr/openemr/blob/master/Documentation/api/DEVELOPER_GUIDE.md`

7. **OpenEMR Main Screen Authentication Implementation**  
   `https://github.com/openemr/openemr/blob/master/interface/main/main_screen.php`
