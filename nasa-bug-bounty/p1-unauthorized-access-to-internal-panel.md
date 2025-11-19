# 🟥 {P1} Unauthorized Access to Internal Panel

## How I started

This way are staerted when I extracted a subdomains list of the NASA active, this subdomains file reveals too much subdomains ( +2k ).

## Recon

### Surface Recon

For extract this domains I used this website: [https://subdomainfinder.c99.nl](https://subdomainfinder.c99.nl)

This website help you for save much too much time runing tools like subfinder, amass, etc.

My methodology for extract anything value of all subdomains was run [dirsearch](https://github.com/maurosoria/dirsearch.git) tool and see strange behavior testing manually subdomain for subdomain.

In big systems like in this case NASA I test stranger subdomains, I don't focus on principal subdomains.

¿What can I find in this subdomains?

* Config files
* Exposed sensitive information
* Old administrative panels
* Exposed PII Information
* XSS & HTMLI



### Target Recon



