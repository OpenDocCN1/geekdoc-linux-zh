# Chapter 9 ♦ Configuring the System with YaST 245

The Runlevel Editor loads the current system configuration for the services and then displays what services are currently enabled. You have two options to edit the runlevel configuration, Simple and Expert mode:

+   - **Simple mode** — You can select the service and either enable or disable it. You do not have control over the specific runlevel it starts in because YaST enables the service in its default runlevel.
- **Expert mode** Use Expert mode if you want to enable or disable a service in a specific runlevel.

In 9-22, for example, in Expert mode, we have selected the Postfix service. At the bottom of the screen you can see a description of the service (although the Postfix service's description is rather nondes). Below the service description, you can set the levels that this process is enabled in. We have runlevels 3 and 5 (networking and networking with X, respectively).

![](bbox=[0.2165, 0.403, 0.716, 0.733])

9-22: Editing runlevels with YaST

When you are happy with the runlevel editing, then press the Finish button to continue.

Your runlevel configuration is now saved and will take when your next system boots up. You can always manually start Postfix or any other service with the `rc` script. For Postfix, you use `rc postfix`.

Runlevels are discovered in more detail in Chapter 4.