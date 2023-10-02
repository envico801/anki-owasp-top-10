# OAOT - Anki owasp top 10 - owasp

## Questions

### Part I - Introduction

#### Chapter 1 - What is OWASP?

Q:: What is OWASP?  
A:: The Open Worldwide Application Security Project (OWASP) is an online community that produces freely-available articles, methodologies, documentation, tools, and technologies in the field of web application security. The OWASP provides free and open resources. It is led by a non-profit called The OWASP Foundation.

Q:: What is OWASP Top 10?  
A:: OWASP Top 10 is a list of the top 10 most critical web application security risks, compiled by the Open Web Application Security Project.

### Part II - A01:2021-Broken Access Control

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Broken_Access_Control.png)

#### Chapter 1 - Overview

Q:: What is the "Broken Access Control" category about?  
A:: **A01:2021 - Broken Access Control**: This category is now the most serious web application security risk. It focuses on issues related to access control, where users can access resources or perform actions they shouldn't. It includes numerous Common Weakness Enumerations (CWEs) and is a prevalent risk.

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

Q:: In which type of code is access control effective in preventing broken access control?  
A:: Access control is only effective in trusted server-side code or server-less API, where attackers cannot modify access control checks or metadata.

Q:: What is the recommended default access control policy for resources?  
A:: Except for public resources, the recommended default access control policy is to deny access by default.

Q:: How should access control mechanisms be implemented and used?  
A:: Implement access control mechanisms once and re-use them throughout the application, including minimizing Cross-Origin Resource Sharing (CORS) usage.

Q:: What should model access controls enforce?  
A:: Model access controls should enforce record ownership rather than assuming that users can create, read, update, or delete any record.

Q:: How should unique application business limit requirements be enforced?  
A:: Unique application business limit requirements should be enforced by domain models.

Q:: Why is it important to disable web server directory listing?  
A:: Disabling web server directory listing helps prevent exposure of sensitive information and files and ensure file metadata (e.g., .git)

Q:: What should be done in case of access control failures?  
A:: Access control failures should be logged, and appropriate alerts, such as notifying administrators, should be triggered (e.g., repeated failures).

Q:: What is the purpose of rate limiting API and controller access?  
A:: Rate limiting API and controller access helps minimize the harm from automated attack tooling, preventing abuse of the application.

Q:: How should session identifiers be handled after logout?  
A:: Stateful session identifiers should be invalidated on the server after logout. Stateless JWT tokens should be short-lived, and for longer-lived JWTs, it's recommended to follow OAuth standards for revoking access.

Q:: What is the role of functional access control unit and integration tests in secure development?  
A:: Functional access control unit and integration tests are essential for ensuring that access control mechanisms are implemented correctly and that unauthorized access attempts are detected and prevented during the development and testing phases.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is being performed in this situation?

The application uses unverified data in a SQL call that is accessing account information:

```java
 pstmt.setString(1, request.getParameter("acct"));
 ResultSet results = pstmt.executeQuery( );
```

An attacker simply modifies the browser's 'acct' parameter to send whatever account number they want. If not correctly verified, the attacker can access any user's account.

```plaintext
 https://example.com/app/accountInfo?acct=notmyacct
```
A:: A01 Broken Access Control

Q:: What type of attack is happening here?

An attacker simply forces browsing to target URLs. Admin rights are required for access to the admin page.

```plaintext
 https://example.com/app/getappInfo
 https://example.com/app/admin_getappInfo
```

- If an unauthenticated user can access either page, it's a flaw.
- If a non-admin can access the admin page, this is a flaw.

A:: A01 Broken Access Control

### Part III - A02:2021-Cryptographic Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Crypto_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Cryptographic Failures" category about?  
A:: **A02:2021 - Cryptographic Failures**: This category, previously known as Sensitive Data Exposure (A3:2017), has been renamed to emphasize issues related to cryptographic failures. It often leads to sensitive data exposure or system compromise.

Q:: What data requires extra protection in terms of cryptography?  
A:: Data such as passwords, credit card numbers, health records, personal information, and business secrets require extra protection through cryptography, especially if they fall under privacy laws or regulations.

Q:: What is the concern regarding data transmitted in clear text?  
A:: Data transmitted in clear text, especially over external internet traffic, is vulnerable to interception. It's important to verify the security of all internal traffic as well, not just external communication.

