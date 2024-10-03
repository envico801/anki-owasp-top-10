========== Question ==========  

### What should be logged for security-related events?  

========== Answer ==========  

All login attempts, access control, and server-side input validation failures with sufficient context.

**Example**: Logging failed login attempts with username, IP address, and timestamp.

========== Id ==========  
136

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part X - A09 2021-Security Logging and Monitoring Failures::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-X-A09-2021-Security-Logging-and-Monitoring-Failures::#Chapter-2-How-to-Prevent::#136-What-should-be-logged-for-security-related

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
