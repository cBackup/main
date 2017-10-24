# User settings

There're two configuration sections available: user settings and system-wide settings. The first one is available as submenu items under your username on the top right corner of the screen. Two options are available:

1. **Profile**<br>
    Here you can change your full name, password, mail and access token.<br><br>
2. **Settings**<br>
    Here you can adjust personalization options such as date format, interface language and interface options.
    
---------

# System settings

These settings dilate to the whole system. Four global sections are available in system settings:

## Global settings

1. **Administrator email**<br>
    Mail recipient for all major reports, by default it's equal to your root user's mail.<br><br>

2. **Nodes lifetime**<br>
    This settings defines how long unreachable node will stay in database. By default it's `0`, so no nodes will be purged from database. Adjust this value according to your needs and policies.<br><br>

3. **Logs lifetime**<br>
    This setting defines how long log entries will be stored in database. Logs are main database disk space consumers, so limiting this value will have major impact on how much disk space database will utilize. By default it's `7` days. For 1200 nodes with daily discovery and backup processes 7 days of logs consume ~13 Mb on INFO logging level.<br><br>
    
4. **System log level**<br>
    This setting defines how much detalization do you need. Logging levels are identical to default *nix system logging levels.

## Git settings

1. **Use Git**<br>
    Git functionality is one of main cBackup features and shoud not be ignored if you want to run the tool at its' full potential. Git repository initialization will be run in the directory marked as backup root (see `Path to storage folder` from [Background process settings](#background-process-settings))<br><br>
    
2. **Git username**, **Git email**<br>
    Username and email which will be used as author credentials for configuration file commits<br><br>
    
4. **Use git remote**<br>
    You can push data to remote Git repository, if you would like to use it as additional safety replication layer. E.g. you can push it to your local gitlab installation. 
    
    !!! warning
         We strictly discourage you from using Github, Bitbucket or any other public services as long as your configuration files can contain sensitive data.
    
3. **Git path**<br>
    Path to git executable, ensure it's valid
    
!!! note
    After saving configuration, two buttons on top of the section's panel will become available: **Init repository** and **Reinit Git settings**. You want to initialize repository upon the first run to start using Git. Initialization writes down `.git` folder with related metadata.

## Mailer settings

All settings should be understandable. You can adjust sender address and choose between SMTP or sendmail transport, adjusting related variables if necessary. These settings will be used sending regular scheduled reports or dumping critical errors in case of emergency.

## Background process settings

These settings are related to the cBackup Java daemon:

1. **SNMP timeout**<br>
    Increase it if necessary, on LAN 500ms should be enough<br><br>
    
2. **SNMP retries**<br>
    How many attempts daemon will make trying to reach the node, 3 by default<br><br>
    
3. **Telnet timeout**<br>
    Generally it has to be substantially longer than SNMP timeout<br><br>
    
4. **Telnet before send delay**<br>
    We recommend putting at least 200 ms delay before command send<br><br>
    
5. **SSH before send delay**<br>
    We recommend putting at least 1000 ms delay before command send<br><br>
    
6. **Path to storage folder**<br>
    Where all config data is stored, must exist and be writable<br><br>
    
7. **Thread count**<br>
    How much threads Java daemon will launch. For two cores on VM on Xeon E5620, 30 threads utilizes CPU completely when backup is running, but yet without excessive overload
