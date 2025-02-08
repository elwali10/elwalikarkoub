---
date: '2025-02-08T17:51:03Z'
draft: false
title: 'Turning my Linux Mint Laptop into A server: Systemd targets & logind'
tags:
  - Linux
  - Home Lab
  - Systemd
---

 
I have been tinkering lately to build a home lab (K8s, Wazuh ...) and wanted to turn my old laptop (Running Linux Mint 21) into a server. While going through that process I had issues with configuring RDP (The session immediately closed after connecting) also I needed to be able to close the laptop's lid while keeping it running.


For the first issue, I was able to solve it by running the following and then reboot:
 

```
sudo systemctl set-default multi-user.target

sudo reboot

```

That is where I came across the notion of systemd targets that was introduced to replace traditional runlevels in SysVinit systems.

 - multi-user.target → Boots into a multi-user text-based environment without a graphical interface.

 - graphical.target (Default mode) → Boots into a multi-user environment with a graphical interface (GUI enabled).


If for any reason, I need to switch back to GUI mode, running `sudo systemctl set-default graphical.target` then reboot should do it. 


And to keep the laptop "server" running with the lid closed, I performed the following: 


 - Edit the logind configuration file `/etc/systemd/logind.conf` to set the below option to `ignore`: 

```
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

 - Save then apply the changes by running `sudo systemctl restart systemd-logind` 






