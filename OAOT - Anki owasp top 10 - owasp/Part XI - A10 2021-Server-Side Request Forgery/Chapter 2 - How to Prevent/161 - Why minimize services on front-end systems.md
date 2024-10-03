========== Question ==========  

### Why minimize services on front-end systems?  

========== Answer ==========  

To reduce the attack surface exposed to potential SSRF attempts.

**Example**: Keeping only the web server on the front-end, moving application logic to separate servers.

========== Id ==========  
161

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-2-How-to-Prevent::#161-Why-minimize-services-on-front-end-systems

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
