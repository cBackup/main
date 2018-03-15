!!! cite "Note"
    Please note, that since version 1.1.2 Live update feature is no longer available due to numerous issues. We have put different "live update" implementation on our schedule but for now manual update is the only option.

# Manual update

For this guide we'll assume that your cBackup is installed in `/opt/cbackup`

1. Create backups (or even better - make full system snapshot):

        $ tar czf /opt/backup-$(date +%Y-%m-%d).tar.gz -C /var/www/html .
        $ mysqldump -u root -p cbackup | gzip > /opt/backup-$(date +%Y-%m-%d).sql.gz

2. Download the latest update
    
        $ wget http://cbackup.me/latest?package=update -P /opt -O update.tar.gz

3. Create lock file in your cBackup installation folder to enable maintentance mode, blocking access to the interface
    
        $ touch /var/www/html/update.lock
 
4. Stop the service<br>In case of systemd use `sudo systemctl stop cbackup`<br>In case of SysVinit use `sudo service cbackup stop`<br><br>

5. Unpack downloaded archive to your cBackup installation overriding all files
    
        $ tar -xzf /opt/update.tar.gz -C /opt/cbackup

6. Remove archive 
    
        $ rm -f /opt/update.tar.gz
        
7. Restore permissions<br>If you have nginx or running web server with another user:group - adjust corresponding data

        $ chown -R apache:apache /opt/cbackup

8. Update database
    
        $ /opt/cbackup/yii migrate

9. Flush cache and runtime resources

        $ /opt/cbackup/yii cache/flush-all
        $ /opt/cbackup/yii asset/flush-all

10. Start service 
    
        $ sudo systemctl start cbackup

11. Remove lock file 
    
        $ rm /opt/cbackup/update.lock

!!! note "Pay attention"
    It's strongly recommended to reset your browser cache for your cBackup installation by pressing CTRL+F5

!!! cite "Update is complete"
    Now update is finished, check if everything works as it is intended. 
