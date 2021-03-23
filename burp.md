---
title: Burp
tags: tool
---

## overview

* i had installed DVWA using metasploitable during 30 Days Challenge itself when i was practicing web security
* however, i also went through the other methods like the docker setup and apache setup
* i downloaded the certificate from [http://burpsuite](http://burpsuite) and added it to my firefox browser
* then i learnt about scopes to restrict the proxy to only my target - DVWA at 10.0.2.6
* installed **foxyproxy** for ease of switching proxies

i'll explain the different tabs using the screenshots for reference

## DVWA

![dvwa homepage](/assets/dvwa_homepage.png)

![dvwa xss](/assets/dvwa_xss.png)

## burp tabs

### target

![burp target](/assets/burp/burp_target.png)

here, the request verb (GET) and body, response status code (200) and body are highlighted

the target tab is used to

* have a look at the outgoing request
* decide whether to forward it or not
* forward it to other components (tabs)
* edit the request before sending

it can also be used to see a tree view of the website structure

### repeater

![burp repeater](/assets/burp/burp_repeater.png)

* repeater is a simple feature that can be used to repeat another request with different parameters
* it offers a good UI to add query parameters, request body among others
* it also shows the response to the corresponding request and can also follow redirects

### intruder

![burp intruder - positions](/assets/burp/burp_intruder1.png)

* this tab allows us to set variables that can be subsituted with a list of payloads
* we can either set the variable limits manually or even set it automatically
* in this case, i've set up the password as the variable for a bruteforce attack to find the admin password

![burp intruder - payloads](/assets/burp/burp_intruder2.png)

* here, i'm using a simple list with substitution for the password
* for brute-forcing the password, we can use a common password list for intruder to iterate through

![burp intruder - results](/assets/burp/burp_intruder3.png)

* as we can see, all the requests except `password` have received a smaller and same response
* this can mean that `password` is the right `password`

### comparer

![burp comparer - list](/assets/burp/burp_comparer1.png)

from our previous usage of **intruder**, i've loaded 2 different responses - one for wrong password and one for the right password

![burp comparer - diff](/assets/burp/burp_comparer2.png)

* as we can see, similar to `git diff` or `git difftool`, burpsuite shows us the difference in the repsonse value
* we can notice that different stylesheets and scripts are loaded for different responses and sites

### decoder

![burp decoder](/assets/burp/burp_decoder.png)

* decoder can be used to decode or encode text repetitively
* a use-case demonstrated here would be to encode the characters properly for a SQLi attack
* it can be also used to encode text for xss such that the encoding and filters are bypassed

### sequencer

![burp sequencer](/assets/burp/burp_sequencer.png)

* sequencer can be used to test the randomness of any token
* here, i've used it to check the randomness of PHPSESSID cookie
* to start with, we have to load a response with the `Set-Cookie` header (can be forwarded from **target**)
* then, we have to select which cookie's randomness to check for
* now we can start collecting the token in mass number
* we can analyze the tokens for proper results after getting a good number of tokens
* the sequencer will tell us if the cookie is actually generated randomly or if there is a pattern which can be broken
