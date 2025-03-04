---
hidden: true
---

# 🍴 The Fork ATO

#### **Summary**

A critical vulnerability has been identified in TheFork's authentication system, allowing **Account Takeover** without any prior validation. This flaw enables any malicious user to gain full access to another user's account simply by signing in with Google, without requiring any identity confirmation.

***

#### **Vulnerability Description**

TheFork's authentication system has a deficiency in email validation, creating a scenario where an attacker can gain full access to third-party accounts without authorization.

**Steps to Reproduce the Issue:**

1. A user can create an account or already have an account on TheFork with an arbitrary email address (e.g., `gorkabochi@gmail.com`) without the system requiring email verification.
2. After creating the account, the user can log out without restrictions.
3. If an attacker now creates a Google account with the same victim's email and simply logs in using **Google Sign-In**, the system grants full access to the existing account without any additional validation.
4. The attacker, now logged in through Google, can modify account details such as the email address, password, and access any personal information associated with the account.

_A video demonstrating step-by-step how to reproduce this attack has been attached._

***

#### **Severity of the Vulnerability**

This vulnerability is **critical** as it allows account takeover without any intervention from the legitimate user and without requiring additional credentials from the attacker.

**Potential Impact:**

* **Identity theft & account hijacking:** An attacker can take control of other users' accounts simply by using Google authentication with an already registered email.
* **Personal data modification:** The attacker can change the account information, including the email and password, locking the legitimate user out.
* **Fraud risk:** Depending on the account functionalities (e.g., reservations, stored payment methods), the attacker could take harmful actions on behalf of the user.

***

#### **What Could an Attacker Do?**

If an attacker exploits this vulnerability, they could:

* Create accounts using third-party email addresses without their consent and later gain full access to these accounts.
* Take control of **existing user accounts** if the victims have not previously verified their email.
* Steal **personal information**, such as names, phone numbers, and addresses associated with the account.
* Modify **account credentials**, preventing the legitimate user from recovering their account.
* Use the **compromised account** to conduct fraud or scams within the platform.

***

#### **Recommendations to Mitigate the Risk**

To fix this vulnerability and prevent future exploits, the following security measures are recommended:

1. **Mandatory Email Verification:**

Before granting access to an account, the system should require the user to verify their email via a confirmation link.

1. **Authentication Unification:**

Prevent coexistence of two authentication methods that do not consistently validate identity (**email & Google Sign-In**).\
If a user registers with an email and password, they should undergo additional verification when attempting to log in with Google.

1. **Duplicate Account Validation:**

The system should check if a user attempting to log in with Google **already has an existing account**, and if so, require additional authentication to confirm ownership.

1. **Credential Change Notifications:**

If a user changes their email or password, an immediate notification should be sent to their previous email to detect unauthorized access.

!\[\[ATO TheFork.mp4]]

***

#### **Conclusion**

The vulnerability discovered in TheFork enables unauthorized account takeovers and poses a **serious security risk** to users. Immediate action is strongly recommended to fix this issue and prevent potential security incidents.
