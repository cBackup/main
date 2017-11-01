# Concept

Content delivery system is cBackup module intended to simplify system's usage in terms of hardware support. It allows to install support of new devices in one click, updating both [devices](devices) and [authentication templates](authentication/#authentication-templates) for them. Of course you can still manage entities manually, using the documentation herein.

!!! note
    It's impossible to use Content Delivery on zero-access systems. You need internet access to fetch data from external repository. 

When you open `System -> Content delivery` it will try to update content listings from external repository. It may take some time. Next you want to look through available categories: **Devices** and **Workers**. The first category contains hardware specifications for supported network equipment models, the second one contains command sequences. Find corresponding device and sequence and <i class="fa fa-save"></i> save them to your cBackup.

!!! warning
    If you have the similarly-named device or authentication template, you'll see the warning. Remove your device or template and fetch content again. 
    
By pressing <i class="fa fa-caret-square-o-down"></i> you can look through the code to be fetched to your cBackup. All code is plaing PHP using Yii2 framework notation and specifications. See [developers guide](../developers-guide/architecture.md) for more information.

# Managing installed entities

Once entry is downloaded it can be removed via corresponding cBackup functions as [device management](devices/#device-management) and [authentication template management](authentication/#authentication-templates). For reinstalling entry - see warning above.
