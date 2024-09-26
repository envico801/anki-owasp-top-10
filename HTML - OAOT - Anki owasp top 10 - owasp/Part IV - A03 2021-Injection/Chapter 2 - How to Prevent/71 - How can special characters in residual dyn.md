========== Question ==========  

### How can special characters in residual dynamic queries be handled to prevent injection?  

========== Answer ==========  

Special characters in residual dynamic queries should be escaped using the specific escape syntax for that interpreter.

> **Note:** SQL structures such as table names, column names, and so on cannot be escaped, and thus user-supplied structure names are dangerous. This is a common issue in report-writing software.

========== Id ==========  
71

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 2 - How to Prevent

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-2-How-to-Prevent::#71-How-can-special-characters-in-residual-dyn

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
