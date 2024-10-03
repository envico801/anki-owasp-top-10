========== Question ==========  

### How can SSRF impact containerized environments?  

========== Answer ==========  

It may allow access to the host system or other containers.

**Example**: An SSRF vulnerability in a container allowing access to the Docker socket on the host.

========== Id ==========  
152

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 1 - Overview

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-1-Overview::#152-How-can-ssrf-impact-containerized-environm

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
