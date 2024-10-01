# OAOT - Anki owasp top 10 - owasp

## Questions

### Part I - Introduction

#### Chapter 1 - What is OWASP?

Q:: What is OWASP?  
A:: A non-profit organization providing free resources on web application security.  
Example: OWASP offers tools like ZAP (Zed Attack Proxy) for security testing.

Q:: What is the OWASP Top 10?  
A:: A regularly updated list of the most critical web application security risks.  
Example: "Broken Access Control" was the top risk in the 2021 edition.

### Part II - A01:2021-Broken Access Control

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Broken_Access_Control.png)

#### Chapter 1 - Overview

Q:: What is "Broken Access Control" in OWASP Top 10 2021?  
A:: The most critical web application security risk, involving unauthorized access to resources or actions.  
Example: A regular user accessing admin functions by modifying the URL.

Q:: What is the main purpose of access control?  
A:: To enforce user permissions and prevent unauthorized actions.  
Example: Ensuring only HR staff can access employee salary information.

Q:: What is the "principle of least privilege"?  
A:: Granting users only the minimum permissions necessary for their tasks.  
Example: Giving a content editor rights to edit articles but not system settings.

Q:: How can access control checks be bypassed?  
A:: By manipulating requests, URLs, or application state.  
Example: Changing a user ID in a URL to access another user's profile.

Q:: What are "insecure direct object references"?  
A:: Exposing internal implementation objects without access checks.  
Example: Accessing order #123 by changing URL from order/789 to order/123.

Q:: Why are access controls important for POST, PUT, and DELETE requests?  
A:: To prevent unauthorized data modification or deletion.  
Example: Ensuring only account owners can delete their own posts.

Q:: What is "elevation of privilege"?  
A:: Gaining higher-level permissions than intended.  
Example: A regular user accessing admin features by modifying a cookie.

Q:: How can metadata manipulation be a security risk?  
A:: By altering tokens or hidden fields to gain unauthorized access.  
Example: Modifying a JWT token to change user roles or permissions.

Q:: What is CORS misconfiguration?  
A:: Improper setup of Cross-Origin Resource Sharing, allowing unauthorized access.  
Example: A misconfigured API accepting requests from any origin, not just trusted ones.

Q:: What is "force browsing"?  
A:: Attempting to access restricted pages by guessing URLs.  
Example: A user trying to access "/admin" pages without proper authentication.

#### Chapter 2 - How to Prevent?

Q:: Where should access control be implemented?  
A:: In trusted server-side code or server-less API.  
Example: Implementing user role checks in backend PHP code, not in JavaScript.

Q:: What's the recommended default access policy?  
A:: Deny access by default, except for public resources.  
Example: Requiring authentication for all pages except the homepage and login page.

Q:: How should access control mechanisms be used?  
A:: Implement once and reuse throughout the application.  
Example: Creating a central authorization service used by all app modules.

Q:: What should model access controls enforce?  
A:: Record ownership, not assuming users can access any record.  
Example: Ensuring users can only edit their own profile, not others'.

Q:: How to handle access control failures?  
A:: Log failures and trigger alerts for administrators.  
Example: Sending an email to admins after 5 failed access attempts in 1 minute.

Q:: Why implement rate limiting?  
A:: To minimize harm from automated attacks and prevent abuse.  
Example: Limiting API calls to 100 per hour per user.

Q:: How to handle session identifiers after logout?  
A:: Invalidate on the server; use short-lived JWTs for stateless sessions.  
Example: Deleting session data from the server when a user logs out.

Q:: What's the role of access control testing?  
A:: To ensure correct implementation and detect unauthorized access attempts.  
Example: Writing unit tests to verify admin functions are inaccessible to regular users.

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

Q:: What is "Cryptographic Failures" in OWASP Top 10 2021?  
A:: Security issues related to cryptography, often leading to data exposure.  
Example: Using outdated encryption algorithms like MD5 for password storage.

Q:: What types of data require extra cryptographic protection?  
A:: Sensitive information like passwords, credit card numbers, and personal data.  
Example: Encrypting social security numbers before storing in a database.

