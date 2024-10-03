========== Question ==========  

### Why is session ID reuse after login risky?  

========== Answer ==========  

It can allow unauthorized users to take over authenticated sessions.

**Example**: Not generating a new session ID after a user logs in, potentially allowing old IDs to remain valid.

========== Id ==========  
104

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part VIII - A07 2021-Identification and Authentication Failures::Chapter 1 - Overview

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-VIII-A07-2021-Identification-and-Authentication-Failures::#Chapter-1-Overview::#104-Why-is-session-id-reuse-after-login-risky

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
