Q: What kind of attack is described in this situation?
A React application calls a set of Spring Boot microservices. Being functional programmers, they tried to ensure that their code is immutable. The solution they came up with is serializing the user state and passing it back and forth with each request. An attacker notices the "rO0" Java object signature (in base64) and uses the Java Serial Killer tool to gain remote code execution on the application server.  
A: A08 Software and Data Integrity Failures
<!--ID: 1697070648219-->

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IX - A08 2021-Software and Data Integrity Failures::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP #OWASP-Top-10 #Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```

QUESTION STATUS: Safe to store