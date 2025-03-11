# 🎒 Open Redirect

### Vulnerability Description

The vulnerability arises because the **post\_logout\_redirect\_uri** parameter is not restricted to a specific set of allowed URLs. This means that any value (e.g., [_evil.com_](http://evil.com/)) can be injected, allowing an attacker to redirect users to a malicious site after logout. Such an open redirect can be exploited for phishing, credential theft, or other malicious activities.

***

### Steps to Reproduce the Vulnerability&#x20;

1. **Access the Base URL:**
   *   Start the logout process by navigating to:

       ```
       <https://[TARGET_DOMAIN]/auth/realms/restaurant/protocol/openid-connect/logout>
       ```
   *

       <figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
2. **Modify the Parameter:**
   *   Append or modify the **post\_logout\_redirect\_uri** parameter to point to a URL under the attacker's control, for example:

       ```
       ?post_logout_redirect_uri=https://evil.com
       ```
   *   The complete URL becomes:

       ```
       <https://[TARGET_DOMAIN]/auth/realms/restaurant/protocol/openid-connect/logout?post_logout_redirect_uri=https://evil.com>
       ```
   *

       <figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
3. **Execution and Observation:**
   * Share the modified link with a victim.
   * When the victim logs out, they will be redirected to [_https://evil.com_](https://evil.com/).
   *

       <figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

       <figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

***

### Impact and Possible Exploitations

*   **Phishing:**

    An attacker can distribute the manipulated URL via email or messaging, tricking the victim into believing they are logging out of the legitimate service. Once redirected to the malicious site, the attacker could prompt the user to enter sensitive information.
*   **Credential or Personal Data Theft:**

    The attacker may create a fake login interface mimicking the original service, capturing user credentials and personal information.
*   **Malware Distribution:**

    The redirection could lead to a site that attempts to download malware or execute harmful scripts on the victim's device.
*   **Brand Reputation Damage:**

    Exploiting this vulnerability can erode user trust and harm the company’s reputation by associating the service with insecure practices.

***

### Mitigation Measures

1. **Whitelist Validation:**
   * Restrict allowed values for **post\_logout\_redirect\_uri** to a predefined list of trusted URLs belonging to the application.
2. **Reject External URLs:**
   * Configure the system to accept only internal redirects or URLs that belong to the primary domain of the service.
3. **Redirection Confirmation:**
   * Implement an intermediate page that notifies the user of the destination URL and requests confirmation before proceeding with the redirection.
4. **Update and Configure Authentication Framework:**
   * If using an authentication system like Keycloak (as the URL structure suggests), review its redirection settings and apply any available patches or updates that address this vulnerability.
5. **Logging and Monitoring:**
   * Set up detailed logging of logout actions and redirection parameters to quickly detect and respond to potential exploitation attempts.

***

### Conclusion

Although open redirect vulnerabilities might seem trivial, they can be leveraged in conjunction with phishing and data theft tactics to execute significant attacks. By enforcing strict validation and restricting redirect parameters to a trusted whitelist, the risk can be mitigated, protecting both users and the integrity of the service.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

***