Q:: What should you check for regarding cryptographic algorithms or protocols?  
A:: Check for the use of old or weak cryptographic algorithms or protocols, especially in older code.

Q:: Why is proper key management essential in cryptography?  
A:: Proper key management is essential to ensure that default crypto keys are not in use, weak crypto keys are not generated or reused, and keys are not accidentally checked into source code repositories.

Q:: Why is encryption enforcement important, and where can it be enforced?  
A:: Encryption enforcement is important to protect data. Ensure that encryption is enforced not just in external communication but also within internal systems, including between load balancers, web servers, or back-end systems.

Q:: What should you check regarding server certificates in cryptography?  
A:: Verify that the received server certificate and the trust chain are properly validated to prevent man-in-the-middle attacks.

Q:: What is the importance of initialization vectors in cryptographic operations?  
A:: Initialization vectors should not be ignored, reused, or generated in an insecure manner. The cryptographic mode of operation should be appropriate, and insecure modes like ECB should be avoided.

Q:: Why is using passwords as cryptographic keys a concern?  
A:: Using passwords as cryptographic keys without a proper key derivation function can lead to security vulnerabilities.

Q:: What is the significance of randomness in cryptographic purposes?  
A:: Randomness used for cryptographic purposes must meet cryptographic requirements and should not be overwritten with insufficiently unpredictable seeds by developers.

Q:: What are some deprecated hash functions that should be avoided in cryptography?  
A:: Deprecated hash functions like MD5 or SHA1 should be avoided, and cryptographic hash functions should be used when needed.

Q:: Why should cryptographic padding methods like PKCS #1 v1.5 be checked?  
A:: Check for the use of deprecated cryptographic padding methods like PKCS #1 v1.5 and avoid their usage.

Q:: How can cryptographic error messages or side channel information be exploited?  
A:: Cryptographic error messages or side channel information can be exploited, for example, in padding oracle attacks. They should be carefully managed to prevent security vulnerabilities.

Q:: What OWASP components should be referred to for guidance on cryptographic issues?  
A:: Refer to ASVS Crypto (V7), Data Protection (V9), and SSL/TLS (V10) for guidance on cryptographic issues.

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

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack involves the following situation?

An application encrypts credit card numbers in a database using automatic database encryption. However, this data is automatically decrypted when retrieved, allowing a SQL injection flaw to retrieve credit card numbers in clear text.

A:: A02 Cryptographic Failures

Q:: Can you identify the type of attack happening here?

A site doesn't use or enforce TLS for all pages or supports weak encryption. An attacker monitors network traffic (e.g., at an insecure wireless network), downgrades connections from HTTPS to HTTP, intercepts requests, and steals the user's session cookie. The attacker then replays this cookie and hijacks the user's (authenticated) session, accessing or modifying the user's private data. Instead of the above they could alter all transported data, e.g., the recipient of a money transfer.

A:: A02 Cryptographic Failures

Q:: What kind of attack is described in this situation?

The password database uses unsalted or simple hashes to store everyone's passwords. A file upload flaw allows an attacker to retrieve the password database. All the unsalted hashes can be exposed with a rainbow table of pre-calculated hashes. Hashes generated by simple or fast hash functions may be cracked by GPUs, even if they were salted.

A:: A02 Cryptographic Failures

### Part IV - A03:2021-Injection

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Injection.png)

#### Chapter 1 - Overview

Q:: What is the "Injection" category about?  
A:: **A03:2021 - Injection**: Injection vulnerabilities have moved down to the third position. It includes various forms of injection attacks, such as SQL injection, and now also includes Cross-Site Scripting (XSS).

Q:: What makes an application vulnerable to injection attacks?  
A:: An application is vulnerable to injection attacks when:
- User-supplied data is not properly validated, filtered, or sanitized.
- Dynamic queries or non-parameterized calls are used without context-aware escaping.
- Hostile data is used in ORM search parameters.
- Hostile data is directly used or concatenated in SQL queries, commands, or stored procedures.

Q:: What is the risk of not validating user-supplied data in an application?  
A:: Not validating user-supplied data can lead to injection vulnerabilities, where attackers can manipulate input to execute malicious code.

Q:: Why is it important to use parameterized calls and context-aware escaping?  
A:: Parameterized calls and context-aware escaping help prevent injection vulnerabilities by ensuring that input data is treated as data, not code.