Q:: Why is clear text data transmission dangerous?  
A:: It's vulnerable to interception, especially over external networks.  
Example: Sending login credentials over HTTP instead of HTTPS.

Q:: What's the risk of using old cryptographic algorithms?  
A:: They may have known vulnerabilities, making data easier to compromise.  
Example: Using DES encryption, which is now considered insecure.

Q:: Why is proper key management crucial?  
A:: To prevent unauthorized access and ensure cryptographic integrity.  
Example: Regularly rotating encryption keys and securely storing them.

Q:: Where should encryption be enforced?  
A:: In all data transmissions, both external and internal.  
Example: Using TLS for communication between web servers and databases.

Q:: What's important about server certificates?  
A:: They should be properly validated to prevent man-in-the-middle attacks.  
Example: Checking certificate expiration dates and trusted certificate authorities.

Q:: Why are initialization vectors important in cryptography?  
A:: To ensure unique encryption results, even for identical data.  
Example: Using a unique IV for each AES encryption operation.

Q:: What's the risk of using passwords as cryptographic keys?  
A:: It can lead to weak encryption if not properly processed.  
Example: Directly using a user's password to encrypt files, instead of deriving a key.

Q:: Why is cryptographic randomness crucial?  
A:: To prevent predictability in security-critical operations.  
Example: Using a cryptographically secure random number generator for session tokens.

Q:: What's wrong with using deprecated hash functions?  
A:: They may have known vulnerabilities, compromising data integrity.  
Example: Using SHA-1 for digital signatures, which is vulnerable to collision attacks.

Q:: Why avoid deprecated cryptographic padding methods?  
A:: They can introduce vulnerabilities in encryption systems.  
Example: Avoiding PKCS #1 v1.5 padding in RSA encryption due to known attacks.

Q:: How can cryptographic error messages be exploited?  
A:: They may leak information useful for attacks.  
Example: A padding oracle attack exploiting detailed decryption error messages.

Q:: Where to find guidance on cryptographic best practices?  
A:: In OWASP resources like ASVS Crypto, Data Protection, and SSL/TLS sections.  
Example: Consulting ASVS V7 for proper key management practices.

#### Chapter 2 - How to Prevent?

Q:: What's the first step in preventing cryptographic failures?  
A:: Classify data and identify sensitive information.  
Example: Categorizing customer data as public, internal, or confidential.

Q:: Why discard unnecessary sensitive data?  
A:: To reduce the risk and impact of potential data breaches.  
Example: Deleting credit card details after a transaction is completed.

Q:: Why encrypt sensitive data at rest?  
A:: To protect data even if physical storage is compromised.  
Example: Encrypting stored passwords in case the database is stolen.

Q:: What's crucial for cryptographic algorithms and keys?  
A:: Use up-to-date, strong standards and proper key management.  
Example: Using AES-256 instead of DES, and rotating keys regularly.

Q:: How to protect data in transit?  
A:: Use secure protocols like TLS with forward secrecy.  
Example: Implementing HTTPS with TLS 1.3 on all web services.

Q:: Why disable caching for sensitive responses?  
A:: To prevent sensitive data from being stored in insecure locations.  
Example: Setting 'Cache-Control: no-store' for pages with personal info.

Q:: Why apply security controls based on data classification?  
A:: To ensure appropriate protection levels for different data types.  
Example: Using multi-factor authentication for accessing financial records.

Q:: Why avoid legacy protocols for sensitive data?  
A:: They lack modern security features and encryption.  
Example: Using SFTP instead of FTP for file transfers.

Q:: Why use strong, salted hashing for passwords?  
A:: To make password recovery from hashes extremely difficult.  
Example: Using bcrypt instead of MD5 for password storage.

Q:: How should initialization vectors (IVs) be used?  
A:: Chosen appropriately and never reused for the same key.  
Example: Using a unique IV for each AES-CBC encryption operation.

