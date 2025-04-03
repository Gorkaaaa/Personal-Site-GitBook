# 🦹‍♂️ Account Take Over oAuth  🍴The Fork

## Overview of the Vulnerability

A critical security flaw has been found in the authentication process of example.com. The vulnerability allows an attacker to perform an **Account Takeover** by bypassing any identity verification steps. Essentially, the system accepts a new login via Google without verifying whether the account truly belongs to the user, thus granting full access to an account that was originally created with an unverified email.

***

## Detailed Description of the Vulnerability

The root cause of this issue lies in the way the system handles user registration and authentication across different methods. Here’s how it happens:

* **Unverified Email Registration:**\
  The system permits the creation of an account using any email address (for instance, [_email@example.com_](mailto:email@example.com)) without requiring the user to verify the ownership of the email address. This lack of email verification means that accounts are activated immediately, regardless of whether the email is legitimate or even owned by the registrant.
* **Lack of Cross-Verification in Google Sign-In:**\
  When a user subsequently attempts to sign in using Google authentication, the system does not check if the Google account’s email matches a verified account on the platform. As a result, if an attacker creates a Google account with the same email used during the initial registration, they can log in through Google Sign-In and obtain full control of the already existing account without any additional checks.

This oversight in the authentication process leads directly to the possibility of an account takeover, where an attacker can assume control of a user’s account with minimal effort.

***

## Step-by-Step Reproduction of the Attack

The following steps detail how an attacker could exploit this vulnerability:

1. **Account Creation Without Verification:**\
   A user registers on example.com using any email address (e.g., [_email@example.com_](mailto:email@example.com)) without the system requiring an email confirmation. This immediately activates the account.
2. **Logging Out:**\
   After the account creation, the user logs out of the platform. No additional security measure is triggered upon logout.
3. **Exploitation via Google Sign-In:**\
   The attacker, knowing the email used during registration, either creates or already has a Google account with the exact same email address ([_email@example.com_](mailto:email@example.com)). By selecting the Google Sign-In option on example.com, the system, failing to perform further validation, grants the attacker access to the previously created account.
4. **Account Control:**\
   Once logged in, the attacker is able to change critical account details such as the email address, password, and any personal information stored in the account. This effectively locks out the legitimate user and enables the attacker to fully control the account.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Impact and Severity

**Severity:**\
This vulnerability is classified as **critical** because it enables an attacker to take over user accounts without any additional authentication or validation steps.

**Potential Impact:**

* **Identity Theft and Account Hijacking:**\
  Attackers can impersonate users by taking control of their accounts, which could lead to identity theft and unauthorized access to personal data.
* **Data Modification:**\
  Once an account is compromised, the attacker can modify sensitive information, such as the registered email or password, thereby preventing the legitimate owner from regaining control of the account.
* **Fraud and Misuse:**\
  Depending on the functionalities available in the user account (e.g., booking services, payment methods), an attacker could perform fraudulent transactions or misuse the account for scams and other malicious activities.

***

## Potential Actions an Attacker Could Take

If exploited, the vulnerability opens several avenues for malicious activities, including:

* **Unauthorized Account Creation:**\
  An attacker could create multiple accounts with unverified email addresses, potentially targeting users unknowingly and setting up conditions for future compromises.
* **Stealing Personal Information:**\
  With access to sensitive user data, attackers could extract and misuse personal information such as names, phone numbers, and addresses.
* **Preventing Legitimate Access:**\
  By changing account credentials (like the email and password), the attacker effectively locks out the legitimate user, making recovery difficult.
* **Conducting Fraud:**\
  The compromised account could be used to execute fraudulent transactions or other forms of scams within the platform, undermining user trust and the integrity of the service.

***

## Recommendations to Mitigate the Risk

To remediate this vulnerability and prevent similar exploits in the future, the following security measures are recommended:

1. **Mandatory Email Verification:**\
   Implement a system where a verification link is sent to the user’s email upon registration. Only after confirming the email should the account be activated.
2. **Authentication Method Consistency:**\
   Ensure that there is a unified authentication process across different methods. For instance, if a user registers with an email and password, additional verification should be required when using Google Sign-In to confirm that the Google account belongs to the same user.
3. **Duplicate Account Validation:**\
   The system should check if a user attempting to log in via Google already has an existing account. In such cases, additional authentication or verification steps must be enforced to confirm ownership.
4. **Credential Change Notifications:**\
   When changes are made to critical account details (e.g., email or password), an immediate notification should be sent to the previously registered email. This helps detect unauthorized modifications promptly.

***

## Conclusion

The discovered vulnerability in the authentication system of **example.com** represents a serious security risk, as it allows unauthorized account takeovers without any identity confirmation. The ability for an attacker to exploit this flaw, gain access, and modify sensitive information underscores the need for immediate action. By implementing robust email verification, unifying authentication processes, validating duplicate accounts, and issuing real-time notifications for credential changes, the risk of such attacks can be significantly mitigated.

Immediate remediation is critical not only to protect user data but also to maintain the integrity and trustworthiness of the platform. Addressing these issues will help prevent potential security breaches and safeguard the interests of all users.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***
