---
date: '{{ .Date }}'
draft: false
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
tags:
  - tag1
  - tag2
  - tag3
---
