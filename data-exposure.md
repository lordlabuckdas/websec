---
title: DataExpo
tags: owasptop10
---

## description

many web applications and APIs do not properly protect sensitive data, such as financial, healthcare, and PII.

attackers may steal or modify such weakly protected data to conduct credit card fraud, identity theft, or other crimes. Sensitive data may be compromised without extra protection, such as encryption at rest or in transit, and requires special precautions when exchanged with the browser.

## link

[https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure](https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure)

## overview

### attack vector

* steal keys
* mitm attack
* sensitive info from:
  * server
  * transit
  * client's browser
* passwords stolen can be brute-forced

### security weakness

* unencrypted sensitive info
* weak crypto:
  * key generation
  * key mgmt
  * algo
  * protocol usage
  * cipher usage

### impact

* pii and other sensitive leaked

## vuln

* plain-text data transfer protocols:
  * http
  * smtp
  * ftp
* external and internal net traffic

## prevention

## attack example
