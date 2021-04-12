---
description: 'https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist'
---

# Checklist - Linux Priv Esc



### **Best tool to look for Linux local privilege escalation vectors:** [**LinPEAS**](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)\*\*\*\*

### [System Information](https://book.hacktricks.xyz/linux-unix/privilege-escalation#system-information)

* [ ] Get **OS information**
* [ ] Check the [**PATH**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#path), any **writable folder**?
* [ ] Check [**env variables**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#env-info), any sensitive detail?
* [ ] Search for [**kernel exploits**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits) **using scripts** \(DirtyCow?\)
* [ ] **Check** if the [**sudo version** is vulnerable](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version)
* [ ] \*\*\*\*[**Dmesg** signature verification failed](https://book.hacktricks.xyz/linux-unix/privilege-escalation#dmesg-signature-verification-failed) error?
* [ ] More system enum \([date, system stats, cpu info, printers](https://book.hacktricks.xyz/linux-unix/privilege-escalation#more-system-enumeration)\)
* [ ] [Enumerate more defenses](https://book.hacktricks.xyz/linux-unix/privilege-escalation#enumerate-possible-defenses)

### [Drives](https://book.hacktricks.xyz/linux-unix/privilege-escalation#drives)

* [ ] **List mounted** drives
* [ ] **Any unmounted drive?**
* [ ] **Any creds in fstab?**

### \*\*\*\*[**Installed Software**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#installed-software)\*\*\*\*

1. [ ] **Check for** [**useful software**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#useful-software) **installed**
2. [ ] **Check for** [**vulnerable software**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#vulnerable-software-installed) **installed**

### [Processes](https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes)

* [ ] Is  any **unknown software running**?
* [ ] Is any software with **more privileges that it should have running**?
* [ ] Search for **exploits for running processes** \(specially if running of versions\)
* [ ] Can you **modify the binary** of any running process?
* [ ] **Monitor processes** and check if any interesting process is running frequently
* [ ] Can you **read** some interesting **process memory** \(where passwords could be saved\)?

### [Scheduled/Cron jobs?](https://book.hacktricks.xyz/linux-unix/privilege-escalation#scheduled-jobs)

* [ ] Is the [**PATH**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#cron-path) ****being modified by some cron and you can **write** in it?
* [ ] Any [**wildcard**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#cron-using-a-script-with-a-wildcard-wildcard-injection) ****in a cron job?
* [ ] Some [**modifiable script**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#cron-script-overwriting-and-symlink) is being **executed** or is inside **modifiable folder**?
* [ ] Have you detected that some **script** could be being [**executed** very **frequently**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#frequent-cron-jobs)? \(every 1, 2 or 5 minutes\)

### [Services](https://book.hacktricks.xyz/linux-unix/privilege-escalation#services)

* [ ] Any **writable .service** file?
* [ ] Any **writable binary** executed by a **service**?
* [ ] Any **writable folder in systemd PATH**?

### [Timers](https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers)

* [ ] Any **writable timer**?

### [Sockets](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets)

* [ ] Any **writable .socket** file?
* [ ] Can you **communicate with any socket**?
* [ ] **HTTP sockets** with interesting info?

### [D-Bus](https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus)

* [ ] Can you **communicate with any D-Bus**?

### [Network](https://book.hacktricks.xyz/linux-unix/privilege-escalation#network)

* [ ] Enumerate the network to know where you are
* [ ] **Open ports you couldn't access before** getting a shell inside the machine?
* [ ] Can you **sniff traffic** using `tcpdump`?

### [Users](https://book.hacktricks.xyz/linux-unix/privilege-escalation#users)

* [ ] Generic users/groups **enumeration**
* [ ] Do you have a **very big UID**? Is the **machine** **vulnerable**?
* [ ] Can you [**escalate privileges thanks to a group**](https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe) you belong to?
* [ ] **Clipboard** data?
* [ ] Password Policy?
* [ ] Try to **use** every **known password** that you have discovered previously to login **with each** possible **user**. Try to login also without password.

### [Writable PATH](https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-path-abuses)

* [ ] If you have **write privileges over some folder in PATH** you may be able to escalate privileges

### [SUDO and SUID commands](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-and-suid)

* [ ] Can you execute **any comand with sudo**? Can you use it to READ, WRITE or EXECUTE anything as root? \([**GTFOBins**](https://gtfobins.github.io/)\)
* [ ] Is any **exploitable suid binary**? \([**GTFOBins**](https://gtfobins.github.io/)\)
* [ ] Are [**sudo** commands **limited** by **path**? can you **bypass** the restrictions](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-execution-bypassing-paths)?
* [ ] \*\*\*\*[**Sudo/SUID binary without path indicated**?](https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-command-suid-binary-without-command-path)
* [ ] \*\*\*\*[**SUID binary specifying path**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#suid-binary-with-command-path)? Bypass
* [ ] \*\*\*\*[**LD\_PRELOAD vuln**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#ld_preload)\*\*\*\*
* [ ] \*\*\*\*[**Lack of .so library in SUID binary**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#suid-binary-so-injection) ****from a writable folder?
* [ ] \*\*\*\*[**SUDO tokens available**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#reusing-sudo-tokens)? [**Can you create a SUDO token**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#var-run-sudo-ts-less-than-username-greater-than)?
* [ ] Can you [**read or modify sudoers files**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#etc-sudoers-etc-sudoers-d)?
* [ ] Can you [**modify /etc/ld.so.conf.d/**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#etc-ld-so-conf-d)?
* [ ] \*\*\*\*[**OpenBSD DOAS**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#doas) ****command

### [Capabilities](https://book.hacktricks.xyz/linux-unix/privilege-escalation#capabilities)

* [ ] Has any binary any **unexpected capability**?

### [ACLs](https://book.hacktricks.xyz/linux-unix/privilege-escalation#acls)

* [ ] Has any file any **unexpected ACL**?

### [Open Shell sessions](https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-shell-sessions)

* [ ] **screen**?
* [ ] **tmux**?

### [SSH](https://book.hacktricks.xyz/linux-unix/privilege-escalation#ssh)

* [ ] **Debian** [**OpenSSL Predictable PRNG - CVE-2008-0166**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#debian-openssl-predictable-prng-cve-2008-0166)\*\*\*\*
* [ ] \*\*\*\*[**SSH Interesting configuration values**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#ssh-interesting-configuration-values)\*\*\*\*

### [Interesting Files](https://book.hacktricks.xyz/linux-unix/privilege-escalation#interesting-files)

* [ ] **Profile files** - Read sensitive data? Write to privesc?
* [ ] **passwd/shadow files** - Read sensitive data? Write to privesc?
* [ ] **Check commonly interesting folders** for sensitive data
* [ ] **Weird Localtion/Owned files,** you may have access or alter executable files
* [ ] **Modified** in last mins
* [ ] **Sqlite DB files**
* [ ] **Hidden files**
* [ ] **Script/Binaries in PATH**
* [ ] **Web files** \(passwords?\)
* [ ] **Backups**?
* [ ] **Known files that contains passwords**: Use **Linpeas** and **LaZagne**
* [ ] **Generic search**

### \*\*\*\*[**Writable Files**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files)\*\*\*\*

* [ ] **Modify python library** to execute arbitrary commands?
* [ ] Can you **modify log files**? **Logtotten** exploit
* [ ] Can you **modify /etc/sysconfig/network-scripts/**? Centos/Redhat exploit
* [ ] Can you [**write in ini, int.d, systemd or rc.d files**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#init-init-d-systemd-and-rc-d)?

### \*\*\*\*[**Other tricks**](https://book.hacktricks.xyz/linux-unix/privilege-escalation#other-tricks)\*\*\*\*

* [ ] Can you [**abuse NFS to escalate privileges**?](https://book.hacktricks.xyz/linux-unix/privilege-escalation#nfs-privilege-escalation)
* [ ] Do you need to [**escape from a restrictive shell**?](https://book.hacktricks.xyz/linux-unix/privilege-escalation#escaping-from-restricted-shells)

