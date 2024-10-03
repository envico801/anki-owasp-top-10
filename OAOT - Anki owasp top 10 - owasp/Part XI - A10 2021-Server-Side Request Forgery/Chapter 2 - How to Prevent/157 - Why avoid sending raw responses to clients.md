========== Question ==========  

### Why avoid sending raw responses to clients?  

========== Answer ==========  

To prevent exposure of sensitive information obtained through SSRF.

**Example**: Sanitizing error messages before sending them to the client.

========== Id ==========  
157

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-2-How-to-Prevent::#157-Why-avoid-sending-raw-responses-to-clients

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
