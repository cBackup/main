# Prepare environment

To use cBackup you want to have Linux server with the following software:

* PHP 7.0 or newer with the following modules:
    * mbstring
    * snmp
    * SSH2
    * Reflection
    * pcre
    * spl
    * ctype
    * openssl
    * intl
    * mysqlnd
    * pdo_mysql
    * PDO
    * gmp
    * curl
    * zip
* Web server (e.g. Apache or NGinx)
    * PHP must be supported
    * PHP can work as module or FastCGI/FPM
* MySQL-compatible database server of 5.7 or newer (Oracle MySQL, MariaDB, Percona)
* Java Runtime 8.0.10 or newer
* Git 1.8 or newer
* NetSNMP 5.7 or newer
* libCurl 7.29 or newer

# Install cBackup

Installation process is maintained by wizard and contains of 5 steps. Every step is reversable, so you are able to go back manually or wizard will redirect you to the erroneous step giving you a chance to fix certain options. 

## 1. Initialization

Basic system requirements are being checked. Installation process will be aborted if web-server is configured incorrectly and system files are world-accessible. You want to mark the `web` folder as wwwroot in your web-server configuration.

Apache:
```apacheconfig
<VirtualHost *:%httpsport%>
   # ....
   DocumentRoot    /var/www/html/web
   # ....
</VirtualHost>
```

Nginx:
```
server {
   # ...
   location / {
      root /var/www/html/web;
      # ...
   } 
}
```

## 2. Requirements check

During this step installer checks if all required PHP extensions and environmental systems are available (including Java runtime and Git). 

## 3. Acquire credentials

You will be prompted to enter database and system credentials, as well as path to your Git executable if installer is unable to find it aidless. Fill all form inputs and proceed.

## 4. Integrity check

All settings are being set in the beginning of this step. Acquired data is saved to relevant files and database. Therefore the step might take some time to complete. When data is saved, the integrity check will be performed. If everything works as intended, you may proceed to final step and start working with cBackup.

Also all files and directories permissions will be checked. Look through if everything is set correctly. If necessary - fix it from the shell via `chmod` command. 

## 5. Finalizing

The final step removes all runtime installation data from the system and redirects you to the authentication page. 

------------

Now you may proceed with [initial cBackup setup](initial-setup), adjusting your networks, credentials, schedules and all other parts of configuration backup processes.
