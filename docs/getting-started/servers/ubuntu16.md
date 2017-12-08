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

#### Setting up environment

There's two ways how you can install all necessary web server packages first is LAMP(Linux Apache MySql PHP) second LEMP (Linux Nginx MySql PHP).

#### 1. Installing LAMP web server

#### Install web server

```bash
sudo apt-get install lamp-server^
sudo mysql_secure_installation
```

This package will install all latest available in Ubuntu repository versions of required software. Just follow instruction showed during package installation. 

After installation is finished install all necessary php-modules.
```bash
sudo apt-get install php-gmp php-zip php-intl php-ssh2 php-snmp php-mbstring php-mcrypt php-bcmath php-cli php-curl
```
    
#### Set document root

Make cbackup `web` folder your web server's root by setting `DocumentRoot` directive in `/etc/apache2/sites-enabled/000-default.conf` to `/var/www/html/web`. If you have virtualhost, adjust corresponding value in your `/etc/apache2/sites-enabled/` configuration file.

#### Reload service

```bash
sudo service apache2 restart
```

After web server installation is finished proceed with step "Server configuration".

#### 2. Installing LEMP web server

#### Install web server

```bash
sudo apt-get -y install nginx
```

#### Install PHP

We can make PHP work in nginx through PHP-FPM. It is an alternative PHP FastCGI implementation with some additional features useful for sites of any size, especially busier sites

```bash
sudo apt-get -y install php7.0-fpm
sudo apt-get install php7.0-gmp php7.0-zip php7.0-intl php7.0-mysql php7.0-snmp php7.0-mbstring php7.0-mcrypt php7.0-bcmath php7.0-curl php-ssh2
``` 
    
#### Install MySQL

```bash
sudo apt-get -y install mysql-server mysql-client
sudo mysql_secure_installation
``` 

#### Basic web server configuration

Make cbackup `web` folder your web server's root by setting `root` directive in `/etc/nginx/sites-enabled/default` in server{} section to `/var/www/html/web` in the same 
section locate `index` directive and add `index.php` to it. Uncomment `~ \.php$ {}` section in `/etc/nginx/sites-enabled/default` to enable php-fpm.

After changes were made reload nginx and php-fpm services

```bash
sudo service nginx reload
sudo service php7.0-fpm reload
```
 
## Server configuration
    
#### Adjust security

```bash
# ...
``` 

#### Create user

```bash
sudo adduser cbackup
```

Remember user cbackup password. This password will be asked during cBackup installation. 

#### Upload cbackup installation

```bash
wget ...
tar xvf release-prod.tar.gz
rm -f release-prod.tar.gz
chown -R www-data:www-data /var/www/html
```

#### Start installation

Open up you browser pointing to `http://your.server.name/index.php` and compele setup process.

#### Register cbackup daemon

!!! note
    Detailed information about registering service is [available here](/getting-started/servers/service.md).

!!! cite "Setup complete"
    After you've registered service you can start using your cBackup and proceed with its [initial setup](/getting-started/initial-setup.md)
