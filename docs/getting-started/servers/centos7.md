#### Update system

```bash
yum update
reboot
```
    
#### Install required software

```bash
sudo yum install -y chrony wget mlocate git net-snmp net-tools epel-release yum-utils jre 
```
    
#### Install web server

To install nginx, follow [the instructions on official website](http://nginx.org/en/linux_packages.html), to install Apache use:
 
```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```
    
#### Install PHP

For RHEL-based distrib you want to add repository with PHP 7 or newer. E.g. for CentOS it could be [REMI repository](https://rpms.remirepo.net/):

```bash
sudo rpm -ivh https://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum-config-manager --enable remi-php71
sudo yum install -y php php-gmp php-pecl-zip php-pdo php-mysqlnd php-intl php-pecl-ssh2 php-snmp php-mbstring php-mcrypt php-bcmath php-common php-cli
    
# If you have nginx as web server, install PHP-FPM
sudo yum install -y php-fpm
```    
 
#### Install MySQL

Either from _base_ repository or go to mariadb.org and setup external repo:

```bash
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
mysql_secure_installation
```
    
#### Adjust security

```bash
firewall-cmd --add-service=http --permanent
firewall-cmd --reload
setenforce 0
```

#### Create user

```bash
useradd cbackup
passwd cbackup
```

#### Upload cbackup installation

```bash
wget ...
tar xvf release-prod.tar.gz
rm -f release-prod.tar.gz

# Adjust owner for your DocumentRoot
chown -R apache:apache /var/www/html
```

#### Set document root

* **For apache**:<br>
make cbackup `web` folder your web server's root by setting `DocumentRoot` directive in `/etc/httpd/conf/httpd.conf` to `/var/www/html/web/`. If you have virtualhost, adjust corresponding value in your `/etc/httpd/conf.d/` configuration file<br><br>
* **For nginx:**<br>
make cbackup `web` folder your web server's root by setting `root /var/www/html;` in `/etc/nginx/conf.d/default.conf` in server{} section.

#### Start installation

Open up you browser pointing to `http://your.server.name/index.php` and compele setup process.

#### Register cbackup daemon

!!! note
    Detailed information about registering service is [available here](/getting-started/servers/service.md).

!!! cite "Setup complete"
    After you've registered service you can start using your cBackup and proceed with its [initial setup](/getting-started/initial-setup.md)
