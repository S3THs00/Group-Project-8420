# OpenEMR Security Assurance Case Analysis

## Part 1 – Assurance Case

### Unauthorized Access Assurance Case

**Top-Level Claim C1:** OpenEMR sufficiently prevents unauthorized access to protected system resources.

This assurance case provides an argument and identifies planned evidence supporting the claim that OpenEMR sufficiently prevents unauthorized access to protected system resources. The argument addresses three primary concerns: repeated credential-guessing and credential-stuffing attempts, compromised user passwords, and authenticated users accessing resources beyond their assigned privileges.

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

## Part 2 – OpenEMR Evidence Assessment

### Gap Analysis & Bridging Efforts

#### Gap 1: Authentication Protection Evidence (E1–E3)

**Gap:** OpenEMR provides mechanisms for tracking and restricting repeated failed authentication attempts, and project documentation and source code provide evidence that these protections are implemented. However, the project materials examined do not fully provide the deployment-specific configuration records, executed failed-login test results, or credential-stuffing penetration-test results identified as Evidence E1–E3 in the assurance case.

**Bridging Effort:** A representative OpenEMR deployment should be configured with appropriate failed-login restrictions and tested using controlled authentication attempts. Configuration records should document the enabled thresholds, while functional testing should verify that repeated unsuccessful login attempts trigger the expected restrictions. An authorized credential-stuffing test using synthetic accounts and credentials could provide additional evidence that the controls resist repeated credential-based attacks.

#### Gap 2: Multi-Factor Authentication Evidence (E4–E6)

**Gap:** OpenEMR provides multi-factor authentication functionality, which supports the assurance argument that a compromised password alone can be insufficient to access a protected account. However, the existence of MFA functionality does not demonstrate that MFA is enabled for applicable accounts or provide the configuration and executed test results represented by Evidence E4–E6.

**Bridging Effort:** MFA should be enabled for representative protected accounts in an OpenEMR test environment. Configuration records should document MFA enrollment and enforcement. Testing should then attempt authentication with a valid password but without the required secondary factor and verify that access is denied. Additional testing should verify that valid MFA responses are accepted and invalid responses are rejected.

#### Gap 3: Authorization and Access-Control Evidence (E7–E9)

**Gap:** OpenEMR provides role- and privilege-based access-control mechanisms for restricting authenticated users. These mechanisms provide implementation evidence supporting the assurance case, but they do not independently establish that roles follow least privilege or that users cannot bypass authorization restrictions. The project materials examined do not fully provide the deployment-specific role configuration, access-control test results, or penetration-test results represented by Evidence E7–E9.

**Bridging Effort:** Representative user roles should be configured with documented privileges and tested against protected OpenEMR resources. Testing should verify that authorized operations succeed while operations outside the user's assigned privileges are denied. Authorized security testing should also attempt restricted-resource access and privilege escalation to determine whether access-control restrictions can be bypassed.

---

### Conclusion

The evidence assessment indicates that OpenEMR provides security mechanisms relevant to preventing unauthorized access, including authentication protections, multi-factor authentication, and role- and privilege-based access controls.

However, the existence of these mechanisms does not independently establish that they are appropriately configured and effective in every deployment.

The evidence assessment identified three primary gaps involving authentication protection, multi-factor authentication, and authorization enforcement. Although OpenEMR provides documented security mechanisms supporting these areas, additional configuration verification, functional testing, and authorized security testing are necessary to establish that the controls operate effectively in a representative deployment.

Addressing these gaps would provide stronger measurable evidence supporting the top-level claim that OpenEMR sufficiently prevents unauthorized access to protected system resources.

---

## References

1. **OpenEMR Authentication Documentation**  
   https://github.com/openemr/openemr/blob/master/Documentation/api/AUTHENTICATION.md

2. **OpenEMR AuthUtils.php**  
   https://github.com/openemr/openemr/blob/master/src/Common/Auth/AuthUtils.php

3. **OpenEMR Access Control List Help**  
   https://github.com/openemr/openemr/blob/master/Documentation/help_files/adminacl_help.php

4. **OpenEMR Authorization and Scopes**  
   https://github.com/openemr/openemr/blob/master/Documentation/api/AUTHORIZATION.md
