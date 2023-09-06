# OAOT - Anki owasp top 10 - owasp

## Questions

### Part I - Introduction

#### Chapter 1 - What is OWASP?

Q:: What is OWASP?  
A:: The Open Worldwide Application Security Project (OWASP) is an online community that produces freely-available articles, methodologies, documentation, tools, and technologies in the field of web application security. The OWASP provides free and open resources. It is led by a non-profit called The OWASP Foundation.

Q:: What is OWASP Top 10?  
A:: OWASP Top 10 is a list of the top 10 most critical web application security risks, compiled by the Open Web Application Security Project.

### Part II - A01:2021-Broken Access Control

#### Chapter 1 - Overview

Q:: What is the purpose of access control?  
A:: Access control enforces policy to prevent users from acting outside their intended permissions. Failures can lead to unauthorized information disclosure, modification, or destruction of data, or performing unauthorized business functions.

Q:: Name some common access control vulnerabilities.  
A:: Common access control vulnerabilities include:
- Violation of the principle of least privilege
- Bypassing access control checks
- Insecure direct object references
- Missing access controls for POST, PUT, and DELETE
- Elevation of privilege
- Metadata manipulation
- CORS misconfiguration
- Force browsing to authenticated or privileged pages

Q:: What is meant by "violation of the principle of least privilege" in access control?  
A:: It means that access is granted to capabilities, roles, or users beyond what is necessary. Access should only be given for specific needs, but in this case, it's available to anyone.

Q:: How can access control checks be bypassed?  
A:: Access control checks can be bypassed by modifying the URL (parameter tampering or force browsing), internal application state, or the HTML page. Attack tools can also be used to modify API requests.

Q:: What is "insecure direct object references"?  
A:: Insecure direct object references occur when an attacker can view or edit someone else's account by providing its unique identifier.

Q:: Why is it important to have access controls for POST, PUT, and DELETE requests?  
A:: Without access controls for these requests, attackers can perform actions such as modifying or deleting data without proper authorization.

Q:: What is "elevation of privilege" in the context of access control?  
A:: Elevation of privilege refers to the ability to act as a user without being logged in or to act as an admin when logged in as a regular user. It's a serious security issue.

Q:: How can metadata manipulation be a security risk in access control?  
A:: Metadata manipulation can involve replaying or tampering with tokens like JSON Web Tokens (JWTs), cookies, or hidden fields to elevate privileges or abuse token invalidation mechanisms.

Q:: What is the risk associated with CORS misconfiguration in access control?  
A:: CORS misconfiguration can allow unauthorized/untrusted origins to access an API, potentially leading to security breaches.

Q:: What is "force browsing" in access control?  
A:: Force browsing is the act of accessing authenticated pages as an unauthenticated user or accessing privileged pages as a standard user, which can result in unauthorized access.

#### Chapter 2 - How to Prevent?

### Part III - A02:2021-Cryptographic Failures

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part IV - A03:2021-Injection

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part V - A04:2021-Insecure Design

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part VI - A05:2021-Security Misconfiguration

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part VII - A06:2021-Vulnerable and Outdated Components

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part VIII - A07:2021-Identification and Authentication Failures

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part IX - A08:2021-Software and Data Integrity Failures

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part X - A09:2021-Security Logging and Monitoring Failures

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

### Part XI - A10:2021-Server-Side Request Forgery

#### Chapter 1 - Overview

#### Chapter 2 - How to Prevent?

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp

FILE TAGS: #OWASP #OWASP-Top-10 #Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```