Q: What type of attack is being carried out in this situation?
An application uses untrusted data in the construction of the following vulnerable SQL call:
```java
String query = "SELECT * FROM accounts WHERE custID='" + request.getParameter("id") + "'";
```  
A: A03 Injection
<!--ID: 1697070655835-->

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP #OWASP-Top-10 #Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```

QUESTION STATUS: Safe to store