========== Question ==========  

### How to prevent mass record disclosure in SQL injection?  

========== Answer ==========  

Use SQL controls like LIMIT to restrict query results.

**Example**: Adding "LIMIT 1000" to queries to cap the number of returned records.

========== Id ==========  
55

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-2-How-to-Prevent::#55-How-to-prevent-mass-record-disclosure-in-s

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
