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

Q:: What is the preferred option to prevent injection attacks?  
A:: The preferred option is to use a safe API that avoids using the interpreter entirely, provides a parameterized interface, or migrates to Object Relational Mapping Tools (ORMs).

> **Note:** Even when parameterized, stored procedures can still introduce SQL injection if PL/SQL or T-SQL concatenates queries and data or executes hostile data with EXECUTE IMMEDIATE or exec().

Q:: Can stored procedures introduce SQL injection vulnerabilities?  
A:: Yes, even when parameterized, stored procedures can introduce SQL injection if PL/SQL or T-SQL concatenates queries and data or executes hostile data with EXECUTE IMMEDIATE or exec().

Q:: What is the role of positive server-side input validation in preventing injection?  
A:: Positive server-side input validation helps prevent injection by ensuring that input adheres to expected patterns and formats. However, it's not a complete defense in cases where special characters are required.

Q:: How can special characters in residual dynamic queries be handled to prevent injection?  
A:: Special characters in residual dynamic queries should be escaped using the specific escape syntax for that interpreter.

> **Note:** SQL structures such as table names, column names, and so on cannot be escaped, and thus user-supplied structure names are dangerous. This is a common issue in report-writing software.

Q:: What is the limitation of escaping user-supplied structure names in SQL queries?  
A:: User-supplied structure names, such as table names or column names, cannot be escaped, making them dangerous if directly used in queries. This is a common issue in report-writing software.

Q:: How can mass disclosure of records in case of SQL injection be prevented?  
A:: To prevent mass disclosure of records in case of SQL injection, use controls like LIMIT and other SQL controls within queries.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is being carried out in this situation?

An application uses untrusted data in the construction of the following vulnerable SQL call:

```java
String query = "SELECT * FROM accounts WHERE custID='" + request.getParameter("id") + "'";
```  
A:: A03 Injection

Q:: Can you identify the type of attack happening here?

Similarly, an application’s blind trust in frameworks may result in queries that are still vulnerable, (e.g., Hibernate Query Language (HQL)):

```java
Query HQLQuery = session.createQuery("FROM accounts WHERE custID='" + request.getParameter("id") + "'");
```

In both cases, the attacker modifies the ‘id’ parameter value in their browser to send: ' UNION SLEEP(10);--. For example:

```plaintext
http://example.com/app/accountView?id=' UNION SELECT SLEEP(10);--
```

This changes the meaning of both queries to return all the records from the accounts table. More dangerous attacks could modify or delete data or even invoke stored procedures.  
A:: A03 Injection

### Part V - A04:2021-Insecure Design

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Insecure_Design.png)

#### Chapter 1 - Overview

Q:: What is the "Insecure Design" category about?  
A:: **A04:2021 - Insecure Design**: This is a new category for 2021, emphasizing the importance of secure design patterns, threat modeling, and reference architectures. Insecure design flaws cannot be fixed by perfect implementation alone.

Q:: How is insecure design different from insecure implementation?  
A:: Insecure design and insecure implementation are different. Insecure design relates to weaknesses in control design, while insecure implementation refers to defects in the actual coding. They have different root causes and require different remediation approaches.

Q:: Can a secure design have implementation defects that lead to vulnerabilities?  
A:: Yes, a secure design can still have implementation defects that may result in vulnerabilities. However, an insecure design, by definition, lacks the necessary security controls to defend against specific attacks and cannot be fixed by perfect implementation.

Q:: What contributes to insecure design in software development?  
A:: One factor contributing to insecure design is the lack of business risk profiling in the software or system being developed, leading to a failure to determine the required level of security design.

Q:: What should be considered during requirements and resource management in secure design?  
A:: During requirements and resource management, collect and negotiate business requirements, protection requirements (confidentiality, integrity, availability, authenticity), and technical requirements. Plan and budget for all design, build, testing, and operation activities, including security.

Q:: What is the importance of secure design in preventing known attack methods?  
A:: Secure design constantly evaluates threats and ensures that code is robustly designed and tested to prevent known attack methods. It is a proactive approach to security.

