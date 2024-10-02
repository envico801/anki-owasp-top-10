# OAOT - Anki owasp top 10 - owasp

## Questions

### Part I - Introduction

#### Chapter 1 - What is OWASP?

Q:: What is OWASP?  
A:: A non-profit organization providing free resources on web application security.  
**Example**: OWASP offers tools like ZAP (Zed Attack Proxy) for security testing.

Q:: What is the OWASP Top 10?  
A:: A regularly updated list of the most critical web application security risks.  
**Example**: "Broken Access Control" was the top risk in the 2021 edition.

### Part II - A01:2021-Broken Access Control

![icon](https://owasp.org/Top10/assets/TOP_10_Icons_Final_Broken_Access_Control.png)

#### Chapter 1 - Overview

Q:: What is "Broken Access Control" in OWASP Top 10 2021?  
A:: The most critical web application security risk, involving unauthorized access to resources or actions.  
**Example**: A regular user accessing admin functions by modifying the URL.

Q:: What is the main purpose of access control?  
A:: To enforce user permissions and prevent unauthorized actions.  
**Example**: Ensuring only HR staff can access employee salary information.

Q:: What is the "principle of least privilege"?  
A:: Granting users only the minimum permissions necessary for their tasks.  
**Example**: Giving a content editor rights to edit articles but not system settings.

Q:: How can access control checks be bypassed?  
A:: By manipulating requests, URLs, or application state.  
**Example**: Changing a user ID in a URL to access another user's profile.

Q:: What are "insecure direct object references"?  
A:: Exposing internal implementation objects without access checks.  
**Example**: Accessing order #123 by changing URL from order/789 to order/123.

Q:: Why are access controls important for POST, PUT, and DELETE requests?  
A:: To prevent unauthorized data modification or deletion.  
**Example**: Ensuring only account owners can delete their own posts.

Q:: What is "elevation of privilege"?  
A:: Gaining higher-level permissions than intended.  
**Example**: A regular user accessing admin features by modifying a cookie.

Q:: How can metadata manipulation be a security risk?  
A:: By altering tokens or hidden fields to gain unauthorized access.  
**Example**: Modifying a JWT token to change user roles or permissions.

Q:: What is CORS misconfiguration?  
A:: Improper setup of Cross-Origin Resource Sharing, allowing unauthorized access.  
**Example**: A misconfigured API accepting requests from any origin, not just trusted ones.

Q:: What is "force browsing"?  
A:: Attempting to access restricted pages by guessing URLs.  
**Example**: A user trying to access "/admin" pages without proper authentication.

#### Chapter 2 - How to Prevent?

Q:: Where should access control be implemented?  
A:: In trusted server-side code or server-less API.  
**Example**: Implementing user role checks in backend PHP code, not in JavaScript.

Q:: What's the recommended default access policy?  
A:: Deny access by default, except for public resources.  
**Example**: Requiring authentication for all pages except the homepage and login page.

Q:: How should access control mechanisms be used?  
A:: Implement once and reuse throughout the application.  
**Example**: Creating a central authorization service used by all app modules.

Q:: What should model access controls enforce?  
A:: Record ownership, not assuming users can access any record.  
**Example**: Ensuring users can only edit their own profile, not others'.

Q:: How to handle access control failures?  
A:: Log failures and trigger alerts for administrators.  
**Example**: Sending an email to admins after 5 failed access attempts in 1 minute.

Q:: Why implement rate limiting?  
A:: To minimize harm from automated attacks and prevent abuse.  
**Example**: Limiting API calls to 100 per hour per user.

Q:: How to handle session identifiers after logout?  
A:: Invalidate on the server; use short-lived JWTs for stateless sessions.  
**Example**: Deleting session data from the server when a user logs out.

Q:: What's the role of access control testing?  
A:: To ensure correct implementation and detect unauthorized access attempts.  
**Example**: Writing unit tests to verify admin functions are inaccessible to regular users.

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
**Example**: Using outdated encryption algorithms like MD5 for password storage.

Q:: What types of data require extra cryptographic protection?  
A:: Sensitive information like passwords, credit card numbers, and personal data.  
**Example**: Encrypting social security numbers before storing in a database.

Q:: Why is clear text data transmission dangerous?  
A:: It's vulnerable to interception, especially over external networks.  
**Example**: Sending login credentials over HTTP instead of HTTPS.

Q:: What's the risk of using old cryptographic algorithms?  
A:: They may have known vulnerabilities, making data easier to compromise.  
**Example**: Using DES encryption, which is now considered insecure.

Q:: Why is proper key management crucial?  
A:: To prevent unauthorized access and ensure cryptographic integrity.  
**Example**: Regularly rotating encryption keys and securely storing them.

Q:: Where should encryption be enforced?  
A:: In all data transmissions, both external and internal.  
**Example**: Using TLS for communication between web servers and databases.

Q:: What's important about server certificates?  
A:: They should be properly validated to prevent man-in-the-middle attacks.  
**Example**: Checking certificate expiration dates and trusted certificate authorities.

Q:: Why are initialization vectors important in cryptography?  
A:: To ensure unique encryption results, even for identical data.  
**Example**: Using a unique IV for each AES encryption operation.

Q:: What's the risk of using passwords as cryptographic keys?  
A:: It can lead to weak encryption if not properly processed.  
**Example**: Directly using a user's password to encrypt files, instead of deriving a key.

Q:: Why is cryptographic randomness crucial?  
A:: To prevent predictability in security-critical operations.  
**Example**: Using a cryptographically secure random number generator for session tokens.

Q:: What's wrong with using deprecated hash functions?  
A:: They may have known vulnerabilities, compromising data integrity.  
**Example**: Using SHA-1 for digital signatures, which is vulnerable to collision attacks.

Q:: Why avoid deprecated cryptographic padding methods?  
A:: They can introduce vulnerabilities in encryption systems.  
**Example**: Avoiding PKCS #1 v1.5 padding in RSA encryption due to known attacks.

Q:: How can cryptographic error messages be exploited?  
A:: They may leak information useful for attacks.  
**Example**: A padding oracle attack exploiting detailed decryption error messages.

Q:: Where to find guidance on cryptographic best practices?  
A:: In OWASP resources like ASVS Crypto, Data Protection, and SSL/TLS sections.  
**Example**: Consulting ASVS V7 for proper key management practices.

#### Chapter 2 - How to Prevent?

Q:: What's the first step in preventing cryptographic failures?  
A:: Classify data and identify sensitive information.  
**Example**: Categorizing customer data as public, internal, or confidential.

Q:: Why discard unnecessary sensitive data?  
A:: To reduce the risk and impact of potential data breaches.  
**Example**: Deleting credit card details after a transaction is completed.

Q:: Why encrypt sensitive data at rest?  
A:: To protect data even if physical storage is compromised.  
**Example**: Encrypting stored passwords in case the database is stolen.

Q:: What's crucial for cryptographic algorithms and keys?  
A:: Use up-to-date, strong standards and proper key management.  
**Example**: Using AES-256 instead of DES, and rotating keys regularly.

Q:: How to protect data in transit?  
A:: Use secure protocols like TLS with forward secrecy.  
**Example**: Implementing HTTPS with TLS 1.3 on all web services.

Q:: Why disable caching for sensitive responses?  
A:: To prevent sensitive data from being stored in insecure locations.  
**Example**: Setting 'Cache-Control: no-store' for pages with personal info.

Q:: Why apply security controls based on data classification?  
A:: To ensure appropriate protection levels for different data types.  
**Example**: Using multi-factor authentication for accessing financial records.

Q:: Why avoid legacy protocols for sensitive data?  
A:: They lack modern security features and encryption.  
**Example**: Using SFTP instead of FTP for file transfers.

Q:: Why use strong, salted hashing for passwords?  
A:: To make password recovery from hashes extremely difficult.  
**Example**: Using bcrypt instead of MD5 for password storage.

Q:: How should initialization vectors (IVs) be used?  
A:: Chosen appropriately and never reused for the same key.  
**Example**: Using a unique IV for each AES-CBC encryption operation.

Q:: What's better than just encryption?  
A:: Authenticated encryption, ensuring both confidentiality and integrity.  
**Example**: Using AES-GCM instead of AES-CBC for data protection.

Q:: How should cryptographic keys be handled?  
A:: Generated randomly and stored securely as byte arrays.  
**Example**: Using a hardware security module (HSM) to generate and store keys.

Q:: What's important about cryptographic randomness?  
A:: It should be unpredictable and have high entropy.  
**Example**: Using /dev/urandom on Unix systems for random number generation.

Q:: Why avoid deprecated cryptographic functions?  
A:: They have known vulnerabilities and weaknesses.  
**Example**: Using SHA-256 instead of SHA-1 for digital signatures.

Q:: Why verify cryptographic configurations independently?  
A:: To ensure they're functioning correctly and providing intended protection.  
**Example**: Using third-party security audits to verify TLS configurations.

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

Q:: What is "Injection" in OWASP Top 10 2021?  
A:: Vulnerabilities allowing attackers to insert malicious code into applications.  
**Example**: SQL injection attack manipulating a database query.

Q:: What makes an application vulnerable to injection?  
A:: Improper handling of user-supplied data in queries or commands.  
**Example**: Directly concatenating user input into an SQL query.

Q:: Why is data validation crucial?  
A:: To prevent malicious input from being executed as code.  
**Example**: Sanitizing user input to remove potential SQL commands.

Q:: What are parameterized queries?  
A:: Queries separating data from SQL commands, preventing injection.  
**Example**: Using prepared statements in Java with JDBC.

Q:: How can ORM be exploited?  
A:: By manipulating search parameters to access unauthorized data.  
**Example**: Modifying an ORM query to bypass filters and access all records.

Q:: What's the risk of concatenating user input in queries?  
A:: It can allow attackers to modify or inject malicious commands.  
**Example**: User input changing "WHERE id = " + userId to "WHERE id = 1 OR 1=1".

Q:: What are common types of injection attacks?  
A:: SQL, NoSQL, OS command, LDAP, and Expression Language injection.  
**Example**: OS command injection in a file upload feature.

Q:: How to best detect injection vulnerabilities?  
A:: Through source code review and automated security testing.  
**Example**: Using SAST tools to analyze code for potential SQL injection points.

#### Chapter 2 - How to Prevent?

Q:: What's the best way to prevent injection attacks?  
A:: Use safe APIs or ORMs that avoid interpreters entirely.  
**Example**: Using Hibernate ORM instead of writing raw SQL queries.

Q:: Can stored procedures be vulnerable to injection?  
A:: Yes, if they concatenate queries and data unsafely.  
**Example**: Using EXECUTE IMMEDIATE with user input in PL/SQL.

Q:: What's the role of input validation in preventing injection?  
A:: It helps ensure input matches expected patterns, but isn't a complete defense.  
**Example**: Validating that a username contains only alphanumeric characters.

Q:: How to handle special characters in dynamic queries?  
A:: Escape them using the specific syntax for that interpreter.  
**Example**: Using MySQLi's real_escape_string() for MySQL queries in PHP.

Q:: Why are user-supplied structure names dangerous in SQL?  
A:: They can't be safely escaped, allowing potential schema manipulation.  
**Example**: Allowing users to specify table names in a custom report builder.

Q:: How to prevent mass record disclosure in SQL injection?  
A:: Use SQL controls like LIMIT to restrict query results.  
**Example**: Adding "LIMIT 1000" to queries to cap the number of returned records.

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

Q:: What is "Insecure Design" in OWASP Top 10 2021?  
A:: Security flaws resulting from poor design choices, not just implementation.  
**Example**: A system allowing unlimited login attempts without any lockout mechanism.

Q:: How does insecure design differ from insecure implementation?  
A:: Design flaws are in the system's architecture; implementation flaws are in the code.  
**Example**: Designing a system without access controls vs. incorrectly coding access checks.

Q:: Can secure designs have vulnerabilities?  
A:: Yes, through implementation errors, but they're easier to fix than design flaws.  
**Example**: A well-designed authentication system with a bug in password hashing.

Q:: What contributes to insecure design?  
A:: Lack of risk assessment and security planning in early development stages.  
**Example**: Not considering potential data breaches when designing a user database.

Q:: What's crucial in secure design requirements?  
A:: Balancing business needs with security requirements from the start.  
**Example**: Planning for both user-friendly features and robust data encryption.

Q:: Why is threat modeling important in secure design?  
A:: It helps identify potential attacks and necessary defenses early.  
**Example**: Modeling threats to an e-commerce site to design appropriate security measures.

Q:: How can security be integrated throughout development?  
A:: By involving security experts from project inception to completion.  
**Example**: Having security reviews at each stage of an agile development process.

#### Chapter 2 - How to Prevent?

Q:: What is "Insecure Design" in OWASP Top 10 2021?  
A:: A category of security risks resulting from missing or ineffective security controls in software design.  
**Example**: A banking app allowing unlimited login attempts without lockouts.

Q:: How can AppSec professionals help prevent insecure design?  
A:: By evaluating and designing security controls as part of the secure development lifecycle.  
**Example**: Reviewing authentication mechanisms before implementation.

Q:: What is a secure design pattern library?  
A:: A collection of pre-approved, secure software components that developers can use.  
**Example**: A library containing a properly implemented password hashing function.

Q:: How does threat modeling contribute to secure design?  
A:: By identifying potential threats to critical aspects of the application early in development.  
**Example**: Analyzing possible attacks on a new payment processing feature.

Q:: Why integrate security into user stories?  
A:: To ensure security is considered from the beginning of the development process.  
**Example**: Including "verify user identity" in a story about account creation.

Q:: What are plausibility checks in application design?  
A:: Validations at each tier of the app to ensure inputs and processes are correct and secure.  
**Example**: Checking if a user's age input is within a reasonable range.

Q:: How do unit and integration tests prevent insecure design?  
A:: By validating that critical flows resist identified threats and meet security requirements.  
**Example**: Testing if the password reset function is vulnerable to enumeration attacks.

Q:: What is tier segregation in system design?  
A:: Separating application layers based on their exposure and protection needs.  
**Example**: Isolating the database server from direct internet access.

Q:: Why is tenant segregation important in multi-tenant applications?  
A:: To prevent unauthorized access or data leakage between different customers or user groups.  
**Example**: Ensuring Company A cannot access Company B's data in a cloud service.

Q:: How can limiting resource consumption improve security?  
A:: By preventing denial of service and ensuring fair usage across users or services.  
**Example**: Setting a maximum number of API calls per user per minute.

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

Q:: What is "Security Misconfiguration" in OWASP Top 10 2021?  
A:: Vulnerabilities resulting from improper configuration of application components.  
**Example**: Using default credentials on a production database server.

Q:: Why is security hardening important across the application stack?  
A:: To reduce vulnerabilities by properly configuring all components of the application.  
**Example**: Disabling unnecessary services on a web server.

Q:: How can cloud service misconfigurations lead to vulnerabilities?  
A:: Improper permission settings can allow unauthorized access to resources.  
**Example**: Accidentally making an S3 bucket publicly readable.

Q:: Why should unnecessary features be disabled?  
A:: To reduce the attack surface and minimize potential vulnerabilities.  
**Example**: Disabling unused modules in a content management system.

Q:: What's the risk of keeping default accounts and passwords?  
A:: They provide an easy entry point for attackers to gain unauthorized access.  
**Example**: Not changing the default 'admin' password on a router.

Q:: How can overly informative error messages be a security risk?  
A:: They may reveal sensitive information that aids attackers in exploiting vulnerabilities.  
**Example**: A database error exposing table names and query structure.

Q:: Why is it crucial to enable the latest security features?  
A:: To protect against newly discovered threats and vulnerabilities.  
**Example**: Enabling HTTP Strict Transport Security (HSTS) on a web server.

Q:: What components need secure configuration in an application?  
A:: All components including servers, frameworks, libraries, and databases.  
**Example**: Configuring proper access controls in a MySQL database.

Q:: Why are security headers important in web applications?  
A:: They provide browser-level protection against various attacks.  
**Example**: Using Content Security Policy to prevent XSS attacks.

Q:: How does keeping software up-to-date improve security?  
A:: It patches known vulnerabilities and adds new security features.  
**Example**: Updating a WordPress installation to fix a known SQL injection flaw.

Q:: What is a repeatable security configuration process?  
A:: A standardized approach to consistently apply secure settings across all systems.  
**Example**: Using automated scripts to apply security patches across all servers.

#### Chapter 2 - How to Prevent?

Q:: What is a repeatable hardening process?  
A:: A standardized method to quickly deploy secure environments across development, QA, and production.  
**Example**: Using automated scripts to apply security settings on all new servers.

Q:: Why is a minimal platform important for security?  
A:: It reduces the attack surface by eliminating unnecessary features and components.  
**Example**: Disabling unused services like FTP on a web server.

Q:: How does patch management relate to security configuration?  
A:: It ensures that security updates and patches are regularly applied to maintain a secure environment.  
**Example**: Promptly applying a security patch to fix a known vulnerability in a web framework.

Q:: What is a segmented application architecture?  
A:: A design that separates components or tenants to limit the impact of potential breaches.  
**Example**: Using separate databases for different customer groups in a SaaS application.

Q:: Why are security headers important in web applications?  
A:: They instruct the client's browser to enable specific security controls.  
**Example**: Using the X-Frame-Options header to prevent clickjacking attacks.

Q:: How can configuration effectiveness be verified across environments?  
A:: Through automated processes that check and validate security settings in all environments.  
**Example**: Running automated security scans nightly to detect misconfigurations.

Q:: What's the benefit of consistent configurations across environments?  
A:: It reduces the risk of security issues when moving from development to production.  
**Example**: Using the same firewall rules in development and production environments.

Q:: How can containerization improve security?  
A:: By isolating applications and their dependencies, reducing the impact of potential breaches.  
**Example**: Running different microservices in separate Docker containers.

Q:: Why is it important to review configurations regularly?  
A:: To ensure they remain secure as the application and its environment evolve.  
**Example**: Checking that database access permissions are still appropriate after a system upgrade.

Q:: What role do cloud security groups play in preventing misconfigurations?  
A:: They provide a way to control network access to cloud resources, enhancing security.  
**Example**: Using AWS security groups to limit database access to specific application servers.

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

Q:: What are "Vulnerable and Outdated Components" in OWASP Top 10 2021?  
A:: Software elements with known security flaws or lacking necessary updates.  
**Example**: Using an old version of jQuery with a known XSS vulnerability.

Q:: Why is it important to track component versions in your software?  
A:: To identify and address potential vulnerabilities quickly.  
**Example**: Maintaining a list of all npm packages and their versions used in a project.

Q:: What risks come with using unsupported or outdated components?  
A:: Increased vulnerability to known exploits and security breaches.  
**Example**: Running a website on an unsupported version of PHP.

Q:: How can you stay informed about component vulnerabilities?  
A:: By regularly scanning for vulnerabilities and subscribing to security bulletins.  
**Example**: Using tools like OWASP Dependency-Check in your CI/CD pipeline.

Q:: Why is timely updating of platforms and dependencies crucial?  
A:: To protect against known vulnerabilities and reduce security risks.  
**Example**: Promptly applying security patches to your web server software.

Q:: How can developers ensure component security when updating?  
A:: By testing the compatibility and security of updated libraries.  
**Example**: Running a full test suite after updating a critical framework.

Q:: Why is proper configuration important for component security?  
A:: To prevent misconfigurations that could introduce vulnerabilities.  
**Example**: Ensuring proper access controls are set on a database component.

#### Chapter 2 - How to Prevent?

Q:: What should be removed during patch management?  
A:: Unused dependencies, features, components, files, and documentation.  
**Example**: Removing unused modules from a content management system.

Q:: How can component versions be continuously inventoried?  
A:: By using automated tools to track both client-side and server-side components.  
**Example**: Implementing a software composition analysis tool in your development process.

Q:: Why obtain components from official sources over secure links?  
A:: To reduce the risk of including modified or malicious components.  
**Example**: Downloading Node.js packages from the official npm registry over HTTPS.

Q:: How to handle unmaintained components lacking security patches?  
A:: By monitoring them closely and considering virtual patching when updates aren't possible.  
**Example**: Using a Web Application Firewall to mitigate a vulnerability in a legacy library.

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

Q:: What are "Identification and Authentication Failures" in OWASP Top 10 2021?  
A:: Weaknesses in systems that verify user identity and manage user sessions.  
**Example**: A website that doesn't lock accounts after multiple failed login attempts.

Q:: Why is proper user authentication critical?  
A:: To prevent unauthorized access and protect against identity-related attacks.  
**Example**: Ensuring only authorized users can access sensitive financial data.

Q:: What is credential stuffing?  
A:: An attack using stolen username/password pairs to gain unauthorized access.  
**Example**: Using leaked email/password combinations to try logging into various websites.

Q:: Why are weak passwords a security risk?  
A:: They are easily guessable, making unauthorized access more likely.  
**Example**: Using "password123" as an account password.

Q:: What's wrong with knowledge-based answers for password recovery?  
A:: They can often be guessed or obtained through social engineering.  
**Example**: Using "mother's maiden name" as a security question, which might be publicly available.

Q:: Why is storing passwords in plain text dangerous?  
A:: It allows anyone with database access to see users' passwords.  
**Example**: Storing user passwords as clear text in a database file.

Q:: What is multi-factor authentication (MFA)?  
A:: A security system requiring two or more forms of identification to grant access.  
**Example**: Requiring both a password and a fingerprint scan to log in.

Q:: Why shouldn't session IDs be exposed in URLs?  
A:: It can lead to session hijacking and unauthorized access.  
**Example**: Having a URL like "example.com/account?sessionid=1234", which can be easily copied.

Q:: Why is session ID reuse after login risky?  
A:: It can allow unauthorized users to take over authenticated sessions.  
**Example**: Not generating a new session ID after a user logs in, potentially allowing old IDs to remain valid.

Q:: Why is proper session invalidation important?  
A:: To prevent unauthorized access after a user logs out or is inactive.  
**Example**: Ensuring a user can't access their account from an old browser tab after logging out on another device.

Q:: What is a brute force attack?  
A:: Systematically trying many passwords to gain unauthorized access.  
**Example**: A program that tries every possible 4-digit PIN on a locked phone.

#### Chapter 2 - How to Prevent?

Q:: How does multi-factor authentication (MFA) enhance security?  
A:: By requiring multiple forms of verification, making unauthorized access more difficult.  
**Example**: Using a password and a fingerprint scan to log into a banking app.

Q:: Why should default credentials be avoided in deployments?  
A:: To prevent easy unauthorized access to newly deployed systems.  
**Example**: Changing the default 'admin/admin' credentials on a new router before use.

Q:: How can weak password checks improve security?  
A:: By preventing users from choosing easily guessable passwords.  
**Example**: Rejecting '123456' as a password during account creation.

Q:: What are modern password policy recommendations?  
A:: Focusing on length over complexity and avoiding frequent mandatory changes.  
**Example**: Encouraging passphrases like "correct-horse-battery-staple" instead of "P@ssw0rd!".

Q:: How can account enumeration attacks be prevented?  
A:: By providing consistent responses regardless of whether an account exists.  
**Example**: Showing "If an account exists, a reset email has been sent" for all reset attempts.

Q:: Why limit or delay failed login attempts?  
A:: To prevent brute force attacks without causing denial of service.  
**Example**: Implementing a 30-second delay after 5 failed login attempts.

Q:: What makes a session manager secure?  
A:: Generating random, high-entropy session IDs and properly managing their lifecycle.  
**Example**: Creating a new session ID after login and invalidating it after 30 minutes of inactivity.

Q:: Why shouldn't session IDs be included in URLs?  
A:: To prevent session hijacking through URL sharing or logging.  
**Example**: Using cookies instead of URLs to store session information.

Q:: How can password strength be effectively measured?  
A:: By comparing against lists of common passwords and using entropy calculations.  
**Example**: Using a password strength meter that checks against a database of breached passwords.

Q:: What's the importance of secure credential recovery?  
A:: To prevent unauthorized access through weak password reset mechanisms.  
**Example**: Sending a time-limited reset link to a pre-registered email address instead of asking security questions.

Q:: How can API security be enhanced for authentication?  
A:: By implementing rate limiting and consistent error responses.  
**Example**: Limiting login API calls to 10 per minute per IP address.

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

Q:: What are "Software and Data Integrity Failures" in OWASP Top 10 2021?  
A:: Issues related to code and data that can be tampered with due to insufficient verification.  
**Example**: An application accepting software updates without verifying their source.

Q:: How can untrusted libraries compromise software integrity?  
A:: By introducing vulnerabilities or malicious code into the application.  
**Example**: Using a compromised npm package that steals user data.

Q:: What risks do insecure CI/CD pipelines pose?  
A:: They can allow unauthorized code changes or malicious injections during deployment.  
**Example**: An attacker accessing an unsecured Jenkins server to inject malware into builds.

Q:: Why is auto-update functionality a potential security risk?  
A:: It may apply unverified updates, potentially distributing malware.  
**Example**: A fake update server tricking applications into installing malicious code.

Q:: What is insecure deserialization?  
A:: Converting serialized data to objects without proper security checks.  
**Example**: A Java application deserializing user-supplied data without validation, allowing code execution.

#### Chapter 2 - How to Prevent?

Q:: How can digital signatures prevent integrity failures?  
A:: By verifying the authenticity and integrity of software or data.  
**Example**: Verifying a downloaded software package's GPG signature before installation.

Q:: Why use trusted repositories for dependencies?  
A:: To reduce the risk of including compromised components in your software.  
**Example**: Using official Maven repositories instead of third-party mirrors for Java dependencies.

Q:: How do software supply chain security tools help?  
A:: They check components for known vulnerabilities, enhancing software integrity.  
**Example**: Using OWASP Dependency-Check to scan libraries for CVEs before deployment.

Q:: Why is code review important for preventing integrity failures?  
A:: It helps catch malicious code or configuration changes before they're deployed.  
**Example**: A team member spotting a suspicious API call during a pull request review.

Q:: How does proper CI/CD pipeline security prevent integrity failures?  
A:: By ensuring only authorized changes are made during the build and deploy process.  
**Example**: Using separate build and production environments with strict access controls.

Q:: How can serialized data transmission be made more secure?  
A:: By adding integrity checks or digital signatures to detect tampering.  
**Example**: Using HMAC to sign JSON Web Tokens before sending them to clients.

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

Q:: What are "Security Logging and Monitoring Failures" in OWASP Top 10 2021?  
A:: Inadequacies in tracking and responding to security events and incidents.  
**Example**: A system that doesn't log failed login attempts, making it hard to detect brute force attacks.

Q:: Why is security logging and monitoring crucial?  
A:: To detect, escalate, and respond to active breaches quickly.  
**Example**: Using log analysis to identify a data exfiltration attempt in real-time.

Q:: What events should always be logged?  
A:: High-value transactions and security-relevant events like user authentication.  
**Example**: Logging each time an admin accesses sensitive customer data.

Q:: Why are clear and adequate log messages important?  
A:: To quickly understand and respond to potential security issues.  
**Example**: A log message stating "User 'john_doe' failed login 5 times in 2 minutes" instead of just "Login error".

Q:: Why monitor application and API logs?  
A:: To detect suspicious activities that might indicate a security threat.  
**Example**: Noticing an unusual spike in API calls from a single IP address.

Q:: What's the risk of storing logs only locally?  
A:: Loss of critical data if the local system is compromised or fails.  
**Example**: An attacker deleting local logs to cover their tracks after a successful intrusion.

Q:: Why are alerting thresholds important in security monitoring?  
A:: To promptly notify security teams when suspicious activity occurs.  
**Example**: Sending an alert when more than 10 failed login attempts occur within a minute.

Q:: How can penetration testing improve monitoring?  
A:: By ensuring monitoring systems can detect and alert on simulated attacks.  
**Example**: Verifying that a web application firewall alerts on SQL injection attempts during a pentest.

Q:: Why is real-time attack detection crucial?  
A:: To minimize damage by enabling immediate response to security incidents.  
**Example**: Automatically blocking an IP address when it starts a DDoS attack.

Q:: What's the importance of log retention policies?  
A:: To ensure logs are available for future forensic analysis if needed.  
**Example**: Keeping authentication logs for 90 days to investigate potential past breaches.

Q:: How can log integrity be ensured?  
A:: By using tamper-evident logging mechanisms and secure storage.  
**Example**: Using blockchain technology to create an immutable audit log of system changes.

#### Chapter 2 - How to Prevent?

Q:: What should be logged for security-related events?  
A:: All login attempts, access control, and server-side input validation failures with sufficient context.  
**Example**: Logging failed login attempts with username, IP address, and timestamp.

Q:: Why use standardized log formats?  
A:: To ensure easy consumption by log management solutions for efficient analysis.  
**Example**: Using the Common Log Format for web server logs to facilitate processing by various tools.

Q:: How can log injection attacks be prevented?  
A:: By properly encoding log data to prevent manipulation of log content or systems.  
**Example**: Escaping special characters in user input before including it in log messages.

Q:: What are integrity controls for high-value transactions?  
A:: Mechanisms to prevent tampering or deletion of audit trails for critical operations.  
**Example**: Using an append-only database table to store financial transaction logs.

Q:: How can DevSecOps teams enhance security monitoring?  
A:: By implementing effective monitoring and alerting systems for quick incident detection and response.  
**Example**: Setting up a SIEM system to correlate logs from various sources and generate alerts.

Q:: Why is an incident response plan important?  
A:: To ensure a coordinated and effective approach to handling security incidents.  
**Example**: Having a documented process for responding to a detected data breach, including roles and communication protocols.

Q:: What's the importance of log retention?  
A:: To ensure sufficient data is available for forensic analysis after an incident.  
**Example**: Keeping authentication logs for 90 days to trace the origin of a recently discovered breach.

Q:: How can log analysis be automated?  
A:: By using tools that can process logs in real-time and flag suspicious patterns.  
**Example**: Using machine learning algorithms to detect anomalies in user behavior from log data.

Q:: Why is context important in security logging?  
A:: To provide enough information for accurate analysis and incident response.  
**Example**: Including user ID, resource accessed, and action performed in every access log entry.

Q:: How can log confidentiality be maintained?  
A:: By encrypting sensitive log data and controlling access to log storage systems.  
**Example**: Encrypting logs containing personal data before transmitting them to a central log server.

Q:: What role do log reviews play in security?  
A:: Regular log reviews can help identify security issues and improve monitoring processes.  
**Example**: Weekly reviews of failed login attempts to identify potential brute force attack patterns.

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

Q:: What is Server-Side Request Forgery (SSRF)?  
A:: An attack where an application is tricked into making unintended server-side requests.  
**Example**: An attacker manipulating a URL parameter to make an internal API call to delete user data.

Q:: Why is SSRF considered a significant security risk?  
A:: It can bypass security controls and access sensitive internal resources.  
**Example**: An SSRF attack accessing AWS metadata to steal cloud credentials.

Q:: How does cloud computing increase SSRF risks?  
A:: Cloud architectures often have complex internal networks vulnerable to SSRF.  
**Example**: An SSRF vulnerability allowing access to other customers' data in a multi-tenant cloud environment.

Q:: Why are modern web apps prone to SSRF?  
A:: They often include features for fetching external URLs, which can be exploited.  
**Example**: A website preview feature that can be manipulated to access internal network resources.

Q:: How can SSRF bypass network security measures?  
A:: By originating requests from within the trusted network perimeter.  
**Example**: An SSRF attack accessing an internal database server that's not exposed to the internet.

Q:: What makes SSRF detection challenging?  
A:: The malicious requests often appear to come from legitimate internal sources.  
**Example**: An SSRF attack mimicking normal API calls between microservices.

Q:: How can SSRF lead to data breaches?  
A:: By allowing attackers to access and exfiltrate sensitive internal data.  
**Example**: Using SSRF to retrieve and leak customer information from an internal database.

Q:: What role does input validation play in preventing SSRF?  
A:: Proper validation can prevent malicious URLs from being processed.  
**Example**: Whitelisting allowed domains for a URL fetching feature to prevent SSRF.

Q:: How can SSRF impact containerized environments?  
A:: It may allow access to the host system or other containers.  
**Example**: An SSRF vulnerability in a container allowing access to the Docker socket on the host.

Q:: Why is SSRF particularly dangerous in microservices architectures?  
A:: It can allow attackers to move laterally between different services.  
**Example**: Using SSRF in one microservice to attack another internal service not exposed externally.

#### Chapter 2 - How to Prevent?

Q:: How can network segmentation reduce SSRF risks?  
A:: By isolating remote resource access functionality in separate networks.  
**Example**: Placing web servers in a DMZ, separate from internal application servers.

Q:: Why use "deny by default" firewall policies?  
A:: To block all but essential intranet traffic, reducing potential SSRF targets.  
**Example**: Only allowing specific ports and protocols needed for application functionality.

Q:: Why establish ownership for firewall rules?  
A:: To ensure proper management and regular review of access controls.  
**Example**: Assigning each firewall rule to a specific team or application owner.

Q:: How does logging network flows help prevent SSRF?  
A:: By providing visibility into potential SSRF attempts and anomalies.  
**Example**: Logging all blocked requests to internal resources from web servers.

Q:: Why sanitize and validate all client-supplied input?  
A:: To prevent malicious data from being used in server-side requests.  
**Example**: Validating and encoding URL parameters before using them in API calls.

Q:: How does a positive allow list help prevent SSRF?  
A:: By restricting outbound requests to only trusted and known destinations.  
**Example**: Only allowing API calls to whitelisted internal service endpoints.

Q:: Why avoid sending raw responses to clients?  
A:: To prevent exposure of sensitive information obtained through SSRF.  
**Example**: Sanitizing error messages before sending them to the client.

Q:: Why disable HTTP redirections for SSRF prevention?  
A:: To prevent the application from being tricked into accessing malicious sites.  
**Example**: Disabling automatic following of 3xx redirect responses in HTTP clients.

Q:: How can URL consistency awareness prevent attacks?  
A:: By mitigating risks like DNS rebinding and TOCTOU race conditions.  
**Example**: Verifying that the resolved IP address matches the expected domain.

Q:: Why are deny lists ineffective against SSRF?  
A:: Attackers have techniques to bypass these measures.  
**Example**: Using URL encoding to bypass a blacklist of prohibited characters.

Q:: Why minimize services on front-end systems?  
A:: To reduce the attack surface exposed to potential SSRF attempts.  
**Example**: Keeping only the web server on the front-end, moving application logic to separate servers.

Q:: How to secure local traffic on front-end systems?  
A:: By restricting requests to security-relevant services to the local system.  
**Example**: Configuring internal APIs to only accept requests from 'localhost'.

Q:: When should you consider using VPNs for frontend access?  
A:: For scenarios with high protection needs and manageable user groups.  
**Example**: Using a VPN for admin access to a high-security financial application.

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