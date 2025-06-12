---
date: '2025-06-12T23:09:38+01:00'
draft: false
title: 'Running PowerShell Commands on a Wodle Wazuh'
categories:
  - Security
tags:
  - Security
  - Wazuh
  - Powershell
  - Security Monitoring
---
# Running PowerShell Commands on a Wodle in Wazuh

By executing PowerShell commands through a Wazuh Wodle and formatting the results in JSON, you can streamline log processing without the need for custom decoders. This method simplifies integration—only the corresponding rules need to be defined to handle the structured output effectively.

## PowerShell Command Format

The recommended format for PowerShell commands in a Wodle is:

```powershell
Powershell -c "@{ <header> = <command> } | ConvertTo-Json -compress"
```
 - `<command>` is the PowerShell cmdlet or one-liner script that outputs an object

 - `<header>` is any name you want to add to help when writing rules

# Wodle Configuration Example

Here's how to configure the command Wodle to execute PowerShell commands:

```xml
<wodle name="command">
  <disabled>no</disabled>
  <command>Powershell -c "@{ <header> = <command> } | ConvertTo-Json -compress"</command>
  <ignore_output>no</ignore_output>
</wodle>

```

# Rule Example

To create rules for the PowerShell command output, use the following structure:

```xml
<group name="psCommand,">
  <rule id="301000" level="3">
    <decoded_as>json</decoded_as>
    <match>^{"<header>":</match>
    <description>Windows Powershell command base rule</description>
  </rule> 
</group>

```

## Benefits

 - Structured Output: JSON format provides consistent, parseable output

 - Simplified Rule Creation: No need for complex decoders

 - Flexibility: Can adapt to various PowerShell commands

 - Readability: Clear structure makes maintenance easier

## Implementation Tips

 - Always test your PowerShell commands locally before adding them to a Wodle

 - Use descriptive headers to make rule creation more intuitive

 - Consider security implications when running PowerShell commands

 - Monitor performance impact of complex commands
