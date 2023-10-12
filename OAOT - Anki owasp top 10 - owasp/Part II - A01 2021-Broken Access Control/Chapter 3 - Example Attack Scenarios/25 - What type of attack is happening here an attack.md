Q: What type of attack is happening here?
An attacker simply forces browsing to target URLs. Admin rights are required for access to the admin page.
```plaintext
 https://example.com/app/getappInfo
 https://example.com/app/admin_getappInfo
```
- If an unauthenticated user can access either page, it's a flaw.
- If a non-admin can access the admin page, this is a flaw.  
A: A01 Broken Access Control
<!--ID: 1697070660701-->

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part II - A01 2021-Broken Access Control::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP #OWASP-Top-10 #Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```

QUESTION STATUS: Safe to store