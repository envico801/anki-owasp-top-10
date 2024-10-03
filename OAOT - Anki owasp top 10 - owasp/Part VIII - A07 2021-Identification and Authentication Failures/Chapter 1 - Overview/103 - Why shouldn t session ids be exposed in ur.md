========== Question ==========  

### Why shouldn't session IDs be exposed in URLs?  

========== Answer ==========  

It can lead to session hijacking and unauthorized access.

**Example**: Having a URL like "example.com/account?sessionid=1234", which can be easily copied.

========== Id ==========  
103

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part VIII - A07 2021-Identification and Authentication Failures::Chapter 1 - Overview

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-VIII-A07-2021-Identification-and-Authentication-Failures::#Chapter-1-Overview::#103-Why-shouldn-t-session-ids-be-exposed-in-ur

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
