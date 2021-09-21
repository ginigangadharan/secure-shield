---
layout: default
title: SELinux Configuration
permalink: linux/selinux
tags: 
 - linux
 - rhel8
---


## 7.1 Ensure SELinux is installed

```
rpm -q libselinux

## Remediation:
# dnf install libselinux
```

## 7.2 Ensure SELinux is not disabled in bootloader configuration

```
grep -E 'kernelopts=(\S+\s+)*(selinux=0|enforcing=0)+\b' /boot/grub2/grubenv   
## <<<< Nothing should be displayed

## Remediation:
## Edit /etc/default/grub and remove all instances of selinux=0 and enforcing=0 from all CMDLINE_LINUX parameters:
GRUB_CMDLINE_LINUX_DEFAULT="quiet" 
GRUB_CMDLINE_LINUX=""

# grub2-mkconfig -o /boot/grub2/grub.cfg
```

## 7.3 Ensure SELinux policy is configured


```
# grep -E '^\s*SELINUXTYPE=(targeted|mls)\b' /etc/selinux/config 
SELINUXTYPE=targeted

# sestatus | grep Loaded
Loaded policy name: targeted

## Remediation:
## in /etc/selinux/config file to set the SELINUXTYPE parameter: 
SELINUXTYPE=targeted
```

## 7.4 Ensure the SELinux state is enforcing

```
# grep -E '^\s*SELINUX=enforcing' /etc/selinux/config
SELINUX=enforcing

# sestatus
SELinux status: enabled
Current mode: enforcing
Mode from config file: enforcing

## Remediation:
## Edit the /etc/selinux/config file to set the SELINUX parameter: 
SELINUX=enforcing
```

## 7.5 Ensure no unconfined services exist

```
## should be no output
# ps -eZ | grep unconfined_service_t
```

## 7.6 Ensure SETroubleshoot is not installed

```
# rpm -q setroubleshoot
package setroubleshoot is not installed

## Remediation
# dnf remove setroubleshoot
```

## 7.7 Ensure the MCS Translation Service (mcstrans) is not installed

```
# rpm -q mcstrans
package mcstrans is not installed

## Remediation
# dnf remove mcstrans
```