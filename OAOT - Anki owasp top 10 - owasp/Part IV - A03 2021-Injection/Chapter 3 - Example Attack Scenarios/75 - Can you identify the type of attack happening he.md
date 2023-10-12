Q: Can you identify the type of attack happening here?
Similarly, an application’s blind trust in frameworks may result in queries that are still vulnerable, (e.g., Hibernate Query Language (HQL)):
```java
Query HQLQuery = session.createQuery("FROM accounts WHERE custID='" + request.getParameter("id") + "'");
```
In both cases, the attacker modifies the ‘id’ parameter value in their browser to send: ' UNION SLEEP(10);--. For example:
```plaintext
http://example.com/app/accountView?id=' UNION SELECT SLEEP(10);--
```
This changes the meaning of both queries to return all the records from the accounts table. More dangerous attacks could modify or delete data or even invoke stored procedures.  
A: A03 Injection
<!--ID: 1697070655760-->

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