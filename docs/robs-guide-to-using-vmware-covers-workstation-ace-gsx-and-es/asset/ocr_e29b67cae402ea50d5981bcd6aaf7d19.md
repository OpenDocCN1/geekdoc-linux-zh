# 4.6 Setting the Power On and Power Off Modes

First time users have to get used to seeing the virtual machine as a real PC which can do everything you normally can do with a PC, including powering on and off. VMware virtual machines can even be configured to look more like real PCs. Nowadays, pressing the power off button of a PC does not just power off but also shuts down the operating system. VMware can also do that.

To configure this option, open the Virtual Machine Settings and on the Options tab, select the Power entry. The following settings, displayed in Figure 4.2, are available:

+   - Power off button: Power off or Shut Down Guest
+   - Restart button: Reset or Restart Guest

![](bbox=[0.05, 0.46, 0.9, 0.85])

Figure 4.2: The machine can be powered off but a graceful guest OS shutdown can also be configured with the Virtual Machine Setting Power Options.

Note: The behavior of these settings depends on the guest OS that you are using. The Power Off setting always turns the virtual machine off, but the Shut Down Guest setting sends a signal to the guest operating system to perform a shutdown. If your guest OS does not support this feature, then you must manually stop the guest