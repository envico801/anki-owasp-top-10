========== Question ==========  

### Why disable HTTP redirections for SSRF prevention?  

========== Answer ==========  

To prevent the application from being tricked into accessing malicious sites.

**Example**: Disabling automatic following of 3xx redirect responses in HTTP clients.

========== Id ==========  
158

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-2-How-to-Prevent::#158-Why-disable-http-redirections-for-ssrf-pre

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
