---
title: Verbs
---

## GET

* used to get data
* query strings to fine-tune data
* should not perform state-changing operations
  * if so, potential [[csrf]]

```http
GET /echo/get/json HTTP/1.1
Host: reqbin.com
Accept: */*
```

## POST

* used to send data
* req params present in req body

```http
POST /echo/post/json HTTP/1.1
Host: reqbin.com
Accept: */*
Content-Type: text/plain
Content-Length: 16

abc=123&name=bob
```

**Note:** All the [[cookies]] (of the respective website) are sent along with every request
