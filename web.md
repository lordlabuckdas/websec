---
title: Web
---

* Authorization header -> “Basic <username:passwd in base64>”
* Referer is not passed when using HTTPS on origin
* check Accept header for accepted MIME types and potential vulns
* cookie of example.com is available for example.com and \*.example
* subdomain can set cookie for parent domain and itself, but not sibling domain
* secure -> only https; httponly -> no js access (present in Set-Cookie)
* when WAF and browser parser don't match, potential vuln
* sometimes MIME and encoding are sniffed
* same origin policy:
  * same port
  * same protocol (http(s))
  * same exact domain
* misconfigured cors and iframe -> vulns
* csrf -> because referer is unreliable -> mitigate through dynamic form embedded csrf tokens
