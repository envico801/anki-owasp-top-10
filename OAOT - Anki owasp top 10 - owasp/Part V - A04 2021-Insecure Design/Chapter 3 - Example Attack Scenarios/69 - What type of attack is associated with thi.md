========== Question ==========  

### What type of attack is associated with this situation?

A credential recovery workflow might include “questions and answers,” which is prohibited by NIST 800-63b, the OWASP ASVS, and the OWASP Top 10. Questions and answers cannot be trusted as evidence of identity as more than one person can know the answers, which is why they are prohibited. Such code should be removed and replaced with a more secure design.  

========== Answer ==========  

A04 Insecure Design

========== Id ==========  
69

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part V - A04 2021-Insecure Design::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-V-A04-2021-Insecure-Design::#Chapter-3-Example-Attack-Scenarios::#69-What-type-of-attack-is-associated-with-thi

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