Q:: What's better than just encryption?  
A:: Authenticated encryption, ensuring both confidentiality and integrity.  
Example: Using AES-GCM instead of AES-CBC for data protection.

Q:: How should cryptographic keys be handled?  
A:: Generated randomly and stored securely as byte arrays.  
Example: Using a hardware security module (HSM) to generate and store keys.

Q:: What's important about cryptographic randomness?  
A:: It should be unpredictable and have high entropy.  
Example: Using /dev/urandom on Unix systems for random number generation.

Q:: Why avoid deprecated cryptographic functions?  
A:: They have known vulnerabilities and weaknesses.  
Example: Using SHA-256 instead of SHA-1 for digital signatures.

Q:: Why verify cryptographic configurations independently?  
A:: To ensure they're functioning correctly and providing intended protection.  
Example: Using third-party security audits to verify TLS configurations.

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

Q:: Why is confirmation of the user's identity, authentication, and session management critical?  
A:: Confirmation of the user's identity and proper authentication and session management are critical to protect against authentication-related attacks.

Q:: What are some signs of authentication weaknesses in an application?  
A:: Authentication weaknesses may be present if the application:

- Permits automated attacks like credential stuffing.

- Allows brute force or other automated attacks.

- Permits the use of default, weak, or well-known passwords.

- Uses ineffective credential recovery and forgot-password processes.

- Stores passwords in plain text, encrypted, or weakly hashed formats.

- Lacks or has ineffective multi-factor authentication.

- Exposes session identifiers in the URL.

- Reuses session identifiers after successful login.

- Fails to correctly invalidate session IDs.

Q:: What is credential stuffing, and why is it a concern?  
A:: Credential stuffing is when an attacker uses a list of valid usernames and passwords obtained from breaches to gain unauthorized access. It's a concern because it exploits weak authentication systems.

Q:: What is the risk associated with permitting brute force attacks?  
A:: Permitting brute force attacks poses a risk because attackers can systematically try various combinations of usernames and passwords until they find the correct combination to gain unauthorized access.

Q:: Why are default, weak, or well-known passwords a security risk?  
A:: Default, weak, or well-known passwords pose a security risk because they are easily guessable and can be exploited by attackers.

Q:: Why are "knowledge-based answers" for credential recovery not safe?  
A:: "Knowledge-based answers" for credential recovery are not safe because they can often be guessed or obtained through social engineering.

Q:: What are some issues with storing passwords in plain text, encrypted, or weakly hashed formats?  
A:: Storing passwords in such formats can lead to security vulnerabilities, as attackers can easily obtain and crack the passwords.

Q:: Why is multi-factor authentication important?  
A:: Multi-factor authentication adds an extra layer of security by requiring users to provide two or more forms of authentication, making it more challenging for attackers to gain access.

Q:: What are the risks associated with exposing session identifiers in the URL?  
A:: Exposing session identifiers in the URL can lead to session hijacking and unauthorized access.

Q:: How can reusing session identifiers after a successful login pose a security risk?  
A:: Reusing session identifiers after a successful login is risky because it can allow unauthorized users to continue or take over authenticated sessions, potentially compromising security.

Q:: Why is it essential to correctly invalidate session IDs?  
A:: Correctly invalidating session IDs ensures that user sessions or authentication tokens are terminated during logout or periods of inactivity, preventing unauthorized access.

#### Chapter 2 - How to Prevent?

Q:: What is the role of multi-factor authentication in preventing identification and authentication failures?  
A:: Multi-factor authentication should be implemented where possible to prevent automated credential stuffing, brute force, and stolen credential reuse attacks.

Q:: What should be avoided when shipping or deploying an application to prevent identification and authentication failures?  
A:: Do not ship or deploy with any default credentials, especially for admin users, to prevent unauthorized access.

Q:: How can weak password checks be implemented to prevent identification and authentication failures?  
A:: Implement weak password checks, such as testing new or changed passwords against the top 10,000 worst passwords list, to ensure stronger password choices.

