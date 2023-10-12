Q: How should session identifiers be handled after logout?  
A: Stateful session identifiers should be invalidated on the server after logout. Stateless JWT tokens should be short-lived, and for longer-lived JWTs, it's recommended to follow OAuth standards for revoking access.
<!--ID: 1697070661828-->

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part II - A01 2021-Broken Access Control::Chapter 2 - How to Prevent

FILE TAGS: #OWASP #OWASP-Top-10 #Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```

QUESTION STATUS: Safe to store