Q:: How can threat modeling be integrated into the software development process?  
A:: Threat modeling can be integrated into refinement sessions or similar activities during user story development. It involves analyzing data flows, access control, security controls, and assumptions related to expected and failure flows.

Q:: Why is it important to involve security specialists throughout the software development lifecycle?  
A:: Involving security specialists from the beginning of a software project and throughout its lifecycle is crucial to ensure secure development. It helps identify and address security concerns early.

Q:: What is the OWASP Software Assurance Maturity Model (SAMM), and how can it be used?  
A:: The OWASP SAMM is a model that helps structure secure software development efforts. It can be leveraged to guide and improve the security practices and maturity of a software development organization.

Q:: Is secure design a one-time addition, or is it an ongoing practice in software development?  
A:: Secure design is not a one-time addition but a culture and methodology that should be integrated into the entire software development lifecycle. It involves continuous evaluation of threats and proactive security measures.

#### Chapter 2 - How to Prevent?

Q:: What is the role of AppSec professionals in preventing insecure design?  
A:: AppSec professionals can help evaluate and design security and privacy-related controls as part of a secure development lifecycle.

Q:: How can a library of secure design patterns be useful in preventing insecure design?  
A:: A library of secure design patterns provides ready-to-use components that adhere to secure design principles, reducing the risk of insecure design choices.

Q:: What is threat modeling, and how can it be used to prevent insecure design?  
A:: Threat modeling involves identifying and evaluating potential threats to critical aspects of the application, including authentication, access control, business logic, and key flows, helping prevent insecure design decisions.

Q:: How can security language and controls be integrated into user stories?  
A:: Integrating security language and controls into user stories ensures that security considerations are part of the development process from the beginning.

Q:: Why is it important to integrate plausibility checks at each tier of the application?  
A:: Integrating plausibility checks at each tier ensures that inputs and processes are checked for validity and correctness, reducing the risk of insecure design.

Q:: What is the purpose of unit and integration tests in preventing insecure design?  
A:: Unit and integration tests validate that all critical flows in the application are resistant to the threat model, ensuring that insecure design choices are not present.

Q:: How can tier layers be segregated on the system and network layers?  
A:: Tier layers can be segregated based on their exposure and protection needs to prevent insecure design.

Q:: Why is tenant segregation important in preventing insecure design?  
A:: Tenant segregation ensures that tenants (e.g., different customers or users) are kept separate throughout all tiers of the application, preventing insecure design.

Q:: How can resource consumption be limited to prevent insecure design?  
A:: Resource consumption can be limited by user or service to prevent excessive resource usage that could lead to insecure design.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is associated with this situation?

A credential recovery workflow might include “questions and answers,” which is prohibited by NIST 800-63b, the OWASP ASVS, and the OWASP Top 10. Questions and answers cannot be trusted as evidence of identity as more than one person can know the answers, which is why they are prohibited. Such code should be removed and replaced with a more secure design.  
A:: A04 Insecure Design

Q:: Can you identify the type of attack happening here?

A cinema chain allows group booking discounts and has a maximum of fifteen attendees before requiring a deposit. Attackers could threat model this flow and test if they could book six hundred seats and all cinemas at once in a few requests, causing a massive loss of income.  
A:: A04 Insecure Design

Q:: What kind of attack is described in this situation?

A retail chain’s e-commerce website does not have protection against bots run by scalpers buying high-end video cards to resell on auction websites. This creates terrible publicity for the video card makers and retail chain owners and enduring bad blood with enthusiasts who cannot obtain these cards at any price. Careful anti-bot design and domain logic rules, such as purchases made within a few seconds of availability, might identify inauthentic purchases and reject such transactions.  
A:: A04 Insecure Design

### Part VI - A05:2021-Security Misconfiguration

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Security_Misconfiguration.png)

#### Chapter 1 - Overview

