!!! note "Installation fundamentals"
    Using RPM or DEB packages, installation process can be divided in 2 stages:
    
    1. [Prepare server](#1-prepare-server)
    2. [Setup cBackup](#2-setup-cbackup)

### 1. Prepare server

To use cBackup you want to have Linux server (Windows is not officially supported yet) with the following software:

* PHP 7.0 or newer
    * With the following extensions: _mbstring, snmp, SSH2, Reflection, pcre, spl, ctype, openssl, intl, mysqlnd, pdo_mysql, PDO, gmp, curl, zip_
* Web server (e.g. Apache or NGinx)
    * PHP support must be enabled as module or FastCGI/FPM
* MySQL-compatible database server of 5.5 or newer (Oracle MySQL, MariaDB, Percona)
* Java Runtime 8.0.10 or newer
* Git 1.8 or newer
* NetSNMP 5.7 or newer
* libCurl 7.29 or newer
* OpenSSH

First, install operating system. We recommend using latest x64 distribs like CentOS 7, Ubuntu 16 with systemd (systemctl) init management system. Further in this documentation we consider minimal package is installed and related software should be installed manually.

!!! warning "OS-related settings"
    While choosing your operating system, make sure, your security settings are adjusted to necessary level. E.g. **SELinux** in CentOS must be set to `permissive` or `disabled` state. Firewalld, ufw or iptables must allow connections to the web server. And so on and so forth. 

_OS_ | _Documentation_ | _Comment_ | Note 
--------- | --------- | --------- | ---------
CentOS 6 | [/getting-started/servers/centos6](/getting-started/servers/centos6.md) | Can be applied to SysV init CentOS 6 operating system | Disable SELinux and setup iptables
CentOS 7 | [/getting-started/servers/centos7](/getting-started/servers/centos7.md) | Can be applied to all latest RHEL-based distribs with systemctl | Disable SELinux and setup firewalld
Ubuntu 16 | [/getting-started/servers/ubuntu16](/getting-started/servers/ubuntu16.md) | Can be applied to all latest Debian-based distribs | Setup ufw if necessary
Other | [/getting-started/servers/general](/getting-started/servers/general.md) | General description of manual installation on any *nix system | -

## 2. Setup cBackup

First, following the guide from the table above, install DEB or RPM package and then proceed to cBackup web installer. This process is maintained by wizard and contains of 5 steps. Every step is reversable, so you are able to go back manually or wizard will redirect you to the erroneous step giving you a chance to fix certain options.

!!! note
    Detailed guide for web core setup, installation second stage, is [available here](install-web.md).

