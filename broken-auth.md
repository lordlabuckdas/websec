---
title: BrokenAuth
tags: owasptop10
---

## description

application functions related to authentication and session management are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users’ identities temporarily or permanently.

## link

[https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication)

## overview

### attack vector

* weak user and admin creds
* brute-force
* poor [[sess-mgmt]] practices
  * like unexpired session tokens

### security weakness

* prevalence is widespread due to design and implementation of [[access-control]]
* [[sess-mgmt]] forms the bedrock and is v imp

### impact

* either multiple user accounts or 1 admin account will compromise the whole sys
* id theft, sensitive info leak

## vuln

* brute-force possible
* weak passwords allowed
* no MFA
* bad password db practices (ref [[data-exposure]]) like not hashing the passwd
* session ID in url
* poor [[sess-mgmt]] practices:
  * no rotation of sess id
  * improper invalidation of sessions

## prevention

* **checks against above [vulns](#vuln)**
* MFA
* limits multiple attempts, brute-force prevention
  * proper [[log-monitor]] for failed attempts
  * increased duration for each failed attempt
* passwd strength checks
* sess ID generated w/ high entropy
  * definitely shouldn't be present in the url
* api gateways secure af

## attack example

* session id is not invalidated properly
* brute-force vulnerable
* weak password
