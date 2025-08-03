---
date: '2025-08-03T22:19:35+01:00'
draft: false
title: 'KnockKnock : Reveal Persistent MacOS installed softwares'
tags:
  - Incident Response
  - Security
  - Open Source
categories:
  - security
---


During a post-incident malware investigation, having fast and reliable tools is critical for uncovering persistent threats. I have recently came accross **KnockKnock** tool which is a free, open-source macOS tool by Objective-See that uncovers persistently installed software-components.



## Why It Matters

Once malware infects a system, it typically establishes persistence through:

- Launch Agents/Daemons
- Browser Extensions
- Cron Jobs
- Login Items
- Kernel Extensions

KnockKnock automates detection of these persistence mechanisms, providing visibility into what's set to automatically execute on your Mac.


{{< figure src="/images/knockknock.png"  >}}

## Key Features

 **Comprehensive Persistence Scanner**  
 Checks 60+ persistence locations (more than macOS's built-in tools)

 **VirusTotal Integration**  
 Automatically checks items against VirusTotal's malware database

 **Open Source & Transparent**  
 Fully inspectable code on [GitHub](https://github.com/objective-see/KnockKnock)

 **No Installation Needed**  
   Runs as a standalone application


**Download**: [https://objective-see.org/products/knockknock.html](https://objective-see.org/products/knockknock.html)  
**Source Code**: [GitHub Repository](https://github.com/objective-see/KnockKnock)

