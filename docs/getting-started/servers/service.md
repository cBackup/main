# OS with systemctl 

```bash
# Copy service systemctl script
cd /var/www/html

# For CentOS
cp bin/system/systemctl/usr/lib/systemd/system/cbackup.service /usr/lib/systemd/system/

# For Ubuntu
cp bin/system/systemctl/usr/lib/systemd/system/cbackup.service /etc/systemd/system

systemctl daemon-reload

# Run and enable daemon
systemctl start cbackup
systemctl enable cbackup

# Adjust sudoers to enable web core communicate with systemctl
cp bin/system/systemctl/etc/sudoers.d/cbackup /etc/sudoers.d/
```

# OS with init.d

```bash
# Copy service systemctl script
cd /var/www/html
cp bin/system/initd/etc/init.d/cbackup /etc/init.d/

# Run and enable daemon
/etc/init.d/cbackup start
chkconfig cbackup on

# Adjust sudoers to enable web core communicate with systemctl
cp bin/system/initd/etc/sudoers.d/cbackup /etc/sudoers.d/
```

!!! cite "Setup complete"
    You should've completed this step as a third installation step. Now you can start using your cBackup and proceed with its [initial setup](/getting-started/initial-setup.md), adjusting your networks, credentials, schedules and all other parts of configuration backup processes.
