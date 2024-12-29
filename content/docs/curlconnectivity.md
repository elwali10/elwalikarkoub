---
date: '2024-12-28T17:12:18Z'
draft: false
title: 'Check connectivity using only CURL'
tags: 
- Command-Line
- Network
- Linux
---

I have had situations where I needed to check the connectivity using telnet but the server did not have it installed nor the possiblity to do so. I've found that it can be achieved using only curl:

`curl -vv telnet://serverIP:port` 

This will use the telnet portocol instead of the known http(s).

curl support about 28 protocols that you can find here: https://everything.curl.dev/protocols/curl.html