Q:: What is the "Security Misconfiguration" category about?  
A:: **A05:2021 - Security Misconfiguration**: This category has moved up from its previous ranking. It addresses issues related to misconfigurations in applications, which can lead to vulnerabilities. It now includes XML External Entities (XXE).

Q:: What makes an application vulnerable to security misconfigurations?  
A:: An application is vulnerable to security misconfigurations if:
- Appropriate security hardening is missing across any part of the application stack.
- Permissions on cloud services are improperly configured.
- Unnecessary features are enabled or installed.
- Default accounts and their passwords remain enabled and unchanged.
- Error handling reveals overly informative error messages.
- Latest security features are disabled for upgraded systems.
- Security settings in application servers, frameworks, libraries, databases, etc., are not configured securely.
- Security headers or directives are missing or not set to secure values.
- The software is out of date or vulnerable. (see [A06:2021-Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/)).

Q:: What is the risk of missing security hardening across the application stack?  
A:: Missing security hardening across the application stack can lead to vulnerabilities and exploitation by attackers.

Q:: Why should unnecessary features not be enabled or installed?  
A:: Enabling unnecessary features can increase the attack surface and provide opportunities for attackers to exploit vulnerabilities.

Q:: What is the danger of keeping default accounts and passwords enabled and unchanged?  
A:: Keeping default accounts and passwords unchanged can lead to unauthorized access to the system.

Q:: What is the risk of revealing stack traces or overly informative error messages to users?  
A:: Revealing stack traces or overly informative error messages can provide valuable information to attackers and aid in exploiting vulnerabilities.

Q:: Why is it important to configure the latest security features securely for upgraded systems?  
A:: Configuring the latest security features securely is crucial to ensure that upgraded systems remain protected against new threats.

Q:: What components should have their security settings configured to secure values?  
A:: Security settings in application servers, application frameworks (e.g., Struts, Spring, ASP.NET), libraries, databases, and other components should be configured to secure values.

Q:: Why should security headers or directives be set to secure values?  
A:: Setting security headers or directives to secure values helps protect the application against various security threats.

Q:: What should be considered in terms of software to avoid vulnerabilities?  
A:: To avoid vulnerabilities, it is essential to ensure that the software is up-to-date and not vulnerable to known security issues, as highlighted in [A06:2021-Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/).

Q:: Why is a concerted, repeatable application security configuration process important?  
A:: A concerted, repeatable application security configuration process is important because it reduces the risk of vulnerabilities by ensuring consistent and secure settings across the application and its components, helping to protect against potential threats.

#### Chapter 2 - How to Prevent?

Q:: What is the role of a repeatable hardening process in preventing security misconfigurations?  
A:: A repeatable hardening process makes it fast and easy to deploy secure environments and ensures that development, QA, and production environments are configured identically.

Q:: Why is it important to have a minimal platform without unnecessary features and components?  
A:: A minimal platform reduces the attack surface by eliminating unused features and frameworks, preventing security misconfigurations.

Q:: What is the purpose of reviewing and updating configurations as part of the patch management process?  
A:: Reviewing and updating configurations as part of patch management ensures that security notes, updates, and patches are applied to maintain a secure environment.

Q:: How can a segmented application architecture prevent security misconfigurations?  
A:: A segmented application architecture provides secure separation between components or tenants using techniques like segmentation, containerization, or cloud security groups (ACLs).

Q:: What is the significance of sending security directives to clients, such as Security Headers?  
A:: Sending security directives to clients via headers helps ensure that client-side security settings align with the desired security posture.

Q:: How can the effectiveness of configurations and settings be verified in all environments?  
A:: An automated process should be used to verify the effectiveness of configurations and settings in all environments to prevent security misconfigurations.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is taking place in this situation?

The application server comes with sample applications not removed from the production server. These sample applications have known security flaws attackers use to compromise the server. Suppose one of these applications is the admin console, and default accounts weren't changed. In that case, the attacker logs in with default passwords and takes over.  
A:: A05 Security Misconfiguration

Q:: Can you identify the type of attack happening here?

