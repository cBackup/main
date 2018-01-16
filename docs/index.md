# cBackup

[![Minimum PHP Version](https://img.shields.io/badge/php-%3E%3D%207.0-8892BF.svg)](https://php.net/)
[![Java Version](https://img.shields.io/badge/java-%3E%3D%201.8-8892BF.svg?style=flat)](https://java.com/download/)
[![Documentation Status](https://readthedocs.org/projects/cbackup/badge/?version=latest)](http://cbackup.readthedocs.org)
[![Website](https://img.shields.io/website-up-down-brightgreen-red/http/cbackup.me.svg?label=website)](http://cbackup.me)

cBackup [siː ˈbækʌp] — free open source network equipment configuration backup tool.

# Features

* Scheduled network devices configuration backups
* Version control for configuration changes tracking
* Flexible configuration via web interface
* Multithreaded highly efficient java daemon
* Standalone privacy abiding deployment

# System requirements

* Linux server
* Web server
* Java 8, JRE
* MySQL 5.5 or newer (or compatible MariaDB, Percona, etc)
* Git 1.8 or newer
* NetSNMP
* OpenSSH
* libCurl
* PHP 7.0 or newer with necessary modules: _ctype, curl, gmp, intl, mbstring. mysqlnd, openssl, pcre, PDO, pdo_mysql, Reflection, snmp, SPL, SSH2, zip_

# Downloads

Title | Type | Link and version
--------- | --------- | ---------
Stable release, archive | TAR.GZ | [cbackup-1.0.0.tar.gz](http://cbackup.me/latest)
Stable release, CentOS 7 RPM | RPM | [cbackup-1.0.0-1.el7.noarch.rpm](http://cbackup.me/latest?package=rpm&sub=el7)
Stable release, CentOS 6 RPM | RPM | [cbackup-1.0.0-1.el6.noarch.rpm](http://cbackup.me/latest?package=rpm&sub=el6)
Stable release, Ubuntu 16 LTS | DEB | [cbackup-0.1.3.deb](http://cbackup.me/latest?package=deb)
Debug/devel release | TAR.GZ | [cbackup-1.0.0-debug-release.tar.gz](http://cbackup.me/latest?package=debug&sub=release)

# Community and support

* Issues can be reported to [Github](https://github.com/cBackup/main/issues) directly or via [forum](http://cbackup.me/forum);
* For support you can check [cBackup official website](http://cbackup.me) and [discord](http://cbackup.me/discord);
* Feel free to request features and new hardware support.

# cBackup Software License

cBackup is published under the GNU Affero General Public License (AGPLv3)<br>
Copyright 2017 © **cBackup Team**: Oļegs Čapligins, Imants Černovs, Dmitrijs Galočkins  

# cBackup Documentation License

Except where otherwise noted, content on this documentation is distributed under the following license: [CC Attribution-Noncommercial-Share Alike 4.0 International](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode)
