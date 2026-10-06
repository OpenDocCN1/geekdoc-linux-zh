4. When your default profile has been created, you can edit its settings by selecting the default entry and clicking Edit. The screen in Figure 9-20 shows the default profile with its name changed to Work.

![](bbox=[0.214, 0.206, 0.725, 0.513])

Figure 9-20: Editing the default profile

In this screen, you can set the new title and description for the profile using the boxes. You can also add scripts that are executed upon entry and exit of the profile. It is beyond the scope of the book to go into detail, but you can make powerful scripts to customize aspects of the system—for example, copying a specific configuration file for a service you need to control (that is not controlled by SUSE) or running an application that checks for security settings.

4. When your Work profile has been created, you need to create one for Home. To do this, use YaST's modules to change to a static IP address and remove your proxy settings.

We won't show you how to do this with YaST here, because we have discussed network configuration during the installation and discussed proxy configuration earlier in the chapter.

5. When you have configured your system to need it for another profile, you need to click the Add button to define a new profile. You will be prompted for how you want to add this profile (see Figure 9-21). Select The Current System Configuration. If you want to make this active profile, then select Make the Added Profile Active, but for this example, because we spend time at work than at home, we will leave this unselected.