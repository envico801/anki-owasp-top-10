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

Q:: What is the first step in preventing cryptographic failures?  
A:: The first step is to classify data processed, stored, or transmitted by an application and identify which data is sensitive according to privacy laws, regulatory requirements, or business needs.

Q:: Why should sensitive data be discarded or tokenized if not needed?  
A:: Storing sensitive data unnecessarily increases the risk of data breaches. It should be discarded as soon as possible or tokenized to protect it.

Q:: What is the importance of encrypting sensitive data at rest?  
A:: Encrypting sensitive data at rest ensures that even if the data is physically stolen, it remains protected.

Q:: What should be ensured regarding cryptographic algorithms, protocols, and keys?  
A:: Up-to-date and strong standard algorithms, protocols, and keys should be used, and proper key management should be in place.

Q:: How should data in transit be protected?  
A:: All data in transit should be encrypted with secure protocols like TLS, using forward secrecy (FS) ciphers and cipher prioritization. Enforcement can be done using directives like HTTP Strict Transport Security (HSTS).

Q:: Why should caching be disabled for responses containing sensitive data?  
A:: Disabling caching prevents sensitive data from being stored in caches, reducing the risk of exposure.

Q:: What is the significance of applying required security controls based on data classification?  
A:: Applying required security controls based on data classification ensures that the appropriate level of protection is applied to data, aligning with its sensitivity and importance.
Front of Flashcard 5:

Q:: Why is it discouraged to use legacy protocols like FTP and SMTP for transporting sensitive data?  
A:: Using legacy protocols like FTP and SMTP for transporting sensitive data is discouraged because they lack the security features and encryption needed to protect sensitive information from interception and unauthorized access.

Q:: What is the importance of using strong adaptive and salted hashing functions for storing passwords?  
A:: Strong adaptive and salted hashing functions make it difficult for attackers to recover plaintext passwords from stored hashes.

Q:: How should initialization vectors (IV) be chosen and used?  
A:: Initialization vectors should be chosen appropriately for the mode of operation and never used twice for a fixed key.

Q:: What should be used instead of just encryption?  
A:: Authenticated encryption should be used to ensure both data confidentiality and integrity.

Q:: How should cryptographic keys be generated and stored?  
A:: Keys should be generated cryptographically randomly and stored in memory as byte arrays. Passwords should be converted to keys using appropriate key derivation functions.

Q:: What should be ensured about cryptographic randomness?  
A:: Cryptographic randomness should not be seeded in a predictable way or with low entropy.

Q:: Why should deprecated cryptographic functions and padding schemes be avoided?  
A:: Deprecated cryptographic functions and padding schemes like MD5, SHA1, and PKCS #1 v1.5 are known to have vulnerabilities and should be avoided.

Q:: What is the significance of verifying independently the effectiveness of configuration and settings?  
A:: Verifying independently the effectiveness of configuration and settings is crucial to ensure that cryptographic implementations and security measures are functioning correctly and providing the intended level of protection.

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