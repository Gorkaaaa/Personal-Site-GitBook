---
hidden: true
---

# 🎲 Party Poker BAC

## Vulnerability Report

**Title:** Unauthorized Modification of Sensitive Data in Unverified Accounts on partypoker.es

**Author:** Gorka El Bochi Morillo\
**Program:** Entain Public Managed Bug Bounty Engagement 2024

***

### Executive Summary

A vulnerability has been identified on partypoker.es where, once an account is created but remains unverified, it is possible to modify critical data (country, gender, first name, last name, and nationality) that should be immutable. This flaw allows alterations that could disrupt the identity verification process and compromise the integrity of user information. A video demonstrating a step-by-step reproduction of the attack has been attached.

***

### Vulnerability Details

* **Application Context:**\
  Partypoker.es is an online casino platform where users must provide personal information upon account creation. Subsequently, users have a 30-day period to complete identity verification.
* **Expected Restriction:**\
  Once the account is created, sensitive data (country, gender, first name, last name, and nationality) should remain unchangeable until the verification process is complete, preventing alterations that might lead to false or inconsistent verifications.
* **Exploitation Procedure:**
  1. Navigate to: [https://www.partypoker.es/es](https://www.partypoker.es/es)
  2. Log in using an account that has been created but is not yet verified.
  3. Observe in “My Account” that the interface does not allow modifications of these sensitive fields.
  4. Intercept the HTTP requests using tools such as BurpSuite.
  5. Manually modify the parameters corresponding to the sensitive data.
  6. Verify that after manipulation, the sensitive data is updated, thus allowing the alteration of information that should remain unchanged.
* **Evidence:**\
  A video demonstration is attached, showing in detail the step-by-step process to reproduce the attack.

***

### Impact

* **Data Integrity:**\
  The ability to modify critical data in unverified accounts undermines the integrity of the identity verification process, allowing profiles with manipulated information.
* **Fraud and Identity Theft:**\
  An attacker could exploit this vulnerability to alter account data and impersonate other users or create fraudulent accounts, bypassing security controls.
* **Regulatory and Reputational Risk:**\
  Manipulation of sensitive personal information may lead to non-compliance with identity verification regulations and damage user trust, exposing the platform to legal penalties and reputational harm.

***

### Potential Exploitation Scenarios

* **Identity Impersonation:**\
  An attacker could modify their account details to impersonate someone else, affecting the identity verification process and enabling fraudulent activities.
* **Creation of Fraudulent Accounts:**\
  By manipulating sensitive data, attackers can verify accounts with altered information, facilitating illicit activities or evading platform restrictions.
* **Interference with Internal Processes:**\
  Alteration of critical data can distort internal verification processes, reducing the effectiveness of security controls and audit mechanisms.

***

### Mitigation Recommendations

1. **Server-Side Validation:**\
   Implement robust server-side controls to reject any modification attempts of sensitive data, regardless of client-side manipulations.
2. **Strict Access Control:**\
   Restrict access to endpoints that allow data modifications, ensuring that changes to sensitive fields are only permitted following successful identity verification or under controlled circumstances.
3. **Request Integrity:**\
   Introduce mechanisms (e.g., session tokens or digital signatures) to verify the authenticity of modification requests and prevent tampering during transit.
4. **Monitoring and Auditing:**\
   Log detailed records of data change requests to detect abnormal behavior and respond proactively to any manipulation attempts.
5. **Review and Strengthen the Verification Process:**\
   Reassess the identity verification workflow to ensure that once an account is created, critical fields remain unalterable until the verification process has been satisfactorily completed.

***

### Conclusion

This vulnerability enables the modification of sensitive data in unverified accounts, which should remain immutable until the identity verification process is finalized. This flaw opens the door to potential fraud, identity impersonation, and internal process disruption. Implementing the proposed mitigation measures is essential to maintain data integrity, protect user information, and ensure the security of the platform.

_A video demonstration illustrating the step-by-step attack reproduction has been attached to this report._



***

Sincerely,\
**Gorka El Bochi Morillo**\
Bug Bounty Hunter\
Entain Public Managed Bug Bounty Engagement 2024
