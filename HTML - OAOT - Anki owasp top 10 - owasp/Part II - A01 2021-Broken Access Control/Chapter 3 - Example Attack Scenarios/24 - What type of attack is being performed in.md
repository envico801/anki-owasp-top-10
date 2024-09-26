========== Question ==========  

### What type of attack is being performed in this situation?

The application uses unverified data in a SQL call that is accessing account information:

<!-- codeblock-start -->
<pre><code class="hljs language-java"> pstmt.setString(<span class="hljs-number">1</span>, request.getParameter(<span class="hljs-string">"acct"</span>));
 <span class="hljs-type">ResultSet</span> <span class="hljs-variable">results</span> <span class="hljs-operator">=</span> pstmt.executeQuery( );
</code></pre>
<!-- codeblock-end -->

An attacker simply modifies the browser's 'acct' parameter to send whatever account number they want. If not correctly verified, the attacker can access any user's account.

<!-- codeblock-start -->
<pre><code class="hljs language-plaintext"> https://example.com/app/accountInfo?acct=notmyacct
</code></pre>
<!-- codeblock-end -->  

========== Answer ==========  

A01 Broken Access Control

========== Id ==========  
24

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part II - A01 2021-Broken Access Control::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-II-A01-2021-Broken-Access-Control::#Chapter-3-Example-Attack-Scenarios::#24-What-type-of-attack-is-being-performed-in

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
