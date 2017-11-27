# Database table `config`

### java* varaibles

At this moment there's only `javaIP` variable and it represents the IP-address of server, running java daemon. Daemon uses API to work with cBackup, so, theoretically it can be launched on separate server.

### javaScheduler* variables

Used to manage _processes inside the java daemon_. Check if internal scheduler is running, what tasks are processing right now, push any task to immediate execution, etc.

### javaServer* variables

Used to manage _the whole daemon itself_. We check its' status, stop or restart the whole java daemon.