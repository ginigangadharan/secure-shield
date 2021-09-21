---
layout: default
title: Banner Configurations
permalink: linux/banners
tags: 
 - linux
 - rhel8
---

The `/etc/motd`, `/etc/issue`, and `/etc/issue.net` files govern warning banners for standard command line logins for both local and remote users.

## 8.1 Ensure message of the day is configured properly

```
## should return blank
# grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= - f2 | sed -e 's/"//g'))" /etc/motd

## Remediation:
## Edit the /etc/motd file with the appropriate contents, remove any instances of \m , \r , \s , \v or references to the OS platform
```

## 8.2 Ensure local login warning banner is configured properly

```
## should return blank
# grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= - f2 | sed -e 's/"//g'))" /etc/issue

## Remediation:
## Edit the /etc/issue file with the appropriate contents, remove any instances of \m , \r , \s , \v or references to the OS platform
```

## 8.3 Ensure remote login warning banner is configured properly

```
## should return blank
# grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= - f2 | sed -e 's/"//g'))" /etc/issue.net

## Remediation:
##Edit the /etc/issue.net file with the appropriate contents, remove any instances of \m , \r , \s , \v or references to the OS platform
```

## 8.4 Ensure permissions on /etc/motd are configured

```
# stat /etc/motd
Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)

## Remediation
# chown root:root /etc/motd
# chmod u-x,go-wx /etc/motd
```

## 8.5 Ensure permissions on /etc/issue are configured

```
# stat /etc/issue
Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)

## Remediation
# chown root:root /etc/issue
# chmod u-x,go-wx /etc/issue
```

## 8.6 Ensure permissions on /etc/issue.net are configured

```
# stat /etc/issue.net
Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)

## Remediation
# chown root:root /etc/issue.net
# chmod u-x,go-wx /etc/issue.net
```

## 8.7 Ensure GDM login banner is configured

```
## check /etc/gdm3/greeter.dconf-defaults
[org/gnome/login-screen] banner-message-enable=true banner-message-text='<refer to banner text>'

## Remediation - add above details
```

## 8.8 Ensure updates, patches, and additional security software are installed

```
## should be empty
# dnf check-update --security

## Remediation
# dnf update --security
```