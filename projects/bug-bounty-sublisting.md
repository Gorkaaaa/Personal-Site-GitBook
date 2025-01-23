# 🕵️‍♂️ Bug Bounty - Sublisting

<figure><img src="../.gitbook/assets/1693735842478.png" alt=""><figcaption></figcaption></figure>

**Sublisting** is an automated tool for collecting and verifying subdomains. It leverages popular reconnaissance tools such as **subfinder**, **amass**, **sublist3r**, **httpx**, and **socialhunter** to gather subdomains from various sources. The project includes scripts to install necessary dependencies, run subdomain enumeration, and verify their accessibility.

Once subdomains are collected, the tool filters and cleans the results, ensuring only valid and active subdomains are retained. The output is organized and aesthetically formatted for easy review. **Sublisting** simplifies the process of subdomain discovery, making it more efficient and streamlined for security researchers and pentesters.

The repository contains the following scripts:

* **finder.py**: A Python script to check the accessibility of collected subdomains.
* **install.sh**: A setup script to install all required tools.
* **Sublisting.sh**: The main Bash script that automates subdomain collection and verification.

With **Sublisting**, users can quickly gather and validate subdomains, saving time and effort in reconnaissance tasks.

<figure><img src="../.gitbook/assets/imagen (1).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://github.com/Gorkaaaa/Sublisting" %}
