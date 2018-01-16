!!! cite "General info"
    This section describes cBackup manual installation on Linux operating system from TAR.GZ source with Apache or Nginx web server. If you are system administrator who likes to control every step and every bit of process - here's your guide.

#### Update system and disable SELinux

Make sure system has all latest updates and security addons (like SELinux) either are disabled, permissive or properly set up to work with third-party software. Firewall should be adjusted to serve HTTP/HTTPS traffic. 

#### Install required software

To proceed you'll need: `wget`, `git`, `net-snmp` and `jre` (or any other java 8 runtime like `openjdk`).

#### Install web server, MySQL server and PHP 7

Setup LAMP/LEMP (Apache or NGinx in accordance) bundle: **web server**, **PHP 7** and **MySQL-based database server**. For MySQL you are free to choose from Oracle MySQL, Percona or MariaDB based on MySQL 5.5 or higher. For PHP 7 you will need following extensions: `php-gmp`, `php-zip`, `php-intl`, `php-ssh2`, `php-snmp`, `php-mbstring`, `php-mcrypt`, `php-bcmath`, `php-cli` and `php-curl`. If you are installing PHP as a FastCGI, don't forget to install `php-fpm`. Make sure the whole bundle is up, placed in autostart, running and serving PHP documents properly. Prepare your web root and proper FQDN for your cBackup installation.

Prepare user and database for cBackup. You want to use MySQL console to complete this task:

```mysql
CREATE DATABASE cbackup CHARSET utf8 COLLATE utf8_general_ci;
CREATE USER 'cbackup'@'localhost' IDENTIFIED BY 'mypassword';
GRANT USAGE ON *.* TO cbackup@localhost;
GRANT ALL PRIVILEGES ON cbackup.* TO cbackup@localhost;
```

#### Download archive and unpack it

You may want to change path where you cBackup is downloaded and extracted.

```bash
wget -O cbackup.tar.gz "http://cbackup.me/latest"
tar xvf cbackup.tar.gz
```

#### Adjust file owner for your installation

`chown` your extracted files/folder adjusting owner in accorance with your web server. E.g. it could be `apache:apache` or `nginx:nginx` for different servers. In case of using PHP-FPM, make sure which user is used for running FastCGI process.

#### Add cbackup system group and user

Replace `{DIRECTORY}` with your cbackup installation folder and `{apache}` with your web server or FastCGI process owner group. This will create _cbackup_ system user with supplementary group of your web server. 

```bash
groupadd -r cbackup
useradd -r -g cbackup -G {apache} -d {DIRECTORY} -s /bin/bash -c "cBackup System User" cbackup
``` 

#### Place supplementary configurations

There are several subfolders in the folder `./install/system` with configurations for systemd, sysvinit, logrotate, sudoers, firewalld and rsyslog. It's mandatory to configure at least two things:

* **Sudoers**<br>
  Copy `cbackup` file to your `/etc/sudoers.d` directory from `./install/system/centos/systemctl/etc/sudoers.d` or from `./install/system/centos/initd/etc/sudoers.d` depending if your operating system is controlled by systemd or sysvinit
  <br><br>
* **System daemon, systemctl**<br>
  For `systemctl` copy `cbackup.service` unit file from `./install/system/centos/systemctl/usr/lib/systemd/system` to your `systemd/system` folder. Don't forget to adjust path to `cbackup.jar` file in the unit file itself.
  <br><br>
* **System daemon, sysvinit**<br>
  For `SysV`, make a symlink to `cbackup.jar` into your `init.d` or `rc.d` like `ln -s /opt/cbackup/bin/cbackup.jar /etc/init.d/cbackup`. Now you can control it as a regular system service, e.g. `/etc/init.d/cbackup status`. 

#### Setup web server

Point web server wwwroot to the folder `web` in the unpacked cBackup installation. Under no circumstances any files or folders _above_ the `web` folder should be accessible. Actually, there's a check in the setup wizard which won't allow you to proceed unless installation is secured.   

#### Reload services

```bash
systemctl daemon-reload
systemctl restart httpd
```

#### Start cBackup web setup

Open up you browser pointing to `http://your.server.name/index.php` and compele setup process, providing promted data to wizard. Please note, that when setup is complete, installation directories are removed and if you have forgotten to copy system configurations like sudoers or systemctl unit file, extract them from archive again.

#### Register cbackup daemon

Use `systemctl enable cbackup` or `chkconfig cbackup on` for systemctl and sysvinit in accordance, to make cBackup daemon start with server automatically on boot.