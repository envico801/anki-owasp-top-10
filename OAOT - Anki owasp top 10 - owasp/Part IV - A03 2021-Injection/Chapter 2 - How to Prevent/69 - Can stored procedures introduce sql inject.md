========== Question ==========  

### Can stored procedures introduce SQL injection vulnerabilities?  

========== Answer ==========  

Yes, even when parameterized, stored procedures can introduce SQL injection if PL/SQL or T-SQL concatenates queries and data or executes hostile data with EXECUTE IMMEDIATE or exec().

========== Id ==========  
69

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-2-How-to-Prevent::#69-Can-stored-procedures-introduce-sql-inject

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
