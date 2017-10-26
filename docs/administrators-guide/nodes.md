# Node management

Available actions: 

* **Edit node**<br>It's possible to edit node only if it was added manually. Auto discovered nodes are not editable.
* **Delete node**<br>As the name implies, you can delete node with all related data, including existing backups.

On the left you see node general information retrieved during the discovery process via SNMP protocol. All information is readonly, except for `Prepend location` and represents prefix for location OID. This prefix can be set in [system configuration](system-configuration). In each node you can define it's own prefix which will override the default one. 

Tabs on the right side contain related logs, data about subinterfaces (you can change primary interface for the node if needed), assigned tasks and authentication data.

The table below by default shows only one tab - actual configuration backup data. New tabs are added via plugins (e.g. 'geolocation'). Configuration backup can be viewed online, downloaded, copied to buffer (button `copy` becomes available when full configuration text is opened) or checked for changes. Changelog for node configuration is represented by `git log` diff functionality and looks the same. To track configuration changes, press <i class="fa fa-undo"></i> button and in the opened popup press <i class="fa fa-eye"></i> to view what has been changed. By default, only changes in last 31 days are shown (value can be set in [system configuration](system-configuration)).

# Exclusions

If any network contains node(s) you want to exclude from processing by cBackup, use `Nodes -> Exclusions` menu to manage exclusion list. In exclusions list under <i class="fa fa-caret-square-o-down" style=""></i> control element you can see node detailed information if device was previously discovered.

!!! note
    Node still will be discovered and added to node list, yet won't be processed by any tasks  

# Add new node manually

You can add nodes manually, not involving network discovery process. To do so, use `Nodes -> Add manually` menu and fill up the form. Prior to adding new node manually, make sure you have corresponding suitable credentials set saved in [Credentials](credentials) page.

1. Enter IP-address and choose corresponding credentials from dropdown list.
2. Press `SNMP inquire`. If SNMP polling works, form will be filled with retrieved data. Otherwise the error will be displayed.
3. Edit or fill up necessary data and save the node.

# Add nodes automatically

To search and update nodes in the particular subnets, you want to go through [Discovery](discovery) process.
