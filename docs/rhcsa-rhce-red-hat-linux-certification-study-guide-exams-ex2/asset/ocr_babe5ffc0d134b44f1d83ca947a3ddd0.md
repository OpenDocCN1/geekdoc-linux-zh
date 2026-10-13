# FIGURE 5-9

Service
management with
ntsysv

![](bbox=[0.28, 0.18, 0.8, 0.6])

After the noted changes were made, the S50bluetooth file was replaced with the following:

```
K83bluetooth
```

# The GUI Service Configuration Tool

The Service Configuration tool shown in Figure 5-10 allows you to select the services that are to be activated in runlevels 2 through 5. One way to start it is from a command line in the GUI with the system-config-services command. The options are fairly self-explanatory. Click Customize for a list of runlevels affected by any changes made through this tool<=>.

> exam Watch
> When you configure or repair a service, use chkconfig (or a related utility such as ntsysv or system-config-services) to make sure that the service is activated at the appropriate runlevels. Otherwise, you may not get full credit for your work.