# PAtools Integration

This document describes the process of integrating a new BLS plugin/Driver in PAtools using the Template_PowerSupply_BLS module. This document assumes you have  the LabView side of the BLS plugin ready and the PXI target has the EVO runtime installed.

# Deploy plugin to PXI
1. The BLS Plugin, e.g. "BLS PowerSupply Template.1.0.lvlib" should be saved under the following path on the PXI:
/usr/lib/x86_64-linux-gnu/ni-evo-engine/plugins

2. The permission of the file "BLS PowerSupply Template.1.0.lvlib" should be adataped so every user is allowed to read, write and execute the file:

![file rights](../../docs/img/file-rights.png)

# Create PAtools driver

1. If you do not already have the Template_PowerSupply_BLS module in your Database import it:

![Module Import](../../docs/img/Module-Import.png)

![Import BLS PowerSupply Template ](../../docs/img/Import-BLS-PowerSupply-Plugin-Template.png)

2. Click on the module with the right mouse button and select "Duplicate folder...".

![Duplicate module](../../docs/img/Duplicate_Module.png)

3. The window for duplicating the module opens:

    ![Duplication](../../docs/img/Duplication.png)

    Adapt the Target Path as you like. In Find* enter: "Template_PowerSupply_BLS" and in Replace* enter your device name / a modul name, e.g. "NI_RMX412X". Then press "Duplicate".
    Note: In the following the used Normnames/Variables/Group names will all start with "NI_RMX412x" for you they will start with what ever you entered in the Replace* field.

4. After the duplication, the module "NI_RMX412X_(Module_NI_RMX412X) appears in the folder you selected

5. Must do Adaptions:

    5.1 In the "NI_RMX412X_UB" Variables group (NI_RMX412X_system/userbox)
        * NI_RMX412x_Main.UB.Header: Enter a name you want to display in the Userbox, e.g. "NI_RMX412X

    5.2 In the "NI_RMX412X_Version" Variables group (NI_RMX412X_system/version)
        * NI_RMX412x_Version: 1.0.0 (enter a version you would like to start with, 1.0.0 is an example here)

    5.3 In the PAbasic "NI_RMX412X_Version" adapt the content so you give the information when you created that module, who did create it and which template version you used, e.g. like that:

    ![Version](../../docs/img/version.png)

    5.4 In the Initialization of Variables group "NI_RMX412X_Config":

    * BLS Plugin Address: Enter the address of the device, could be an IP address
    * BLS Instance Name: Give an unique Instance Name under which the plugin should be loaded
    * BLS Plugin Execution Frequency: Select the Frequency with which you want to execute the plugin in Hz
    * BLS Plugin Name: Name of the plugin, e.g. "BLS Power Supply Template"
    * BLS Pugin Version: Enter the plugin version, e.g. "1.0"
    * Timeout for initializing: Give a value in seconds how to long to wait until a timeout is triggered

    Note: When you adapt the module later you can increase the version and add also information here. 

6. Adaptions if you added something to the Plugin Configuration:
    The plugin configuration string is build in the PAscript-Graph "NI_RMX412X.PS" (NI_RMX412X_system).

    ![Config](../../docs/img/Build_Config.png)

    Adapt how "NI_RMX412X_PluginConfiguration" is build together so it matches your configuration. If you added parameters, create normnames for them, add them as global variables and also add them in the Initialization of Variables group "NI_RMX412X_Config".

    Note: If the Config json string is getting to large for PAtools (>4096 characters) you need to place the config on the PXI and write the Path to that config in NI_RMX412X_PluginConfiguration.

7. Adaptions if you added/removed Consumer Channels

8. Adaptions if you added/removed Producer Channels

9. Adapt Userbox

10. Adaptions if you have a different amount of channels compared to the template

11. Adapt Mappings

12. Optionally you can add additional functionality in the driver

13. Add the driver to your application and test it
