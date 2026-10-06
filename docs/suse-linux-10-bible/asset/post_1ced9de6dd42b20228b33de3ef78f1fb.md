
# Chapter 9 ◆ Configuring the System with YaST

1. To bring up the Boot Loader Settings screen (see Figure 9-14), select Boot Loader Configuration.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_283_0.png)

Figure 9-14: The boot loader configuration in YaST

2. To add a new boot option, select Add. This brings you to a configuration screen that enables you to create a new configuration, either by cloning an existing boot loader entry or by creating a standard Linux, Xen, or Chainloader configuration. A Chainloader configuration is what you need if you want to boot a Windows system (see Figure 9-15).

3. Now click the Next button to produce a new configuration.

4. As this is another Linux kernel being installed, change the kernel and initial ramdisk entries to reflect the newly installed kernel and initial ramdisk by selecting the kernel and initrd lines and changing the location of the kernel image and ramdisk (see Figures 9-16 and 9-17).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_284_0.png)

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_284_1.png)

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_285_0.png)

5. When you have finished configuring the location of the kernel and initial ramdisk, click OK to return to the boot loader profile list.

6. If you are happy with the overall look of the profiles, press OK to return to the boot loader configuration window. You can see the entry we just created in the Available Sections part of the configuration list.

7. To save the configuration, press the Finish key. Your GRUB configuration will be saved and your entry will be available at next boot.

# Setting Up SCPM

SUSE Configuration and Profile Manager (SCPM) is a profile manager for the SUSE system. Profiles control what runs on the system and the configuration of your system. For example, if you use a laptop and need to switch between a DHCP client with a static IP address and no proxy at configuration in your office, you could configure this with SCPM and switch profiles when needed.

We will configure this same environment as a quick introduction to what can be achieved with SCPM. It is an extremely powerful component of the SUSE system that can profile any system configuration you can think of for future switching.

## 1. To start SCPM, select System -> Profile Manager.

When you start SCPM for the first time, it is likely that the system process is not running (is the default). You will need to start SCPM before you can continue with the addition and configuration of profiles (see Figure 9-18).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_286_0.png)

**Figure 9-18:** Starting SCPM

2. When SCPM starts, it creates a default profile (see Figure 9-19) based on your current system configuration. At the moment, the system has an IP address configured to use DHCP and a proxy setting (discussed earlier in the chapter). You will change the name of the profile to Work.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_286_1.png)

**Figure 9-19:** SCPM profiles

4. When your default profile has been created, you can edit its settings by selecting the default entry and clicking Edit. The screen in Figure 9-20 shows the default profile with its name changed to Work.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_287_0.png)

Figure 9-20: Editing the default profile

In this screen, you can set the new title and description for the profile using the boxes. You can also add scripts that are executed upon entry and exit of the profile. It is beyond the scope of the book to go into detail, but you can make powerful scripts to customize aspects of the system—for example, copying a specific configuration file for a service you need to control (that is not controlled by SUSE) or running an application that checks for security settings.

4. When your Work profile has been created, you need to create one for Home. To do this, use YaST's modules to change to a static IP address and remove your proxy settings.

We won't show you how to do this with YaST here, because we have discussed network configuration during the installation and discussed proxy configuration earlier in the chapter.

5. When you have configured your system to need it for another profile, you need to click the Add button to define a new profile. You will be prompted for how you want to add this profile (see Figure 9-21). Select The Current System Configuration. If you want to make this active profile, then select Make the Added Profile Active, but for this example, because we spend time at work than at home, we will leave this unselected.

Figure 9-21: Adding a new system profile

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_288_0.png)

6. When you have clicked OK, you are presented with the profile title and description screen before you need to configure the display information, this time for your Home profile.

7. When you are happy with the title and description, click OK to save it. YaST analyzes your current profile (as configured via YaST for network and proxy settings) and saves the profile.

8. YaST returns you to the profile list screen where you can switch between the profiles when needed.

9. Click the Close button to commit your changes to SCPM and return to YaST.

> It is not always pertinent to let YaST change your profile. To change your profile from the command line to the Home profile, enter `scpm switch Home`. SCPM analyzes your systems for changes that need to be.

# Runlevel Editor

Throughout the book, we have talked about enabling services at boot. This is a very important concept when dealing with Unix systems. A server would be useless if the server process did not start up. The Runlevel Editor can be used to turn on and off services at boot time.

The Runlevel Editor loads the current system configuration and then displays what services are enabled. You have two options to edit the runlevel, Simple and Expert mode:

- **Simple mode**: You can select the service and either enable or disable it. You do not have control over the specific runlevel it starts in because YaST enables the service in its default runlevel.
- **Expert mode**: Use Expert mode if you want to enable or disable a service in a specific runlevel.

In 9-22, for example, in Expert mode, we have selected the Postfix service. At the bottom of the screen you can see a description of the service (although the service description is long). Below the service description, you can set the levels that this is enabled in. We have runlevels 3 and 5 (networking and graphical, respectively).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_289_0.png)

9-22: Editing runlevels with YaST

When you are happy with the runlevel, then press the Finish button to continue.

Your runlevel configuration is now saved and will take effect when your next system boots up. You can always manually start Postfix or any other service with the `rc` script. For Postfix, you use `rc postfix`.

# Configuring DHCP

To load the configuration for both the DHCP server and the client, you need to edit different system settings. For the DHCP server, choose Network Services DHCP Server. For the DHCP client, you need to edit your network card configuration by selecting Network Devices Network Card.

We discuss DHCP client and server services in Chapters 1 and 20, so we will not go into detail here. Suffice to say, you can edit these settings using YaST.

# Users and Groups

As well editing users and groups directly, as described in Chapter 2, you can use YaST to edit these files in a more user-friendly fashion.

# Adding or Editing Users

To edit users, select Security and Users Edit and create users. You will be presented with a list of users currently in the system (see Figure 9-23).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_290_0.png)

Figure 9-23: Listing the current users on the system
