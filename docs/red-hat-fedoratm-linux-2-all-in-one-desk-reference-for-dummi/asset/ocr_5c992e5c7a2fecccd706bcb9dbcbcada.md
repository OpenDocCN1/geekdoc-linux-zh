The service configuration utility shows the names of services in a scrolling list. Each line in the list shows the name of a service with a box in front of the name. A check mark in the box indicates that the service is already selected to start at boot time for the current run level. When the dialog box first appears, many services are already selected.

You can scroll up and down the list and click the box to select or deselect a service. If you click the box, the check mark alternately turns on and off. To find out more about a service, click the service name and a brief description appears in the right-hand side of the window. For example, Figure 1-2 shows the help text for the `atd` service. Additionally, the utility also shows you whether the selected service is currently running or not.

After you select all the servers you want to start when the system boots, click Save on the toolbar to save the changes. Then choose File*Quit to exit.

![](bbox=[0.15, 0.41, 0.23, 0.5])

By default, the service configuration utility configures the selected services for the current run level. That means if you’re selecting services from the graphical desktop, the system is in run level 5 and the services you configure are set to start at run level 5. If you want to set up the services for a different level, select that run level from the Edit Runlevel menu.

Table 1-1 shows a list of the services, along with a brief description of each one. The first column shows the name of the service, which is the same as the name of the program that has to run to provide the service. You may not see all these services listed when you run the service configuration utility on your system because the exact list of services depends on what is installed on your Fedora Core system.

| **Table 1-1** | **Some Common Services in Fedora Core** |
|---|---|
| **Service Name** | **Description** |
| `acpid` | Listens to Advanced Configuration and Power Interface (ACPI) events from the kernel and notifies other programs when such events occur. ACPI events can occur when the kernel puts the computer into a low-power state (for example, standby mode) to save energy. |
| `aep1000` | Loads and unloads the driver for the Accelerated Encryption Processing card called the AEP1000, which can do encryption fast (use this service only if you have the card installed in your system). |
| `anacron` | Executes commands scheduled to run periodically. |
| `apmd` | Monitors the Advanced Power Management (APM) BIOS and logs the status of electric power (AC or battery backup). |
| `atd` | Runs commands scheduled by the `at` and `cron` commands. |