# ⚔️ BAC 👩🏻‍🎓RMIT University

### Summary

A vulnerability has been discovered on [outbound.rmit.edu.au](http://outbound.rmit.edu.au/) that allows unauthorized account creation. Although the system is not supposed to permit account creation, injecting a single quote (') in the URL bypasses this restriction and grants access to a hidden registration panel. A demonstration video is attached to this report.

### Context and Vulnerability Description

Normally, the main domain (e.g., `https://outbound.rmit.edu.au/index.cfm?FuseAction=Abroad.Home`) and the "NON-RMIT-LOGIN" section do not provide any option for account creation. However, by injecting a quote into the URL, the system’s logic is altered, and the user is redirected to a panel that prompts a series of questions. By answering these questions appropriately—indicating that the user does not have login credentials and is not registered at an institution—the registration process is unlocked. The system then allows the user to create an account and sends temporary credentials via email.

### Steps to Reproduce

1.  **Access the Main Domain:** Navigate to `https://outbound.rmit.edu.au/index.cfm?FuseAction=Abroad.Home` and verify that there is no option for creating an account.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.16.29.png" alt=""><figcaption></figcaption></figure>
2.  **Visit the "NON-RMIT-LOGIN" Section:** Go to the NON-RMIT-LOGIN section and confirm that account creation is not mentioned.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.17.01.png" alt=""><figcaption></figcaption></figure>
3.  **Inject a Quote in the URL:**

    Modify the URL by appending a single quote (') to create:

    ```
    <https://outbound.rmit.edu.au/index.cfm?FuseAction=Security.ExistingUserLogin>'
    ```
4.  **Access the Registration Panel:** The injected quote redirects you to a panel where you must answer several questions.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.17.54.png" alt=""><figcaption></figcaption></figure>
5. **Answer the Questions:**
   *   For the first question, answer: _I do not have login credentials to this site._

       <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.18.17.png" alt=""><figcaption></figcaption></figure>
   *   For the second question, answer: _I am not currently registered at an institution._

       <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.18.30.png" alt=""><figcaption></figcaption></figure>
6.  **Create the Account:** After answering the questions, proceed with the account creation process. Once your details are submitted, you will receive an email containing temporary credentials, including a temporary password.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.18.42.png" alt=""><figcaption></figcaption></figure>

### Impact

* **Unauthorized Account Creation:** An attacker can bypass the intended restrictions to create new accounts without authorization.
* **Access Control Bypass:** The vulnerability undermines the system’s authentication logic, enabling attackers to gain unintended access to registration functions.
* **Potential for Mass Account Registration:** Attackers could automate the process to create multiple accounts, potentially leading to abuse of system resources.
* **Phishing and Social Engineering:** Unauthorized accounts could be used to send fraudulent communications or mimic official notifications, deceiving legitimate users.
* **Reputation and Trust Issues:** Allowing unauthorized account creation can erode user trust and damage the institution's reputation.

### Potential Abuse Scenarios

* **Automated Account Creation:** Attackers could mass-register accounts to flood the system, launch spam campaigns, or conduct further attacks.
* **Impersonation and Phishing:** Fraudulent accounts may be used to impersonate legitimate users or the institution, facilitating phishing schemes.
* **Reconnaissance:** By understanding the account creation process, an attacker might further explore the system for additional vulnerabilities or weaknesses.

### Recommendations and Mitigations

* **Input Validation and Sanitization:** Implement robust input validation and sanitize all parameters, especially those derived from the URL, to prevent manipulation via injection.
* **Restrict Access to Registration Functions:** Ensure that account creation endpoints are only accessible through intended, controlled workflows and require proper authorization.
* **Implement Server-Side Checks:** Validate that incoming requests originate from legitimate channels and adhere to the expected logic before rendering any registration functionality.
* **Regular Security Audits:** Conduct periodic penetration testing and code reviews to detect and remediate similar vulnerabilities before they can be exploited.

### Conclusion

This vulnerability allows for unauthorized account creation on [outbound.rmit.edu.au](http://outbound.rmit.edu.au/) via a simple quote injection in the URL. This bypass of normal account creation restrictions can be exploited to register fraudulent accounts, conduct phishing attacks, or carry out mass account registrations. It is crucial to address this issue by enforcing strict input sanitization, access control, and regular security reviews to maintain the integrity of the system.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.19.07.png" alt=""><figcaption></figcaption></figure>
