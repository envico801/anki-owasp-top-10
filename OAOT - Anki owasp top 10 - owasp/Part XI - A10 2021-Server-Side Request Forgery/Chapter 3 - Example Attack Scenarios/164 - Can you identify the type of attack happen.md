========== Question ==========  

### Can you identify the type of attack happening here?

Sensitive data exposure – Attackers can access local files or internal services to gain sensitive information such as `file:///etc/passwd` and `http://localhost:28017/`.  

========== Answer ==========  

A10 Server Side Request Forgery (SSRF)

========== Id ==========  
164

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part XI - A10 2021-Server-Side Request Forgery::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-XI-A10-2021-Server-Side-Request-Forgery::#Chapter-3-Example-Attack-Scenarios::#164-Can-you-identify-the-type-of-attack-happen

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