Q:: What guidelines can be followed for password length, complexity, and rotation policies?  
A:: Align password length, complexity, and rotation policies with NIST 800-63b's guidelines in section 5.1.1 for Memorized Secrets or other modern, evidence-based password policies.

Q:: How can account enumeration attacks be prevented during registration and credential recovery?  
A:: Harden registration, credential recovery, and API pathways against account enumeration attacks by using the same messages for all outcomes.

Q:: Why is it important to limit or increasingly delay failed login attempts?  
A:: Limit or increasingly delay failed login attempts to prevent credential stuffing, brute force, or other attacks. However, ensure this does not create a denial of service scenario.

Q:: What are the characteristics of a secure session manager for preventing identification and authentication failures?  
A:: Use a server-side, secure, built-in session manager that generates a new random session ID with high entropy after login. The session identifier should not be in the URL, be securely stored, and invalidated after logout, idle, and absolute timeouts.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is happening in this scenario?

Credential stuffing, the use of lists of known passwords, is a common attack. Suppose an application does not implement automated threat or credential stuffing protection. In that case, the application can be used as a password oracle to determine if the credentials are valid.  
A:: A07 Identification and Authentication Failures

Q:: Can you identify the type of attack happening here?

Most authentication attacks occur due to the continued use of passwords as a sole factor. Once considered best practices, password rotation and complexity requirements encourage users to use and reuse weak passwords. Organizations are recommended to stop these practices per NIST 800-63 and use multi-factor authentication.  
A:: A07 Identification and Authentication Failures

Q:: What kind of attack is described in this situation?

Application session timeouts aren't set correctly. A user uses a public computer to access an application. Instead of selecting "logout," the user simply closes the browser tab and walks away. An attacker uses the same browser an hour later, and the user is still authenticated.  
A:: A07 Identification and Authentication Failures

### Part IX - A08:2021-Software and Data Integrity Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Software_and_Data_Integrity_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Software and Data Integrity Failures" category about?  
A:: **A08:2021 - Software and Data Integrity Failures**: This is a new category highlighting issues related to assumptions about software updates, critical data, and CI/CD pipelines without proper verification. It includes Insecure Deserialization from the previous edition.

Q:: How can relying on plugins, libraries, or modules from untrusted sources impact software integrity?  
A:: Relying on plugins, libraries, or modules from untrusted sources can impact software integrity by introducing potential security vulnerabilities, malicious code, or system compromise into the application.

Q:: What is the potential risk associated with an insecure CI/CD pipeline?  
A:: An insecure CI/CD pipeline can introduce the potential for unauthorized access, the injection of malicious code, or compromise of the system during the software development and deployment process.

Q:: What security concern is raised by auto-update functionality in applications?  
A:: Auto-update functionality in applications can be a security concern when updates are downloaded and applied without sufficient integrity verification. Attackers may exploit this to distribute and run their own malicious updates on all installations.

Q:: What is the concept of insecure deserialization, and why is it a vulnerability?  
A:: Insecure deserialization refers to the process of decoding or deserializing data from a serialized format. It becomes a vulnerability when an attacker can view and modify the serialized data, potentially leading to security issues.

Q:: How can organizations protect against software and data integrity failures?  
A:: Organizations can protect against software and data integrity failures by carefully vetting and verifying the sources of plugins, libraries, and modules, implementing secure CI/CD pipelines, conducting integrity verification for updates, and addressing insecure deserialization vulnerabilities.

Q:: How can organizations assess and mitigate the risks associated with insecure deserialization?  
A:: Organizations can assess and mitigate the risks of insecure deserialization by implementing input validation, using safe deserialization methods, and staying informed about potential vulnerabilities in the deserialization process.

#### Chapter 2 - How to Prevent?

Q:: How can digital signatures or similar mechanisms be used to prevent software and data integrity failures?  
A:: Digital signatures or similar mechanisms can be used to verify that the software or data is from the expected source and has not been altered, ensuring integrity.

Q:: Why is it important to ensure that libraries and dependencies are consuming trusted repositories?  
A:: Ensuring that libraries and dependencies use trusted repositories reduces the risk of including compromised or malicious components in your software.

