# 🪖 Inf Disclosure #3 👩🏻‍🎓 RMIT University

### Executive Summary

A vulnerability has been identified in the RMIT University Vulnerability Disclosure Program that allows public access to sensitive information via an exposed directory listing. The URL [https://hdrprojects.its.rmit.edu.au/](https://hdrprojects.its.rmit.edu.au/) displays a directory containing university student projects. In one of these projects, there is a compressed file named **phdprojects-test.zip** that, when analyzed, reveals an **index.html** file containing a link to a Google Spreadsheet. This spreadsheet exposes sensitive data such as the project title, institutional email, full name, supervisor, discipline, group, campus, program code, and other institutional email addresses.

### Vulnerability Description

* **Type of Vulnerability:** Sensitive Data Exposure and Unrestricted Directory Listing.
* **Location:**
  * **Public Directory:** [https://hdrprojects.its.rmit.edu.au/](https://hdrprojects.its.rmit.edu.au/) (directory listing access).
  * **Compressed File:** `phdprojects-test.zip` which contains the file `index.html`.
  * **Linked Spreadsheet:** [Google Spreadsheet](https://docs.google.com/spreadsheets/d/e/2PACX-1vQkbDFCMBZpDQ2t3ys9poRvWjBhf7xiyhSAnSnm4ygOT_yW6umaeghfRP4yYVuMdPssD-3uF0Kbe5-8/pubhtml?widget=true\&headers=false).
* **Details:** The unrestricted directory listing allows any user to access files and directories that should normally be protected. Within the compressed file, there is an HTML file that references a Google Spreadsheet containing personal and academic sensitive data. This issue appears to be a configuration error specific to this project, as it is not present in the other projects.

### Steps to Reproduce

1. **Access the Public Directory:** Navigate to [https://hdrprojects.its.rmit.edu.au/](https://hdrprojects.its.rmit.edu.au/) and observe that the directory listing is enabled.
2.  **Locate the Compressed File:** Identify and click on the file named `phdprojects-test.zip` among the listed projects.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.58.24.png" alt=""><figcaption></figcaption></figure>
3. **Download and Extract the File:** Download `phdprojects-test.zip` and extract its contents.
4.  **Review the HTML File:** Open the extracted `index.html` file, which contains a link to a Google Spreadsheet.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.58.41.png" alt=""><figcaption></figcaption></figure>
5. **Access the Google Spreadsheet:** Click the provided link to open the publicly accessible Google Spreadsheet.
6.  **Observe Exposed Data:** Review the spreadsheet to find sensitive information such as the project title, institutional email, full name, supervisor, discipline, group, campus, program code, and additional institutional emails.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.58.57.png" alt=""><figcaption></figcaption></figure>

### Potential Impact

* **Exposure of Personal Data:** The exposed data includes personally identifiable and academic information about students and staff (such as institutional emails, project titles, groups, disciplines, etc.). This exposure could violate privacy rights and lead to legal issues under data protection regulations.
* **Phishing and Social Engineering Risks:** An attacker could use the available information to craft personalized phishing emails or perform social engineering attacks, impersonating university staff or faculty members.
* **Reputation and Regulatory Compliance:** The public exposure of sensitive data can harm the university’s reputation and may result in penalties for non-compliance with data protection regulations (such as GDPR or local data protection laws).

### Exploitation Scenario

An attacker could:

1. **Collect Information:** Access the directory listing, download the `phdprojects-test.zip`, and extract the `index.html` which references the Google Spreadsheet.
2. **Analyze and Extract Data:** Retrieve sensitive data (names, emails, project details, etc.) from the spreadsheet.
3. **Conduct Phishing/Social Engineering:** Use the extracted data to send fraudulent emails or make phone calls, posing as university personnel.
4. **Sell or Exploit Data:** The gathered information could be sold on underground markets or used to target specific individuals for further attacks.

### Mitigation Recommendations

1. **Disable Directory Listing:**
   * Configure the web server to prevent directory listings to stop unauthorized users from discovering sensitive files and directories.
2. **Review and Restrict Access:**
   * Conduct an audit of all hosted projects to identify and secure files containing sensitive information.
   * Ensure that compressed files or publicly accessible resources do not include links or references to sensitive resources.
3. **Secure Google Spreadsheet Configuration:**
   * Limit the access of the Google Spreadsheet to only authenticated and authorized users, removing public access.
   * Review and update the sharing settings to ensure only internal or specifically authorized users can view or edit the information.
4. **Implement Security Policies:**
   * Establish clear guidelines on what types of information can be published on publicly accessible resources.
   * Provide security training to development and administrative teams to avoid insecure configurations.

### Conclusion

The identified vulnerability in the RMIT University Vulnerability Disclosure Program exposes sensitive student and staff data through an unrestricted directory listing and misconfigured files. An attacker could exploit this vulnerability for phishing, social engineering, or other malicious activities, compromising both the privacy of individuals and the institution's reputation and compliance. It is essential to implement the recommended mitigations to minimize risk and safeguard sensitive information.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.59.30.png" alt=""><figcaption></figcaption></figure>
