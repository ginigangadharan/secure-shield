---
layout: default
title: Process Hardening
permalink: linux/processes
tags: 
 - linux
 - rhel8
---


## 6.1 Ensure core dumps are restricted

```
# grep "hard core" /etc/security/limits.conf /etc/security/limits.d/*   <<< unsuccessful
# sysctl fs.suid_dumpable   <<<< Return error
# grep "fs\.suid_dumpable" /etc/sysctl.conf /etc/sysctl.d/* 
fs.suid_dumpable = 0
# systemctl is-enabled coredump.service

## Remediation:

# vi /etc/security/limits.conf
* hard core 0

# vi /etc/sysctl.conf
fs.suid_dumpable = 0

# sysctl -w fs.suid_dumpable=0

## If systemd-coredump is installed
# vi /etc/systemd/coredump.conf
Storage=none 
ProcessSizeMax=0

# systemctl daemon-reload
```

## 6.2 Ensure address space layout randomization (ASLR) is enabled

```
# sysctl kernel.randomize_va_space 
kernel.randomize_va_space = 2

# grep "kernel\.randomize_va_space" /etc/sysctl.conf /etc/sysctl.d/* 
kernel.randomize_va_space = 2

## Remediation:
## Add in /etc/sysctl.conf or a /etc/sysctl.d/* file:
kernel.randomize_va_space = 2

## Also run
# sysctl -w kernel.randomize_va_space=2
```