Q:: How can software supply chain security tools like OWASP Dependency Check or OWASP CycloneDX be used to prevent integrity failures?  
A:: These tools can be used to verify that components do not contain known vulnerabilities, enhancing the integrity of your software.

Q:: What is the purpose of a review process for code and configuration changes in preventing integrity failures?  
A:: A review process minimizes the chance that malicious code or configuration could be introduced into your software pipeline, ensuring its integrity.

Q:: What role does proper segregation, configuration, and access control play in preventing integrity failures in CI/CD pipelines?  
A:: Proper segregation, configuration, and access control in CI/CD pipelines ensure the integrity of the code flowing through the build and deploy processes, preventing unauthorized changes.

Q:: How can the transmission of unsigned or unencrypted serialized data to untrusted clients be made more secure?  
A:: To enhance security, unsigned or unencrypted serialized data should not be sent to untrusted clients without some form of integrity check or digital signature to detect tampering or replay.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is demonstrated in this scenario?

Many home routers, set-top boxes, device firmware, and others do not verify updates via signed firmware. Unsigned firmware is a growing target for attackers and is expected to only get worse. This is a major concern as many times there is no mechanism to remediate other than to fix in a future version and wait for previous versions to age out.  
A:: A08 Software and Data Integrity Failures

Q:: Can you identify the type of attack happening here?

Nation-states have been known to attack update mechanisms, with a recent notable attack being the SolarWinds Orion attack. The company that develops the software had secure build and update integrity processes. Still, these were able to be subverted, and for several months, the firm distributed a highly targeted malicious update to more than 18,000 organizations, of which around 100 or so were affected. This is one of the most far-reaching and most significant breaches of this nature in history.  
A:: A08 Software and Data Integrity Failures

Q:: What kind of attack is described in this situation?

A React application calls a set of Spring Boot microservices. Being functional programmers, they tried to ensure that their code is immutable. The solution they came up with is serializing the user state and passing it back and forth with each request. An attacker notices the "rO0" Java object signature (in base64) and uses the Java Serial Killer tool to gain remote code execution on the application server.  
A:: A08 Software and Data Integrity Failures

### Part X - A09:2021-Security Logging and Monitoring Failures

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Security_Logging_and_Monitoring_Failures.png)

#### Chapter 1 - Overview

Q:: What is the "Security Logging and Monitoring Failures" category about?  
A:: **A09:2021 - Security Logging and Monitoring Failures**: Previously known as "Insufficient Logging & Monitoring," this category has moved up in ranking and is expanded to include more types of failures related to security logging and monitoring.

Q:: Why is logging and monitoring critical for security?  
A:: Logging and monitoring are critical for security because they help detect, escalate, and respond to active breaches. Without them, breaches cannot be detected.

Q:: What are some indicators of insufficient logging and monitoring?  
A:: Insufficient logging and monitoring occur when:

- Auditable events like logins and high-value transactions are not logged.

- Warnings and errors generate no, inadequate, or unclear log messages.

- Logs of applications and APIs are not monitored for suspicious activity.

- Logs are only stored locally.

- Alerting thresholds and response escalation processes are absent or ineffective.

- Penetration testing and DAST tool scans do not trigger alerts.

- The application cannot detect, escalate, or alert for active attacks in real-time or near real-time.

Q:: Why is it important to log auditable events like logins and high-value transactions?  
A:: Logging auditable events is important for tracking and auditing user actions, which can help in detecting unauthorized or malicious activity.

Q:: What is the risk of generating inadequate or unclear log messages for warnings and errors?  
A:: Inadequate or unclear log messages can hinder the ability to understand and respond to potential issues or attacks.

Q:: Why should logs of applications and APIs be monitored for suspicious activity?  
A:: Monitoring logs for suspicious activity is crucial for early detection of security threats and breaches.

Q:: What are the consequences of only storing logs locally?  
A:: Storing logs only locally can be a security risk because it may result in the loss of critical log data in the event of a breach or system failure, making it difficult to investigate incidents.

