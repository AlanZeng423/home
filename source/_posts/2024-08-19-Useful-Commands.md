---
layout: post
title: Useful Commands
author: AlanZeng
date: 2024-08-18 11:12:30 -0800
tags: Development
---

# Useful Commands

## Git
When you are using Git, you may encounter some problems. Here are some useful commands to help you solve them.

1. Set the postBuffer size to 500MB
When meeting:

```bash
error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400
send-pack: unexpected disconnect while reading sideband packet
Writing objects: 100% (635/635), 2.07 MiB | 2.53 MiB/s, done.
Total 635 (delta 81), reused 0 (delta 0), pack-reused 0
fatal: the remote end hung up unexpectedly
Everything up-to-date
```

You can set the postBuffer size to 500MB:

```bash
git config http.postBuffer 524288000
```