Q:: How can attackers exploit object-relational mapping (ORM) search parameters?  
A:: Attackers can exploit ORM search parameters by using hostile data to extract additional, sensitive records from the database.

Q:: What is the danger of directly using or concatenating hostile data in dynamic queries or commands?  
A:: Directly using or concatenating hostile data in dynamic queries, commands, or stored procedures can lead to injection attacks, where malicious code is injected and executed.

Q:: What are some common examples of injection attacks?  
A:: Common examples of injection attacks include SQL, NoSQL, OS command, Object Relational Mapping (ORM), LDAP, and Expression Language (EL) or Object Graph Navigation Library (OGNL) injection

Q:: What is the most effective method to detect injection vulnerabilities in software applications?  
A:: The best method for detecting injection vulnerabilities in software applications is source code review.

Q:: In the context of application security, how can organizations incorporate automated testing?  
A:: Organizations can incorporate automated testing by including static (SAST), dynamic (DAST), and interactive (IAST) application security testing tools into the CI/CD pipeline.

Q:: Which types of data inputs should be subject to automated testing to identify injection flaws?  
A:: The types of data inputs that should be subject to automated testing to identify injection flaws include, parameters, headers, URL, cookies, JSON, SOAP, and XML data inputs.

#### Chapter 2 - How to Prevent?

### Part V - A04:2021-Insecure Design

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Insecure_Design.png)

#### Chapter 1 - Overview

Q:: What is the "Insecure Design" category about?  
A:: **A04:2021 - Insecure Design**: This is a new category for 2021, emphasizing the importance of secure design patterns, threat modeling, and reference architectures. Insecure design flaws cannot be fixed by perfect implementation alone.

#### Chapter 2 - How to Prevent?

### Part VI - A05:2021-Security Misconfiguration

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Security_Misconfiguration.png)

#### Chapter 1 - Overview

Q:: What is the "Security Misconfiguration" category about?  
A:: **A05:2021 - Security Misconfiguration**: This category has moved up from its previous ranking. It addresses issues related to misconfigurations in applications, which can lead to vulnerabilities. It now includes XML External Entities (XXE).

#### Chapter 2 - How to Prevent?

### Part VII - A06:2021-Vulnerable and Outdated Components

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Vulnerable_Outdated_Components.png)

#### Chapter 1 - Overview

Q:: What is the "Vulnerable and Outdated Components" category about?  
A:: **A06:2021 - Vulnerable and Outdated Components**: This category, previously titled "Using Components with Known Vulnerabilities," has moved up in the ranking. It focuses on the risks associated with outdated and vulnerable software components.

#### Chapter 2 - How to Prevent?

### Part VIII - A07:2021-Identification and Authentication Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Identification_and_Authentication_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Identification and Authentication Failures" category about?  
A:: **A07:2021 - Identification and Authentication Failures**: This category, formerly known as "Broken Authentication," has slid down in ranking. It now includes CWEs related to identification failures and is influenced by the availability of standardized frameworks.

#### Chapter 2 - How to Prevent?

### Part IX - A08:2021-Software and Data Integrity Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Software_and_Data_Integrity_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Software and Data Integrity Failures" category about?  
A:: **A08:2021 - Software and Data Integrity Failures**: This is a new category highlighting issues related to assumptions about software updates, critical data, and CI/CD pipelines without proper verification. It includes Insecure Deserialization from the previous edition.

#### Chapter 2 - How to Prevent?

### Part X - A09:2021-Security Logging and Monitoring Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Security_Logging_and_Monitoring_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Security Logging and Monitoring Failures" category about?  
A:: **A09:2021 - Security Logging and Monitoring Failures**: Previously known as "Insufficient Logging & Monitoring," this category has moved up in ranking and is expanded to include more types of failures related to security logging and monitoring.

#### Chapter 2 - How to Prevent?

### Part XI - A10:2021-Server-Side Request Forgery

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_SSRF.png)

#### Chapter 1 - Overview

Q:: What is the "Server-Side Request Forgery" category about?  
A:: ***A10:2021 - Server-Side Request Forgery**: Added from the Top 10 community survey, this category represents scenarios where security community members have identified the importance, even though it may not be widely illustrated in the data. It deals with the risk of server-side request forgery attacks.

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