!!! cite "General info"
    This section describes cBackup installation for Ubuntu 16 LTS from DEB package. If you are want to undergo manual installation, please refer to [general *nix installation description](/getting-started/servers/general.md). Also please note, that DPKG (or GDEBI) will unpack installation to `/opt/cbackup` by default and use Apache web server. If you want to choose e.g. Nginx, or place installation into different folder, refer to the same [general installation description](/getting-started/servers/general.md).

#### Update system

```bash
sudo apt-get update
sudo apt-get upgrade
reboot
```

#### Install required software

```bash
sudo apt-get install git snmp default-jre openssh-server
```

#### Install LAMP web server

```bash
sudo apt-get install lamp-server^
sudo mysql_secure_installation
```

This package will install all latest available in Ubuntu repository versions of required software. Just follow instruction showed during package installation. 

#### Install necessary php extensions

```bash
sudo apt-get install php-gmp php-zip php-intl php-ssh2 php-snmp php-mbstring php-mcrypt php-bcmath php-cli php-curl
```

#### Prepare user and database for cBackup

You want to use MySQL console to complete this task:

```mysql
CREATE DATABASE cbackup CHARSET utf8 COLLATE utf8_general_ci;
CREATE USER 'cbackup'@'localhost' IDENTIFIED BY 'mypassword';
GRANT USAGE ON *.* TO cbackup@localhost;
GRANT ALL PRIVILEGES ON cbackup.* TO cbackup@localhost;
```
    
#### Download cbackup DEB and install it

```bash
wget -O ~/cbackup.deb "http://cbackup.me/latest?package=deb"
cd ~ && sudo dpkg -i cbackup.deb
```

Being prompted for new `cbackup` user password, consider adding proper one. It will be used to manage system daemon via SSH.

#### Restart apache and syslog services

```bash
sudo systemctl restart apache2
sudo systemctl restart rsyslog
```

#### Start cBackup web setup

Open up you browser pointing to `http://your.server.name/cbackup/index.php` and compele setup process.

!!! cite "Setup complete"
    Now you can start using your cBackup and proceed with its [initial setup](/getting-started/initial-setup.md)
