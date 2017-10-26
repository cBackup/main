# First steps after installation

After you have successfully installed cBackup you want to add nodes you want to process. There are two options: [manual add](../administrators-guide/nodes#add-new-node-manually) or [network discovery](../administrators-guide/discovery). If you have large amount of nodes to process grouped together in networks, we encourage to use discovery. However initial setup requires decent amount of ground work.

# 1. Add authentication template

_Authentication template is a sequence of prompts and responses representing authentication sequence in command line interface_. It describes how particular device handles CLI authentication. Choose `Inventory -> Device auth templates` and add sequence for a particular device. On the right to the form, there're several examples, how authentication template can look like.

# 2. Add devices' models

Now you have to define your devices' models. To do so, choose `Inventory -> Devices`, press `Add device` button and fill out all fields in the form. If you have already defined authentication template for this device, you can choose it from dropdown list. Otherwise, you can click on <i class="fa fa-plus-square"></i> button to add new authentication template without leaving the page. 

# 3. Add credentials

Next you want to do is to define credentials. _Credentials is the set of data used for authentication while interacting with particular node_. Fill out the form with all known credentials details and save it. After saving, you can test credentials set against relevant IP-address filling out the right form.  

# 4. Define networks

To add nodes via discovery, first you want to define subnets. Choose `Inventory -> Subnets` and add networks in CIDR format (e.g. 192.168.5.0/24) you want to look through for nodes. You can choose predefined credentials or create new set on the fly, by pressing <i class="fa fa-plus-square"></i> button.

# 5. Discovery

Now you want to schedule discovery process. Choose `Schedule -> Schedules` and press `Add scheduled task` button. In the following form set task name to `discovery` and choose time when you want created discovery task to start. Restart Java Scheduler. Now your task discovery will start at time you specified. Or you can force discovery by pressing `Start` button next to the task in the list.

When the task is executed, Java daemon starts to look for nodes based on subnets you've specified. You can follow discovery process, in `Logs -> Scheduler`, and the end of discovery process is marked as `Task discovery is finished` message.

When task discovery is finished, at the top right corner in the <i class="fa fa-bell-o"></i> dropdown you will see new system messages. Discovery process will find all device attributes unknown to cBackup. Add these unknown device attributes to corresponding device models. Mark all system messages as approved and run discovery again. If everything is correct, cBackup will add all your nodes to nodes table.

# 6. Task and worker creation

Now you have all your nodes discovered, but cBackup does not know what to do with them. There're some predefined tasks in `Processes -> Tasks`: _discovery_, _git_commit_, _log_processing_, _node_processing_, _save_, _stp_, _backup_. These tasks are considered as 'system' and can't be deleted, however some of them can be modified. For example, you can modify destination and description in the task `backup`.

To assign workers and jobs to tasks go to `Processes -> Workers & Jobs`. Press `Add worker` and fill out all required fields. Set task to `backup` and protocol to `SSH` or `Telnet`. We consider SSH more preferable than Telnet, however you are free to choose. Now you want to add jobs to worker. Find your newly created worker and point mouse over it, you will see available actions press `+` to create new job. Add all necessary jobs for your device to get configuration from it. 

For more detailed information about how to create workers and jobs please see [related chapter of documentation](../administrators-guide/processes)

# 7. Assign task to nodes

To assign task `backup` to existing nodes and devices, go to `Processes -> Task assignments`. First let’s add task and worker to Devices. Select `Device Tasks` tab, press `Advanced task assign` and in the form choose task `backup` and worker you created in previous step. Confirm. You will be redirected to assignment form. Choose all devices you want to backup.

Now go to `Processes -> Task assignments` and select `Node tasks` tab. Press `Advanced task assign`. In the form choose task `backup` and leave the worker empty. Confirm. You will be redirected to assignment form. Choose all nodes you want to backup.

For more detailed information about how to create workers and jobs please see [related chapter of documentation](../administrators-guide/processes)

# 8. Scheduling

The only thing left is adding task to schedule. Go to `Processes -> Schedules` and press `Add scheduled task` button. In the form set task name to `backup` and choose time when you want the task to start. Restart Java Scheduler. Now backup task will start at the time you specified. To run task backup at any time go to `Schedules`, find task backup in the list and press start button next to it.

# 9. Configure version control

To enable VCS functionality for tracking configuration changes tracking, you have to enable it in the configuration first. Go to `System -> System settings`, find `Git settings` section, fill out all required information and press `Save`. Next, press `Init repository`. To complete VCS support integration, you have to schedule system task `git commit` to be executed after all backups were performed.

# 10. Configure log and node purging

Finish initial setup by configuring task `log_processing` to purge logs after certain amount of days. By default `Logs lifetime` configuration value is set to 7 days, but you still need to schedule `log_processing` task.
