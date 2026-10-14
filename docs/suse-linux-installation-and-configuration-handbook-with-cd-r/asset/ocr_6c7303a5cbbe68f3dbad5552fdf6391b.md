Next, from the menu choose System Administration, Kernel and Boot Configuration, LILO Configuration. Or, to go directly to the LILO configuration, you can run YaST like this:

```
root@linux:~> yast --mask lilo
```

Now you are ready to configure LILO (see Figure 8.9). Follow these steps:

FIGURE 8.9
LILO is very easy to configure using YaST.

![](bbox=[0.3, 0.24, 0.75, 0.52])

+   1. The first thing you need to do is create a new configuration for your test kernel. Press F4.
+   2. For the configuration name, enter test and press Tab to move on to the next field.
+   3. Choose Boot Linux for the Which Operating System option. YaST then should automatically fill in the (Root) Partition to Boot option with the correct partition; just check it to make sure.
+   4. As for the Kernel to be Booted by LILO Option, press F3 to get a file selection box.
+   5. Browse over to /usr/src/linux/arch/i386/boot/ and choose bzImage (see Figure 8.10).

FIGURE 8.10
Select the kernel to boot.

![](bbox=[0.3, 0.77, 0.75, 0.93])

+   6. Save and exit.
+   7. You should now have a new entry called test. Press Enter to save the LILO configuration and exit.