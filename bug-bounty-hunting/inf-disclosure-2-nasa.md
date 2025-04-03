# 🪖 Inf Disclosure #2 🚀NASA

### Description

A classified information exposure vulnerability has been identified on the nasa.gov domain. Using Google Dorking techniques, it was possible to access a PDF document containing blueprints and photographs related to a NASA project or mission.

This file is publicly accessible without any access restrictions and is marked with “Classified” and “Confidential” stamps, indicating that the information contained in it has not been officially declassified.

The document is accessible at the following URL:

```

https://ntrs.nasa.gov/api/citations/19930093800/downloads/19930093800.pdf
```

This discovery is independent of previous reports, as it pertains to a completely different document containing distinct information, compromising a different area of sensitive data.

***

### Steps to Reproduce

1.  Open a web browser and navigate to [Google](https://www.google.com/).

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.49.03.png" alt=""><figcaption></figcaption></figure>
2. Enter the following Google Dorking query in the search bar:

```
site:nasa.gov ext:pdf inurl:"19930093800.pdf"
```

3.  Review the search results and access the document link.

    <figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.50.12.png" alt=""><figcaption></figcaption></figure>
4. Download or view the file to confirm the “Classified” and “Confidential” markings.
5. Verify that no official declassification notice is present.

***

### Potential Impact

An attacker with access to this document could:

* Obtain detailed blueprints and photographs of a NASA project/mission.
* Expose confidential data that could compromise national security.
* Facilitate access to critical information for espionage or intelligence purposes.
* Utilize the content for sabotage or reverse engineering.

***

### Mitigation Recommendations

1. Remove the publicly accessible file or restrict access via authentication.
2. Configure the robots.txt file to prevent search engines from indexing sensitive documents.
3. Conduct periodic audits of publicly accessible content on NASA domains.
4. Encrypt classified documents and implement strict access control measures.
5. Monitor for unusual access patterns and Google Dorking attempts against NASA’s servers.

***

### Conclusion

The exposure of this document poses a significant risk to the confidentiality of strategic NASA information. Immediate measures are recommended to prevent unauthorized exploitation.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-03 at 05.51.05.png" alt=""><figcaption></figcaption></figure>

***
