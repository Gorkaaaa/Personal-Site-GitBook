# 🚧 Miss Configuration 👩🏻‍🎓RMIT University

### Summary

A vulnerability was identified in the email update process on the [RMIT Inbound](https://inbound.rmit.edu.au/) site. The application allows a user (attacker) to change their account’s email address to one that is already in use by another user (victim) without any validation to check for uniqueness or ownership. Although this issue does not result in a full account takeover, it can lead to communication confusion, potential privacy concerns, and opportunities for social engineering attacks.

***

### Vulnerability Details

*   Context:

    During bug bounty testing, it was discovered that the application fails to verify if the new email address is already registered when a user attempts to change their email.
*   Behavior:

    An attacker can change the email associated with their account to match that of an already registered victim account without any validation or confirmation.
*   Limitation:

    The attacker does not gain access to the victim’s account; however, the duplicate email could interfere with notification delivery and account recovery processes.

***

### Steps to Reproduce

1.  Create a Hacker Account:

    * Email: `8susn8dghk@qacmjeq.com`
    * Password: `examplePassword`

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.12.05.png" alt=""><figcaption></figcaption></figure>
2.  Create a Victim Account:

    * Email: `jhc7fhw7g4@qejjyl.com`
    * Password: `examplePassword`&#x20;

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.13.03.png" alt=""><figcaption></figcaption></figure>
3. Login as the Attacker (Hacker Account).
4.  Change the Email Address:

    * Change the email associated with the Hacker account to that of the Victim account: `jhc7fhw7g4@qejjyl.com`
    * No validation was performed to prevent this change.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.13.23.png" alt=""><figcaption></figcaption></figure>
5.  Verification:

    * Both the Victim account and Hacker account now share the same email.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.14.13.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.13.44.png" alt=""><figcaption></figcaption></figure>

***

### Potential Impact

* Communication Confusion:
  * Notifications, alerts, and password recovery emails intended for the victim may be sent to the attacker’s account, leading to miscommunication.
* Interference with Account Security:
  * Sharing the same email between two accounts might result in the victim losing control over critical communications, such as password resets or account alerts.
* Social Engineering Opportunities:
  * An attacker could exploit the email confusion to perform phishing attacks or other manipulative tactics.
* Reputational Risk:
  * The integrity of the authentication system could be compromised, potentially affecting user trust in the platform.

***

### Mitigation Recommendations

1. Email Uniqueness Validation:
   * Implement a validation check to ensure that the new email address is not already associated with another account.
2. Ownership Verification:
   * When a user requests an email change, send a confirmation link to the new email address to verify ownership before updating the account.
3. Additional Restrictions:
   * Implement extra security steps or restrictions when modifying sensitive account information, such as email addresses.
4. Audit Logging:
   * Record and monitor email change events to detect any unusual activity or repeated attempts at duplicating email addresses.

***

### Conclusion

The absence of proper validation during the email update process poses a risk to the integrity of user account management. Although it does not directly lead to account takeover, it can result in communication errors and create opportunities for social engineering attacks. Implementing robust validation and verification controls in the email update process is essential to maintaining system integrity and user trust.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.15.19.png" alt=""><figcaption></figcaption></figure>
