========== Question ==========  

### What are the characteristics of a secure session manager for preventing identification and authentication failures?  

========== Answer ==========  

Use a server-side, secure, built-in session manager that generates a new random session ID with high entropy after login. The session identifier should not be in the URL, be securely stored, and invalidated after logout, idle, and absolute timeouts.

========== Id ==========  
149

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part VIII - A07 2021-Identification and Authentication Failures::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-VIII-A07-2021-Identification-and-Authentication-Failures::#Chapter-2-How-to-Prevent::#149-What-are-the-characteristics-of-a-secure-s

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
