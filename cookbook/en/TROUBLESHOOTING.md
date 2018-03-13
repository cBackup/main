# Troubleshooting

**Error `"Can't get settings from API"`**<br>
Is shown, when Java-демон is unable to connect to API via HTTP. Check if API is available. Possible check:
  ```bash
  curl -I `cat /opt/cbackup/bin/application.properties | grep "\.site=" | cut -d'=' -f 2`?r=v1%2Fcore%2Fget-tasks  
  ``` 
  * If you see `401 Unauthorized` it means API is available via address set in application.properties file and you want to check login and password for Java service user.
  * If you see answer codes `302` or `200` it means, that API address is incorrect.

---

**How to handle `Unknown devices`**<br>
`Unknown devices` module is used to assign connection between devices' attributes and "vendor-model" pendant. It doesn't matter, where the _"unknown device"_ was found, it's signal from cBackup, that you need to "explain" how to handle this kind of devices. Press [+] to associate with previosly defined device. Or you may want to define new device if it's necessary.

---

**I don't see previous versions of configurations**<br>
To see diff's, it's necessary to process and/or run scheduled task `git_commit`. If necessary you may run it manually. If it's scheduled, make sure `git_commit` is being started _only after_ all nodes are processed.

---

**I see wrong time in logs and history**<br>
Check system time ___and___ parameter `date.timezone` in `php.ini`

---

**Is it possible to make backup file name to be equals node name?**<br>
No, it's not possible. Filename must be unqiue and this can be assured only by node ID. Hostnames can be non-unique or unset.

---

**I don't see `git_commit` task**<br>
Dropdown task lists and variables are mostly scrollable. We don't know why, but this fact is often missed :)

---

**After saving tasks, nothing changed**<br>
You have to restart internal scheduler after making changes to tasks schedules. It's a bad idea to do so automatically - when changes are made, system may process couple of thousands of nodes. Restart at this moment will ruin the integrity of backup process.

---

**Service status widget shows "Java scheduler is started", but first row is red**<br>

* Make sure, you have set correct login and password for user, who connects to server via SSH and requests service status. 
* Make sure in `/opt/cbackup/config/settings.ini` the parameter `serviceType` corresponds with your operating system. E.g. for Centos 6 it has to be `init.d`, for Centos 7 `system.d` and so on by analogy. For SysVinit operating systems set `init.d`, and for systemctl - `system.d`

---

**How to handle improper service handling in the widget?**<br>
You can read error message by hovering red triangle in the left part of erroneous row. Upper row corresponds to the daemon itself. Bottom row corresponds to the internal scheduler.
