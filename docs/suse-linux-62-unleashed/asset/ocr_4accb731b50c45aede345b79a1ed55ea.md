# Printing with SuSE Linux
CHAPTER 24

# FIGURE 24.10
Choose the REMOTE menu to launch a remote printer configuration.

![](bbox=[0.205, 0.085, 0.815, 0.235])

# FIGURE 24.11
ter a hostname of the remote printer.

![](bbox=[0.205, 0.265, 0.815, 0.365])

# FIGURE 24.12
Enter the name of the remote printer.

![](bbox=[0.205, 0.425, 0.815, 0.525])

Enter the name of the remote printer. This name should be defined in the remote computer's /etc/printcap. Press OK after typing in the name. You'll see the dialog shown in Figure 24.13.

# FIGURE 24.13
Save your remote printer definition.

![](bbox=[0.205, 0.655, 0.815, 0.805])

This dialog is used to save your remote printer definition. Scroll down to the Add menu item and press Enter. The SETUP command should report that a remote printer entry has been created. In /etc/printcap:

```
### BEGIN apfsler: ### remote printer aptiva ip ###
# Warning: Configured for apfsler, do not edit the labels!
```

24
Printing with SuSE Linux