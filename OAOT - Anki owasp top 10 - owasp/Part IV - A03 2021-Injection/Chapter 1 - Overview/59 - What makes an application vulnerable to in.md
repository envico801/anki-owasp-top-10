========== Question ==========  

### What makes an application vulnerable to injection attacks?  

========== Answer ==========  

An application is vulnerable to injection attacks when:

-   User-supplied data is not properly validated, filtered, or sanitized.

-   Dynamic queries or non-parameterized calls are used without context-aware
    escaping.

-   Hostile data is used in ORM search parameters.

-   Hostile data is directly used or concatenated in SQL queries, commands, or
    stored procedures.

========== Id ==========  
59

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 1 - Overview

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-1-Overview::#59-What-makes-an-application-vulnerable-to-in

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
