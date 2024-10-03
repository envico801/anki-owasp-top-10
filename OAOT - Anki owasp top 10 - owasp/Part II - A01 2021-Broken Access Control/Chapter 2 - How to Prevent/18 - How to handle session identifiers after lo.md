========== Question ==========  

### How to handle session identifiers after logout?  

========== Answer ==========  

Invalidate on the server; use short-lived JWTs for stateless sessions.

**Example**: Deleting session data from the server when a user logs out.

========== Id ==========  
18

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part II - A01 2021-Broken Access Control::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-II-A01-2021-Broken-Access-Control::#Chapter-2-How-to-Prevent::#18-How-to-handle-session-identifiers-after-lo

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
