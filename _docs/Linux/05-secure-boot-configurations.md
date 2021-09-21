---
layout: default
title: Secure Boot
#description: 
permalink: linux/secure-boot
tags: 
 - linux
 - rhel8
---


## 5.1 Ensure permissions on bootloader config are configured

```
stat /boot/grub2/grub.cfg
(make sure uid and gid are both 0/root and Access does not grant permission to group or other)

## Remediation:
# chown root:root /boot/grub2/grub.cfg
# chmod og-rwx /boot/grub2/grub.cfg
# chown root:root /boot/grub2/grubenv
# chmod og-rwx /boot/grub2/grubenv
```

## 5.2 Ensure authentication required for single user mode

```
# grep /systemd-sulogin-shell /usr/lib/systemd/system/rescue.service
ExecStart=-/usr/lib/systemd/systemd-sulogin-shell rescue

# grep /systemd-sulogin-shell /usr/lib/systemd/system/emergency.service
ExecStart=-/usr/lib/systemd/systemd-sulogin-shell emergency

## Remediation:
## Edit /usr/lib/systemd/system/rescue.service and add/modify the following line: 
ExecStart=-/usr/lib/systemd/systemd-sulogin-shell rescue

## Edit /usr/lib/systemd/system/emergency.service and add/modify the following line: 
ExecStart=-/usr/lib/systemd/systemd-sulogin-shell emergency
```