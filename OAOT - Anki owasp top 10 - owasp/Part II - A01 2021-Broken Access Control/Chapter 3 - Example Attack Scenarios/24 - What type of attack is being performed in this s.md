Q: What type of attack is being performed in this situation?
The application uses unverified data in a SQL call that is accessing account information:
```java
 pstmt.setString(1, request.getParameter("acct"));
 ResultSet results = pstmt.executeQuery( );
```
An attacker simply modifies the browser's 'acct' parameter to send whatever account number they want. If not correctly verified, the attacker can access any user's account.
```plaintext
 https://example.com/app/accountInfo?acct=notmyacct
```  
A: A01 Broken Access Control
<!--ID: 1697070660916-->

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