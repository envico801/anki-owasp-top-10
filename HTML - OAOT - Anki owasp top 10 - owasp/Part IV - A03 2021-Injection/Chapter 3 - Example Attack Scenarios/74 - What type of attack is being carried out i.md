========== Question ==========  

### What type of attack is being carried out in this situation?

An application uses untrusted data in the construction of the following vulnerable SQL call:

<!-- codeblock-start -->
<pre><code class="hljs language-java"><span class="hljs-type">String</span> <span class="hljs-variable">query</span> <span class="hljs-operator">=</span> <span class="hljs-string">"SELECT * FROM accounts WHERE custID='"</span> + request.getParameter(<span class="hljs-string">"id"</span>) + <span class="hljs-string">"'"</span>;
</code></pre>
<!-- codeblock-end -->  

========== Answer ==========  

A03 Injection

========== Id ==========  
74

---

DECK INFO

TARGET DECK: Web Security::OWASP Top 10::OAOT - Anki owasp top 10 - owasp::Part IV - A03 2021-Injection::Chapter 3 - Example Attack Scenarios

FILE TAGS: #OWASP::#OWASP-Top-10::#Web-Security::#OAOT-Anki-owasp-top-10-owasp::#Part-IV-A03-2021-Injection::#Chapter-3-Example-Attack-Scenarios::#74-What-type-of-attack-is-being-carried-out-i

Reference:

Related:

```dataview
LIST
where file.name = this.file.name
```
QUESTION STATUS: Safe to store
