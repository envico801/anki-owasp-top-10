========== Question ==========  

### Why is SSRF particularly dangerous in microservices architectures?  

========== Answer ==========  

It can allow attackers to move laterally between different services.

**Example**: Using SSRF in one microservice to attack another internal service not exposed externally.

========== Id ==========  
153

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 1 - Overview

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-1-Overview::#153-Why-is-ssrf-particularly-dangerous-in-micr

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