Directory listing is not disabled on the server. An attacker discovers they can simply list directories. The attacker finds and downloads the compiled Java classes, which they decompile and reverse engineer to view the code. The attacker then finds a severe access control flaw in the application.  
A:: A05 Security Misconfiguration

Q:: What kind of attack is described in this situation?

The application server's configuration allows detailed error messages, e.g., stack traces, to be returned to users. This potentially exposes sensitive information or underlying flaws such as component versions that are known to be vulnerable.  
A:: A05 Security Misconfiguration

Q:: What type of attack is being demonstrated here?

A cloud service provider (CSP) has default sharing permissions open to the Internet by other CSP users. This allows sensitive data stored within cloud storage to be accessed.  
A:: A05 Security Misconfiguration

### Part VII - A06:2021-Vulnerable and Outdated Components

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Vulnerable_Outdated_Components.png)

#### Chapter 1 - Overview

Q:: What is the "Vulnerable and Outdated Components" category about?  
A:: **A06:2021 - Vulnerable and Outdated Components**: This category, previously titled "Using Components with Known Vulnerabilities," has moved up in the ranking. It focuses on the risks associated with outdated and vulnerable software components.

Q:: Why is it crucial to know the versions of all components you use in your software?  
A:: It's crucial to know the versions of all components to avoid vulnerabilities and ensure software security.

Q:: What can happen if your software is using vulnerable, unsupported, or outdated components?  
A:: Using such components can lead to security risks and potential exploitation of vulnerabilities.

Q:: How can you proactively address vulnerabilities related to the components you use in your software?  
A:: Regularly scanning for vulnerabilities and subscribing to security bulletins is a proactive approach.

Q:: What are the consequences of not fixing or upgrading underlying platform, frameworks, and dependencies in a timely manner?  
A:: Delaying these updates can expose your organization to unnecessary risks from known vulnerabilities.

Q:: How can software developers contribute to mitigating risks related to components in software?  
A:: Software developers can contribute by testing the compatibility of updated, upgraded, or patched libraries.

Q:: In addition to updating components, what else can help secure software components?  
A:: Securing the components' configurations is also important to prevent security misconfigurations. (see [A05:2021-Security Misconfiguration](https://owasp.org/Top10/A05_2021-Security_Misconfiguration/)).

#### Chapter 2 - How to Prevent?

Q:: What should be removed as part of the patch management process to prevent vulnerabilities?  
A:: As part of the patch management process, remove unused dependencies, unnecessary features, components, files, and documentation to reduce the attack surface.

Q:: How can the versions of client-side and server-side components be continuously inventoried?  
A:: Continuously inventory component versions and dependencies using tools like versions, OWASP Dependency Check, retire.js, etc. Monitor sources like CVE and NVD for vulnerabilities and use software composition analysis tools for automation.

Q:: What is the importance of obtaining components from official sources over secure links?  
A:: Obtaining components from official sources over secure links reduces the risk of including modified, malicious components and enhances software and data integrity. (See [A08:2021-Software and Data Integrity Failures](https://owasp.org/Top10/A08_2021-Software_and_Data_Integrity_Failures/)).

Q:: How can libraries and components that are unmaintained or lack security patches be handled?  
A:: Monitor for unmaintained libraries and components and consider deploying virtual patches to monitor, detect, or protect against discovered issues when patching is not possible.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is demonstrated in this scenario?

Components typically run with the same privileges as the application itself, so flaws in any component can result in serious impact. Such flaws can be accidental (e.g., coding error) or intentional (e.g., a backdoor in a component). Some example exploitable component vulnerabilities discovered are:

- CVE-2017-5638, a Struts 2 remote code execution vulnerability that enables the execution of arbitrary code on the server, has been blamed for significant breaches.

- While the internet of things (IoT) is frequently difficult or impossible to patch, the importance of patching them can be great (e.g., biomedical devices).

There are automated tools to help attackers find unpatched or misconfigured systems. For example, the Shodan IoT search engine can help you find devices that still suffer from Heartbleed vulnerability patched in April 2014.  
A:: A06 Vulnerable and Outdated Components

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