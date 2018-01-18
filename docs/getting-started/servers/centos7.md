!!! cite "General info"
    This section describes cBackup installation for CentOS 7 from RPM package. If you are want to undergo manual installation, please refer to [general *nix installation description](/getting-started/servers/general.md). Also please note, that RPM will unpack installation to `/opt/cbackup` by default and use Apache web server. If you want to choose e.g. Nginx, or place installation into different folder, refer to the same [general installation description](/getting-started/servers/general.md).

#### Update system and disable SELinux

```bash
yum update
sed -i --follow-symlinks 's/^SELINUX=.*/SELINUX=disabled/g' /etc/sysconfig/selinux
reboot
```

#### Install required software

```bash
sudo yum install -y chrony wget git net-snmp epel-release yum-utils jre 
```

#### Install web server

```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

#### Install PHP 7

For RHEL-based distrib you want to add repository with PHP 7 or newer. E.g. for CentOS it could be [REMI repository](https://rpms.remirepo.net/):

```bash
sudo rpm -ivh https://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum-config-manager --enable remi-php71
sudo yum install -y php php-gmp php-pecl-zip php-pdo php-mysqlnd php-intl php-pecl-ssh2 php-snmp php-mbstring php-mcrypt php-bcmath php-common php-cli
```    

#### Install MySQL

Either from _base_ repository or go to [mariadb.org](https://mariadb.com/kb/en/library/yum/) and setup external repo:

```bash
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
mysql_secure_installation
```

Prepare user and database for cBackup. You want to use MySQL console to complete this task:

```mysql
CREATE DATABASE cbackup CHARSET utf8 COLLATE utf8_general_ci;
CREATE USER 'cbackup'@'localhost' IDENTIFIED BY 'mypassword';
GRANT USAGE ON *.* TO cbackup@localhost;
GRANT ALL PRIVILEGES ON cbackup.* TO cbackup@localhost;
```
    
#### Adjust security

```bash
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```

#### Download cbackup RPM and install it

```bash
wget -O ~/cbackup.el7.noarch.rpm "http://cbackup.me/latest?package=rpm&sub=el7"
cd ~ && sudo rpm -ivh cbackup.el7.noarch.rpm
```

#### Change cbackup system user password and restart httpd service

```bash
sudo passwd cbackup
sudo systemctl restart httpd
```

This `cbackup` system user will be used to manage system daemon via SSH.

#### Start cBackup web setup

Open up you browser pointing to `http://your.server.name/cbackup/index.php` and compele setup process.

!!! cite "Setup complete"
    Now you can start using your cBackup and proceed with its [initial setup](/getting-started/initial-setup.md)
