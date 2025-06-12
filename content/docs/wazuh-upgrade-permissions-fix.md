---
date: '2025-06-12T23:56:46+01:00'
draft: false
title: 'Wazuh Upgrade Permissions Fix'
categories:
  - Security
tags:
  - Linux
  - Wazuh
  - SIEM
---
# Updating Wazuh Manager Permissions After Failed Upgrade

If your Wazuh manager upgrade fails due to permission issues, you may need to check the files permissions/ownership if they are still using the old ossec user/group.

## Permission Update Commands

Run these commands to correct ownership:

```bash
# Change ossec user/group to wazuh
find /var/ossec -group ossec -user ossec -exec chown wazuh:wazuh {} \;

# Change root-owned files to wazuh group
find /var/ossec -group ossec -user root -exec chown root:wazuh {} \;
```
## Notes:

- These commands recursively update ownership in the Wazuh directory

- First command changes files owned by ossec:ossec to wazuh:wazuh

- Second command maintains root ownership but updates group to wazuh

- Run as root or with sudo privileges
