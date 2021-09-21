---
# layout: default
title: sudo configuration
permalink: linux/sudo-configuration
description: Confugure sudo
tags: 
 - linux
 - rhel8
---


## Ensure sudo is installed

```
rpm -q sudo

# Remediation 
dnf install sudo
```

## Ensure sudo commands use pty

```
grep -Ei '^\s*Defaults\s+(\[^#]+,\s*)?use_pty' /etc/sudoers

# Remediation:
visudo -f /etc/sudoers 
## add 
Defaults use_pty
```

## Ensure sudo log file exists

```
grep -Ei '^\s*Defaults\s+([^#]+,\s*)?logfile=' /etc/sudoers /etc/sudoers.d/*

# Remediation:
visudo -f /etc/sudoers
Defaults logfile="/var/log/sudo.log"
```
