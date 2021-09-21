---
layout: default
title: Service Configuration
permalink: linux/services
tags: 
 - linux
 - rhel8
---

## 9.1 Ensure xinetd is not installed

```
# rpm -q xinetd
package xinetd is not installed

## Remediation
# dnf remove xinetd
```

## 9.2 Ensure time synchronization is in use

```
# rpm -q chrony
chrony-<VERSION>

## Remediation
# dnf install chrony
```

## 9.3 Ensure chrony is configured

```
# grep -E "^(server|pool)" /etc/chrony.conf 
server <remote-server>

# ps -ef | grep chronyd
chrony 491 1 0 20:32 ? 00:00:00 /usr/sbin/chronyd

## Remediation
## Add entry in /etc/chrony.conf
```

## 9.4 Ensure X Window System is not installed

```
# rpm -qa xorg-x11*

## Remediation
# dnf remove xorg-x11*
```

## 9.5 Ensure rsync service is not enabled

```
# systemctl is-enabled rsyncd
disabled

## Remediation
# systemctl --now disable rsyncd
```

## 9.6 Ensure Avahi Server is not enabled

```
# systemctl is-enabled avahi-daemon
disabled

## Remediation
# systemctl --now disable avahi-daemon
```

## 9.7 Ensure SNMP Server is not enabled

```
# systemctl is-enabled snmpd
disabled

## Remediation
# systemctl --now disable snmpd
```

## 9.8 Ensure HTTP Proxy Server is not enabled

```
# systemctl is-enabled squid
disabled

## Remediation
# systemctl --now disable squid
```

## 9.9 Ensure Samba is not enabled

```
# systemctl is-enabled smb
disabled

## Remediation
# systemctl --now disable smb
```

## 9.10 Ensure IMAP and POP3 server is not enabled

```
# systemctl is-enabled dovecot
disabled

## Remediation
# systemctl --now disable dovecot
```

## 9.11 Ensure HTTP server is not enabled

```
# systemctl is-enabled httpd
disabled

## Remediation
# systemctl --now disable httpd
```

## 9.12 Ensure FTP Server is not enabled

```
# systemctl is-enabled vsftpd
disabled

## Remediation
# systemctl --now disable vsftpd
```

## 9.13 Ensure DNS Server is not enabled

```
# systemctl is-enabled named
disabled

## Remediation
# systemctl --now disable named
```

## 9.14 Ensure NFS is not enabled

```
# systemctl is-enabled nfs
disabled

## Remediation
# systemctl --now disable nfs
```

## 9.15 Ensure RPC is not enabled

```
# systemctl is-enabled rpcbind
disabled

## Remediation
# systemctl --now disable rpcbind
```

## 9.16 Ensure LDAP server is not enabled

```
# systemctl is-enabled slapd
disabled

## Remediation
# systemctl --now disable slapd
```

## 9.17 Ensure DHCP Server is not enabled

```
# systemctl is-enabled dhcpd
disabled

## Remediation
# systemctl --now disable dhcpd
```

## 9.18 Ensure CUPS is not enabled

```
# systemctl is-enabled cups
disabled

## Remediation
# systemctl --now disable cups
```

## 9.19 Ensure NIS Server is not enabled

```
# systemctl is-enabled ypserv
disabled

## Remediation
# systemctl --now disable ypserv
```

## 9.20 Ensure mail transfer agent is configured for local-only mode

```
## should return blank
# ss -lntu | grep -E ':25\s' | grep -E -v '\s(127.0.0.1|::1):25\s'

## Remediation
## Edit /etc/postfix/main.cf and add below
inet_interfaces = loopback-only

# systemctl restart postfix
```

## 9.21 Ensure NIS Client is not installed

```
# rpm -q ypbind
package ypbind is not installed

## Remediation
# dnf remove ypbind
```

## 9.22 Ensure telnet client is not installed

```
# rpm -q telnet
package telnet is not installed

## Remediation
# dnf remove telnet
```

## 9.23 Ensure LDAP client is not installed

```
# rpm -q openldap-clients
package openldap-clients is not installed

## Remediation
# dnf remove openldap-clients
```