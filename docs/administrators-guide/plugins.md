# Introduction

Plugins are addons for cBackup, providing additional functionality in web interface. Our team is certain that _tool with a word 'backup' in its name must do backups_, therefore services aside from the primary one should be moved to separate packages.

We do encourage development of plugins and created [the guide for developers](../contributors-guide/plugins.md) with detailed step-by-step explanation for plugin creation process. Also you can always request help on [official forums](http://cbackup.me/forum). However, on official downloads page only cBackup approved plugins will be stored ex tunc.

!!! warning
    Plugins have access to the whole application namespace and database. Installing unapproved plugin from a third-party you do it at your own peril.   

# Management

In the menu `System -> Plugin manager` you can see list of plugins if there're any already installed in the system. Each plugin can have its own settings (click on plugin's name to manage its settings), each plugin can be deleted or disabled. Also you can check full plugin information in it's description `Plugin metadata`

To install new plugin, go to the corresponding tab in `Plugin manager`. You want to browse for ZIP archive with plugin. The update is performed in the same way - simply upload new ZIP archive and all necessary procedures will be performed automatically.
