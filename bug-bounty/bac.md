# 🧬 BAC

***

#### 1. Context and Overview

In many online platforms, particularly those handling personal data, certain fields provided during account registration—such as country, gender, first name, last name, and nationality—are expected to remain unaltered until identity verification is complete. This immutability is crucial for maintaining data integrity and ensuring that the identity verification process remains trustworthy. However, in this vulnerability scenario, the intended restrictions are enforced only on the client side. This leaves the sensitive data exposed to manipulation if an attacker intercepts and modifies HTTP requests.

***

#### 2. Detailed Exploitation Process

**Step-by-Step Exploitation**

1. **Account Creation and Unverified Status:**\
   The attacker either registers a new account or uses an existing account that remains unverified. During the registration process, the user provides critical personal details that should not change until verification is completed.
2. **Bypassing Client-Side Controls:**\
   Although the account’s user interface is designed to prevent modifications of sensitive fields, the restrictions are implemented only on the client side. This means that while a normal user is unable to alter the information through the interface, the underlying HTTP requests still contain the sensitive parameters.
3. **Intercepting HTTP Requests:**\
   Using tools like BurpSuite, the attacker captures the HTTP requests sent from the client to the server. This interception allows the attacker to view and modify the parameters being transmitted, including those corresponding to sensitive data.
4. **Modifying Request Parameters:**\
   With the intercepted data in hand, the attacker manually alters the values of the sensitive fields (for example, changing the “first name,” “last name,” or “country” values) to suit their malicious intent.
5. **Resubmitting the Altered Request:**\
   After modifying the parameters, the attacker resends the HTTP request to the server. Due to a lack of robust server-side validation, the server accepts the modified data, updating the account details accordingly.
6. **Verifying the Exploit:**\
   The attacker then reviews the account information to confirm that the sensitive data has been successfully altered, bypassing the intended immutability designed to protect the integrity of the verification process.

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

**Key Observations**

* **Client-Side vs. Server-Side Validation:**\
  The exploit capitalizes on the absence of proper server-side validation. Although the front-end may block modifications through the user interface, the server ultimately accepts manipulated requests when they are submitted directly.
* **Ease of Exploitation:**\
  With widely available tools, an attacker does not require advanced skills to intercept and modify HTTP requests, making the vulnerability relatively easy to exploit.
* **Impact on Verification:**\
  By altering data that should remain static until identity verification, the attacker can potentially falsify user identity, leading to further fraudulent activities and undermining the overall security framework of the platform.

***

#### 3. Mitigation Recommendations

To remediate this vulnerability and enhance overall security, the following measures should be implemented:

1. **Robust Server-Side Validation:**
   * **Implement strict validation:** Ensure that any request attempting to modify sensitive data is checked rigorously on the server side. The server should reject any modifications to these fields until the identity verification process has been successfully completed.
   * **Discard manipulated parameters:** Requests that include altered sensitive fields should be logged and rejected.
2. **Strict Access Control:**
   * **Restrict endpoints:** Limit access to endpoints that process modifications of sensitive data. Only allow changes after successful identity verification or through a controlled administrative process.
   * **Authentication for modifications:** Require additional authentication or session verification before any sensitive data changes can be processed.
3. **Request Integrity Mechanisms:**
   * **Use secure tokens:** Employ session tokens or digital signatures to ensure that the request originated from a legitimate client and has not been tampered with in transit.
   * **Validate token authenticity:** Verify the integrity of these tokens on the server side to ensure that the data has not been altered.
4. **Enhanced Monitoring and Auditing:**
   * **Log all change attempts:** Maintain detailed logs of all requests attempting to modify sensitive data. Analyze these logs for abnormal behavior or repeated tampering attempts.
   * **Set up alerts:** Implement real-time alerts for suspicious activities, such as multiple attempts to modify data fields within unverified accounts.
5. **Strengthen the Verification Process:**
   * **Lock sensitive fields:** Design the account verification workflow such that critical fields remain immutable until the verification is complete.
   * **Periodic review:** Regularly review the verification and account modification processes to identify any potential loopholes or areas for improvement.

***

#### 4. Conclusion

The vulnerability allowing the unauthorized modification of sensitive data in unverified accounts is a serious security risk. By exploiting client-side weaknesses—specifically the lack of robust server-side validation—attackers can alter critical user information, potentially leading to identity fraud, regulatory non-compliance, and reputational damage for the platform. Implementing stringent server-side validation, reinforcing access controls, utilizing request integrity mechanisms, and enhancing monitoring can significantly reduce the risk and help safeguard user data.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
