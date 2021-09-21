---
layout: default
title: Filesystem Integrity
permalink: linux/filesystem-integrity
description: FileSystem Integrity Checks
tags: 
 - linux
 - rhel8
---


## 4.1 Ensure AIDE is installed

```
rpm -q aide     <<<< Not installed

## Remediation:
dnf install aide

## Initialize AIDE:
aide --init
mv /var/lib/aide/aide.db.new.gz /var/lib/aide/aide.db.gz
```

## 4.2 Ensure filesystem integrity is regularly checked

```
systemctl is-enabled aidecheck.service
systemctl status aidecheck.service
systemctl is-enabled aidecheck.timer
systemctl status aidecheck.timer

## Remediation:
# cp ./config/aidecheck.service /etc/systemd/system/aidecheck.service # cp ./config/aidecheck.timer /etc/systemd/system/aidecheck.timer
# chmod 0644 /etc/systemd/system/aidecheck.*
# systemctl reenable aidecheck.timer
# systemctl restart aidecheck.timer
# systemctl daemon-reload

# crontab -u root -e
0 5 * * * /usr/sbin/aide --check
```