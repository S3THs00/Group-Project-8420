# OpenEMR Security-Related History

OpenEMR has experienced a number of security vulnerabilities throughout its development. Because the software stores and processes sensitive healthcare information, vulnerabilities involving authentication, access control, injection attacks, and exposure of patient information can create significant risks for healthcare organizations.

## Historical Vulnerabilities

In 2018, security researchers identified numerous vulnerabilities in OpenEMR. These included authentication bypass, SQL injection, command injection, cross-site scripting (XSS), cross-site request forgery (CSRF), unauthorized administrative actions, and improper access to files and patient information.

One example is CVE-2018-15152, an authentication bypass vulnerability affecting OpenEMR versions prior to 5.0.1.4. The vulnerability could allow a remote attacker to access multiple patient portal functions without properly authenticating as a patient.

OpenEMR has continued to receive security advisories as additional vulnerabilities have been discovered. More recent examples have involved broken access control, improper authorization, SQL injection, improper TLS certificate validation, and command injection. These vulnerabilities demonstrate the importance of maintaining current OpenEMR installations and applying security updates.

## Security Engineering Improvements

OpenEMR has implemented and documented a variety of security controls over time. These include access control mechanisms, auditing and logging, encryption options, secure API authentication, HTTPS/TLS recommendations, and multi-factor authentication.

The OpenEMR project also maintains a formal process for reporting vulnerabilities. Security vulnerabilities can be privately reported to the OpenEMR Security Team through GitHub or by contacting the project's security email address. Public GitHub Security Advisories document vulnerabilities and the versions in which they were patched.

OpenEMR's security documentation recommends additional deployment protections such as restricting network access, using HTTPS, protecting document directories from direct web access, securing the database, maintaining supported versions of PHP, and enabling multi-factor authentication.

## Authentication and Multi-Factor Authentication

OpenEMR currently supports multi-factor authentication. According to the OpenEMR documentation, both Time-Based One-Time Password (TOTP) and U2F authentication are supported. Users can configure MFA through the MFA Management interface, and administrators can determine which users have enabled MFA.

This existing functionality makes authentication an especially relevant area for our project. Although OpenEMR already provides software-based MFA options, our team can investigate whether authentication can be strengthened or extended through hardware-backed authentication. One potential enhancement is integration with a hardware security device such as a Nitrokey.

A hardware-based approach could provide an additional layer of protection against stolen passwords and account compromise while allowing the team to examine how an existing security mechanism can be extended within a real open-source healthcare application.

## Sources

- OpenEMR Security Advisories: https://github.com/openemr/openemr/security/advisories
- OpenEMR Security Policy: https://github.com/openemr/openemr/security/policy
- OpenEMR Multi-factor Authentication: https://www.open-emr.org/wiki/index.php/Multi-factor_Authentication
- OpenEMR Securing OpenEMR Guide: https://www.open-emr.org/wiki/index.php/Securing_OpenEMR
- NIST NVD CVE-2018-15152: https://nvd.nist.gov/vuln/detail/CVE-2018-15152
