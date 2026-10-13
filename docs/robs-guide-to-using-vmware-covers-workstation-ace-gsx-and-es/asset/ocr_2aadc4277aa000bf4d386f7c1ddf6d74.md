Something else to keep in mind when running a virtual machine, as a user that is logged in to Windows, is that the virtual machine will be powered off when you close the session. You will receive a warning message like the one displayed in Figure 35.9.

![](bbox=[0.07, 0.2, 0.85, 0.48])

Figure 35.9: Starting a virtual machine as the current user will power off the machine when you log off.

For virtual machines that always need to be available, you need to configure them to run under the local system account. Figure 35.10 shows an example of three virtual machines that run under the system account. You can check this yourself for running virtual machines with the Task Manager on your environment.

![](bbox=[0.05, 0.77, 0.7, 0.92])

Figure 35.10: Virtual machines running under the system account.