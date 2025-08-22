---
title: "Azure Signing Logs Missing from Wazuh Dashboard"
date: "2025-08-22T10:00:00+02:00"
draft: false
tags: ["Wazuh", "Azure", "SIEM"]
categories: ["Security", "Troubleshooting"]
author: "ElWali Karkoub"
---

## Issue Description

Azure sign-in logs (`auditLogs`/`signIns`) are processed by Wazuh manager and visible in alerts, but they don't appear in the Wazuh Dashboard. This happens due to a field mapping conflict.

### The Error

```json
{
  "type": "mapper_parsing_exception",
  "reason": "failed to parse field [data.ms-graph.status] of type [keyword]"
}
```

## Root Cause

The `status` field in Azure logs contains a JSON object, but the Wazuh template expects it to be a keyword string.

## Solution

### Temporary Fix

1. **Edit the Wazuh template:**

```bash
sudo nano /etc/filebeat/wazuh-template.json
```

2. **Find the ms-graph section and update the status field:**

```json
"ms-graph": {
  "properties": {
    "relationship": {
      "type": "keyword"
    },
    "status": {
      "type": "object",
      "dynamic": true
    }
  }
}
```

3. **Apply the template:**

```bash 
filebeat setup --index-management -E setup.template.json.enabled=false
```

4. **Restart Filebeat:**

```bash
sudo systemctl restart filebeat
```



### Permanent Fix

A permanent fix will be available in Wazuh 4.14 based on this PR: https://github.com/wazuh/wazuh/pull/30831 



### Additional Notes

- This fix resolves the mapping conflict that prevents Azure logs from displaying in the dashboard

- The temporary modification changes the status field from keyword to object type with dynamic mapping 
