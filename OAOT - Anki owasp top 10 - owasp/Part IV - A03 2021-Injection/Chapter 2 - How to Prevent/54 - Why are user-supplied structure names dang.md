========== Question ==========  

### Why are user-supplied structure names dangerous in SQL?  

========== Answer ==========  

They can't be safely escaped, allowing potential schema manipulation.

**Example**: Allowing users to specify table names in a custom report builder.

========== Id ==========  
54

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-2-How-to-Prevent::#54-Why-are-user-supplied-structure-names-dang

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