Q:: What is the significance of alerting thresholds and response escalation processes?  
A:: Alerting thresholds and response escalation processes help ensure that security incidents are promptly detected, reported, and escalated for action.

Q:: How can penetration testing and DAST tool scans be integrated with monitoring?  
A:: Penetration testing and DAST tool scans should trigger alerts when potential vulnerabilities or attacks are detected.

Q:: Why is real-time or near real-time detection of active attacks important?  
A:: Real-time or near real-time detection of active attacks allows for immediate response, reducing the potential impact of security incidents.

#### Chapter 2 - How to Prevent?

Q:: What should be ensured regarding the logging of login, access control, and server-side input validation failures?  
A:: Ensure that all login, access control, and server-side input validation failures can be logged with sufficient user context to identify suspicious or malicious accounts and held for enough time for forensic analysis.

Q:: Why is it important to generate logs in a format that log management solutions can easily consume?  
A:: Logs should be generated in a format that log management solutions can easily consume to facilitate efficient analysis and monitoring.

Q:: How can log data be protected from injections or attacks on logging and monitoring systems?  
A:: Ensure log data is encoded correctly to prevent injections or attacks on the logging or monitoring systems, enhancing data integrity.

Q:: What should be established for high-value transactions to prevent tampering or deletion?  
A:: High-value transactions should have an audit trail with integrity controls to prevent tampering or deletion, such as append-only database tables or similar mechanisms.

Q:: What is the role of DevSecOps teams in preventing security logging and monitoring failures?  
A:: DevSecOps teams should establish effective monitoring and alerting systems to quickly detect and respond to suspicious activities, enhancing security.

Q:: What plans should be established or adopted to address security incidents?  
A:: Establish or adopt an incident response and recovery plan, such as NIST 800-61r2 or later, to effectively address security incidents.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is illustrated in this scenario?

A children's health plan provider's website operator couldn't detect a breach due to a lack of monitoring and logging. An external party informed the health plan provider that an attacker had accessed and modified thousands of sensitive health records of more than 3.5 million children. A post-incident review found that the website developers had not addressed significant vulnerabilities. As there was no logging or monitoring of the system, the data breach could have been in progress since 2013, a period of more than seven years.  
A:: A09 Security Logging and Monitoring Failures

Q:: Can you identify the type of attack happening here?

A major Indian airline had a data breach involving more than ten years' worth of personal data of millions of passengers, including passport and credit card data. The data breach occurred at a third-party cloud hosting provider, who notified the airline of the breach after some time.  
A:: A09 Security Logging and Monitoring Failures

Q:: What kind of attack is described in this situation?

A major European airline suffered a GDPR reportable breach. The breach was reportedly caused by payment application security vulnerabilities exploited by attackers, who harvested more than 400,000 customer payment records. The airline was fined 20 million pounds as a result by the privacy regulator.  
A:: A09 Security Logging and Monitoring Failures

### Part XI - A10:2021-Server-Side Request Forgery

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_SSRF.png)

#### Chapter 1 - Overview

Q:: What is the "Server-Side Request Forgery" category about?  
A:: ***A10:2021 - Server-Side Request Forgery**: Added from the Top 10 community survey, this category represents scenarios where security community members have identified the importance, even though it may not be widely illustrated in the data. It deals with the risk of server-side request forgery attacks.

Q:: What is SSRF, and when does it occur in web applications?  
A:: SSRF stands for Server-Side Request Forgery, and it occurs in web applications when they fetch a remote resource without properly validating the user-supplied URL. It allows attackers to manipulate the application into sending crafted requests to unexpected destinations.

Q:: What can make SSRF attacks particularly severe?  
A:: SSRF attacks can be particularly severe due to the growing adoption of cloud services and the increasing complexity of application architectures. These factors raise the potential impact of SSRF vulnerabilities.

