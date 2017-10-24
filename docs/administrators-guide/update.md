Live update subsystem utilizes Git and Yii2 migration functionality. To use live update on the installed cBackup you will need to have internet access from the server. If your cBackup system is zero-access (no access to the internet), the only option is to update cBackup manually.

# Live update

Open `System -> Update` menu and proceed with `Check for updates`. If any update is available, you'll see the information and button to run the update process.

> ## Warning
> During the update web interface will be locked for all users

Live update implements rollback functionality if something goes wrong. However we highly encourage to backup your system and database manually prior to update.

# Manual update

For this guide we'll assume that your cBackup is installed in `/var/www/html`

1. Create backups:
 
    ```
    $ tar czf /opt/backup-$(date +%Y-%m-%d).tar.gz -C /var/www/html .
    $ mysqldump -u root -p cbackup | gzip > /opt/backup-$(date +%Y-%m-%d).sql.gz
    ```

2. Download the latest update

    ```
    $ wget https://github.com/cBackup/main/archive/master.zip -P /opt
    ```

3. Create lock file in your cBackup installation folder to enable maintentance mode, blocking access to the interface

    ```
    $ touch /var/www/html/update.lock
    ```
 
4. Stop the service

    ```
    $ /var/www/html/service.sh stop
    ```

5. Unpack downloaded archive to your cBackup installation overriding all files

    ```
    $ unzip -o /opt/update.zip -d /var/www/html
    ```

6. Remove archive 

    ```
    $ rm /opt/update.zip
    ```

7. Restore permissions 

    ```
    $ /var/www/html/setpermissions.sh
    ```

8. Update database

    ```
    $ /var/www/html/yii migrate
    ```

9. Start service 

    ```
    $ /var/www/html/service.sh start
    ```

10. Remove lock file 

    ```
    $ rm /var/www/html/update.lock
    ```

Now update is finished, check if everything works as it is intended. 