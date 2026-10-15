+   2. Open the configuration file of the ethernet adapter with a text editor:
+   
+   hwcfg-bus-pci-0000:<network_adapter_pci_id>

+   3. From the MODULE option in the configuration file, note the name of the kernel driver module below this step .

--------------------------------------------------------------------------------

+   4. Enter the command lsmod | grep <module_name>. As you can see, the module is still loaded.

+   5. Unload the module with the command rmmod <module_name>

+   6. Verify with lsmod | grep <module_name>, that the module is not loaded anymore.

# Part III: Load the Driver Module with a modalias

+   1. Change into the directory /sys/bus/pci/devices/.

+   2. Change into the directory 0000:network_adapter_pci_id

+   3. Enter cat modaliases to display the modaliases of the ethernet adapter.

+   4. Enter the command modprobe <modalias>. Use copy and paste to enter the modalias from the cat output to enter the modalias.

+   5. Verify with lsmod | grep <module_name>, that modprobe has detected and loaded the driver for the network adapter.

+   6. Enter the command ip a, and verify that the network interface is available again.

+   7. Reboot your system, to restore all network settings.

(End of Exercise)