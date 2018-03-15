cBackup change log
==================

1.1.2
-----

- Fix: Endless loading while adding authentication template in device modal
- Fix: Some missing translations and latest Yii2 framework comatibility issues

- Enh: Console command to flush all assets. Useful for updating cBackup instance

- Del: Live Update is no longer available. Failed in trust

1.1.0
-----

- Fix: Incorrect events' order on Dashboard (req@ilia)
- Fix: Dropdown fix for error on assign task update (req@undro)
- Fix: Device system description length enlarged to 1Kb (req@undro)
- Fix: Cache refresh on git settings changes
- Fix: Configuration text unexpected trimming in web interface
- Fix: Error if application.properties has special symbols in password
- Fix: Scenario for moving device moved from one IP to another now works, node's MAC address now is non unique 
- Fix: Escaping symbols in configs
- Fix: Now you are able to download file if config stored in database only
- Fix: After adding new worker via modal window select2 update went to incorrect url
- Fix: Got rid of warning due to caching issues when task destination is changed
- Fix: Removed Yii command task success message from Java Daemon custom task

- Enh: Yii2 framework updated to 2.0.14.1 for PHP 7.2 support (req@Dimon)
- Enh: Subnets sorting algorithm improved to sort them in natural way
- Enh: Mail event edit interface now has button 'Save and close'
- Enh: Java service has improved in terms of handling custom prompts
- Enh: Handling custom prompt
- Enh: Notification about java scheduler service reload after changing schedules
- Enh: Added quick link to backup errors in dashboard
- Enh: CLI custom prompt added (multiple requests)
- Enh: After multiple requests we added IP-address for newly discovered "Unknown devices"
- Enh: Multiple key shortcuts like CTRL+Y, plain Enter, etc added to authentication sequences and jobs
- Enh: Hyphens in models' names
- Enh: Improved messages in task/worker assignment related
- Enh: Download arbitrary config version from git commit history

- Dev: Nortel supported with separate factory due to SSH optionHandler modification
- Dev: Juniper supported, regex sequence modified 
- Dev: Hewlett Packard supported with 'press any key' and regex sequence modification

- Web: Added plugin download section
- Web: Added cookbook with troubleshooting and more convenient documentation
