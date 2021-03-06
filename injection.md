---
title: Injection
tags: owasptop10
---

## description

injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query.

the attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.

## link

[https://owasp.org/www-project-top-ten/2017/A1_2017-Injection](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection)

## overview

### attack vector

* [injection flaws](https://owasp.org/www-community/Injection_Flaws) occurs when attacker can send (hostile) data to some interpreter
* improperly filtered data -> system call -> malicious code execution
* whole scripts in perl, python, js can be injected
* os and external prog vulns (ref [[comp-vuln]]) should be taken into account
* info thru http req should be properly filtered

### security weakness

* legacy code
* exploited thru
  * SQL
  * LDAP
  * XPath
  * NoSQL queries
  * OS commands
  * XML parsers
  * SMTP headers
  * expression languages
  * ORM queries
* use fuzzers and scanners to test for weaknesses

### impact

* db access
* results in
  * data loss
  * corruption
  * disclosure to unauthorized parties
  * loss of accountability
  * denial of access
  * sometimes lead to complete host takeover

## vuln

* bad input validation or sanitization
* stupid concatenation of user input
* dynamic queries or non-parameterized calls w/o context-aware escaping used directly in the interpreter
* hostile data used within object-relational mapping (ORM) search parameters to extract additional, sensitive records
* hostile data added to the query
* common injections:
  * SQL
  * NoSQL
  * OS command
  * Object Relational Mapping (ORM)
  * LDAP
  * Expression Language (EL)
  * Object Graph Navigation Library (OGNL)
* detection by:
  * source code review
  * thorough automated testing of all:
    * parameters
    * headers
    * URL
    * cookies
    * JSON
    * SOAP
    * XML data inputs
* SAST and DAST in CI/CD pipeline is recommended

## prevention

* use a safe API (that takes care of encoding and escaping)
* use `LIMIT` to limit the amount of data fetched in [[data-exposure]]
* properly escape chars

## attack example

```php
query = "SELECT * FROM accounts WHERE custID='" + request.getParameter("id") + "'";
```

here, the attacker can send data like

```http
http://victim.com?id='OR'1'='1
```

and the final SQL query will be

```sql
SELECT * FROM accounts WHERE custID='' OR '1'='1'
```
