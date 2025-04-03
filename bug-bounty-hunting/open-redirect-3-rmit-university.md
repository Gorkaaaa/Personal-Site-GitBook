# 🎒 Open Redirect #3 👩🏻‍🎓RMIT University

### Summary

An open redirect vulnerability has been identified in the consent endpoint, allowing users to be redirected to arbitrary URLs via the GET parameter `PostConsentDestURL`.

### Bug Details

* **Vulnerability Type:** Open Redirect
* **Affected Endpoint:** `https://outbound.rmit.edu.au/index.cfm`
* **Vulnerable Parameter:** `PostConsentDestURL`
* **Description:**\
  The application does not validate or restrict the content of the `PostConsentDestURL` parameter. This permits any URL to be specified as the redirection target. Given that the redirection occurs on a trusted domain (RMIT), an attacker can exploit this vulnerability to deceive users and direct them to malicious sites.
* **Context:**\
  The vulnerability is found within an environment of the RMIT program, where the role `applicant` is used during the consent process.

### Steps to Reproduce

1.  Access the following example URL:

    ```
    https://outbound.rmit.edu.au/index.cfm?FuseAction=Portal.ConsentUpdate&PostConsentDestURL=https%3A%2F%2Fgoogle.com&chConsentUUID=5F534AC6-962C-93A0-40333590D8F28BF3&consent=1&iConsentId=1&token=61EB89615CE572B20F981BF3DE91E14075B03C5A&vchUserType=applicant
    ```
2.  Modify the value of the `PostConsentDestURL` parameter to a URL controlled by the attacker, for example:

    ```
    https://malicious-site.com
    ```
3.  Send the request and observe that the browser redirects the user to the URL specified in `PostConsentDestURL`.

    ![](https://bugcrowd.com/engagements/rmit-university-vdp-pro/submissions/89400ce4-07a7-4156-b63c-cbdc271e42eb/attachments/7d341549-980e-4020-99e2-c50642916d5e)

    ![](https://bugcrowd.com/engagements/rmit-university-vdp-pro/submissions/89400ce4-07a7-4156-b63c-cbdc271e42eb/attachments/4ddf6e4f-66f4-4db5-9ae6-3fc68eefacc3)

### Impact

* **Phishing and Deception:**\
  An attacker can send seemingly legitimate links that actually redirect to phishing sites, compromising user security.
* **Malware Distribution:**\
  The redirection can be exploited to direct users to sites that distribute malicious software.
* **Credential Theft:**\
  By redirecting users to fraudulent sites that mimic the original portal, sensitive information could be easily captured.

### Potential Abuse

* **Malicious Links in Communications:**\
  The attacker could distribute links that initially appear to come from the RMIT domain but ultimately redirect to attacker-controlled sites for phishing.
* **Bypassing Security Filters:**\
  Leveraging the trust associated with the RMIT domain may allow an attacker to bypass content filtering mechanisms and other security measures implemented on networks or user devices.
* **Targeted Deception:**\
  The vulnerability enables highly targeted attacks, supporting social engineering campaigns to steal credentials or personal information.

### Recommendations and Mitigations

* **Parameter Validation and Sanitization:**\
  Implement strict validation for the `PostConsentDestURL` parameter to ensure that only URLs belonging to a whitelist of authorized domains are accepted.
* **Use of Relative Paths:**\
  Instead of allowing full URLs in the parameter, use internal paths or redirection identifiers that map to secure URLs on the server.
* **Review Redirection Logic:**\
  Ensure that the server does not execute redirections based solely on user-provided data without proper validation.
* **Regular Security Audits:**\
  Conduct periodic security reviews and penetration testing to detect and remediate similar vulnerabilities in the future.

### Conclusion

The open redirect vulnerability in `outbound.rmit.edu.au` represents a significant risk by allowing traffic redirection to malicious sites. It is recommended to implement robust validation controls and restrict redirection URLs to authorized domains to mitigate this risk and protect users against phishing and other related threats.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.54.48.png" alt=""><figcaption></figcaption></figure>