Q:: How can SSRF vulnerabilities occur in modern web applications?  
A:: SSRF vulnerabilities are increasingly common in modern web applications because fetching URLs has become a standard scenario. This convenience feature can inadvertently expose applications to SSRF risks.

Q:: Why is it a concern that SSRF can bypass network access control mechanisms like firewalls and VPNs?  
A:: SSRF is a concern because it allows attackers to coerce the application into sending requests to unexpected destinations even when protected by firewalls, VPNs, or other network access control lists (ACLs).

#### Chapter 2 - How to Prevent?

Q:: How can SSRF be reduced from a network layer?  
A:: SSRF can be reduced by segmenting remote resource access functionality in separate networks.

Q:: What policies can be enforced to prevent SSRF?  
A:: "Deny by default" firewall policies or network access control rules can be enforced to block all but essential intranet traffic.

Q:: What should be built around firewall rules based on applications to prevent SSRF?  
A:: An ownership and a lifecycle should be established for firewall rules based on applications.

Q:: What is recommended for logging on firewalls to prevent SSRF?  
A:: It is recommended to log all accepted and blocked network flows on firewalls to prevent SSRF.

Q:: What does SSRF stand for in the context of web application security?  
A:: Server-Side Request Forgery.

Q:: Why should developers sanitize and validate all client-supplied input data to prevent SSRF?  
A:: To eliminate harmful, strange, or unexpected data which may lead to SSRF attack.

Q:: In SSRF prevention, how does enforcing the URL schema, port, and destination with a positive allow list help?  
A:: It restricts the outbound HTTP traffic to trusted and known destinations, thereby reducing SSRF attack surface.

Q:: Why is it important not to send raw responses to clients as part of SSRF prevention?  
A:: It prevents the exposure of potentially sensitive information obtained from the attack to the client.

Q:: Why should HTTP redirections be disabled in preventing SSRF attacks?  
A:: To stop the application from being tricked into accessing untrusted or manipulated sites.

Q:: What attack risks can you avoid by being aware of the URL consistency?  
A:: DNS rebinding attacks and TOCTOU (time of check, time of use) race conditions.

Q:: Why is denial list or regular expression mitigation not advised in preventing SSRF attacks?  
A:: Because attackers have payload lists, tools, and masking techniques to bypass these security measures.

Q:: Why is it important not to deploy other security-relevant services on front systems?  
A:: It's important not to deploy other security-relevant services on front systems to minimize the attack surface. By keeping front systems dedicated to their primary purpose, you reduce the risk of exposing additional attack vectors.

Q:: How can you control local traffic on front systems to enhance security?  
A:: You can control local traffic on front systems by ensuring that requests to security-relevant services are restricted to the local system, for example, by using "localhost" as the destination address.

Q:: What is the recommended security measure for frontends with dedicated and manageable user groups?  
A:: For frontends with dedicated and manageable user groups, it is recommended to use network encryption, such as VPNs, on independent systems. This is advised for scenarios where very high protection needs exist.

#### Chapter 3 - Example Attack Scenarios

Q:: What type of attack is demonstrated in this scenario?

Port scan internal servers – If the network architecture is unsegmented, attackers can map out internal networks and determine if ports are open or closed on internal servers from connection results or elapsed time to connect or reject SSRF payload connections.  
A:: A10 Server Side Request Forgery (SSRF)

Q:: Can you identify the type of attack happening here?

Sensitive data exposure – Attackers can access local files or internal services to gain sensitive information such as `file:///etc/passwd` and `http://localhost:28017/`.  
A:: A10 Server Side Request Forgery (SSRF)

Q:: What kind of attack is described in this situation?

Access metadata storage of cloud services – Most cloud providers have metadata storage such as `http://169.254.169.254/`. An attacker can read the metadata to gain sensitive information.  
A:: A10 Server Side Request Forgery (SSRF)

Q:: What type of attack is being demonstrated here?

Compromise internal services – The attacker can abuse internal services to conduct further attacks such as Remote Code Execution (RCE) or Denial of Service (DoS).  
A:: A10 Server Side Request Forgery (SSRF)

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```