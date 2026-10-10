![](bbox=[0.23, 0.11, 0.84, 0.43])

Figure 25-4: Begin the installation process for the guest system (here Ubuntu) you choose to install.

Follow the installation procedure for the operating system you selected. I chose the Install Ubuntu selection. Then I followed along with the Ubuntu installation guide to complete the installation. Use installation instructions for whatever operating system distribution you are installing.

12. Shut down or reboot the guest. Once the installation is complete, you can shut down or reboot the guest system as instructed. After that, you can use the Virtual Machine Manager or the virsh command to manage your virtual guest.

# Managing Virtual Guest Systems

After you have installed a guest system, you can manage it through the same interface you used to create it: the Virtual Machine Manager window. Here are some of the things you can do from the Virtual Machine Manager window:

+   * **Start the guest** — Right-click on the guest you want to start and select Run. The guest boots up and displays in a window on your desktop.
+   * **Stop the guest** — Right-click on the guest you want to stop and select Shut Down → . If the guest doesn't stop or if you are in a hurry, you can select Force Off instead, which effectively pulls the plug on the guest.
+   * **Reboot the guest** — Right-click on the guest you want to restart and select Shut Down → Reboot. The guest shuts down and boots back up as you watch it from your desktop.