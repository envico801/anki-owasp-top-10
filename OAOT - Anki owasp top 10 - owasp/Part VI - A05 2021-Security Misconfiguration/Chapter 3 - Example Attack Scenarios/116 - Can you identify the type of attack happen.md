========== Question ==========  

### Can you identify the type of attack happening here?

Directory listing is not disabled on the server. An attacker discovers they can simply list directories. The attacker finds and downloads the compiled Java classes, which they decompile and reverse engineer to view the code. The attacker then finds a severe access control flaw in the application.  

========== Answer ==========  

A05 Security Misconfiguration

========== Id ==========  
116

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part VI - A05 2021-Security Misconfiguration::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-VI-A05-2021-Security-Misconfiguration::#Chapter-3-Example-Attack-Scenarios::#116-Can-you-identify-the-type-of-attack-happen

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
