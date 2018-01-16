# General info

As you may already know, cBackup consists of two parts: **web core** and **daemon**. Web core is used for system management and daily work, and the daemon processes defined tasks, gathers data from nodes and runs discovery process through defined subnets. 

cBackup daemon itself is java executable file `cbackup.jar`, running as background service. Therefore it can be managed as a regular system service: you can start it, stop, restart, enable or disable its autostart with operating system controls (e.g. via `systemctl`). cBackup daemon is posessed by internal scheduler to avoid dependency on system crontab. 

# Shell

Also, the daemon opens its own SSH, so you can manage it internal processes. By default it listens on `8437` port, so to connect to it you want to use `ssh -p 8437 cbadmin@127.0.0.1` changing corresponding credentials, port number and/or IP-address. If you connect to your cBackup remotely, don't forget to allow its port in your server's firewall. 

Here's the list of commands available in cBackup shell:

_Command_ | _Description_ | _Additional keys_
----------- | ----------- | -----------
**help** | displays initial list of available commands | 
**exit** | gracefully exits the shell | 
**cbackup version** | displays the daemon version | add `-json` to retrieve result as json string
**cbackup status** | displays the current status of internal Scheduler service | add `-json` to retrieve result as json string
**cbackup start** | starts internal Scheduler service | add `-json` to retrieve result as json string
**cbackup restart** | restarts internal Scheduler service | add `-json` to retrieve result as json string
**cbackup stop** | stops internal Scheduler service | add `-json` to retrieve result as json string 
**cbackup runtask &lt;NAME&gt;** | runs specified task by it's name | add `-json` to retrieve result as json string 

# Logs

By default all service logs on systemd-controlled OS are falling into `/var/log/messages`. To forward it into separate log file, use syslog functionality. Please note, that on CentOS 6 (or other sysvinit) service logs are written into `/var/log/cbackup.log`.

**Snippet for rsyslog.conf**
    
    # cBackup
    # Place on top of rules or at least above /var/log/messages
    if $programname == 'cbackup.jar' then /var/log/cbackup
    if $programname == 'cbackup.jar' then stop

**Snippet for syslog-ng**

    destination d_cbackup { 
        file("/var/log/cbackup"); 
    };
    filter f_cbackup { 
        program("cbackup.jar"); 
    };
    log { 
        source(s_sys); 
        filter(f_cbackup); 
        destination(d_cbackup); 
    };
    
To omit cbackup log entry from going any further in syslog-ng (e.g. in _messages_), edit `filter f_default` adding corresponding condition there like:

    filter f_default { 
                     level(info..emerg) and
                     not (
                        facility(mail)
                        or facility(authpriv)
                        or program("cbackup.jar")
                        or facility(cron)
                     ); 
    };

# Rotate logs

As long as logging relies on syslog, you can add your new log `/var/log/cbackup` to `/etc/logrotate.d/syslog` file. Just make sure, there's `sharedscripts` directive in it, e.g.:

    /var/log/cron
    /var/log/cbackup/cbackup.log
    /var/log/maillog
    /var/log/messages
    /var/log/secure
    /var/log/spooler
    {
        missingok
        notifempty
        weekly
        rotate 4
        compress
        sharedscripts
        postrotate
            /bin/kill -HUP `cat /var/run/syslogd.pid 2> /dev/null` 2> /dev/null || true
        endscript
    }

Please note, that on CentOS 6 (or other sysvinit) you want to logortate `/var/log/cbackup.log` with `copytruncate` option to avoid file open resource reset, e.g.:

    /var/log/cbackup.log {
        weekly
        missingok
        notifempty
        rotate 4
        compress
        copytruncate
    }
