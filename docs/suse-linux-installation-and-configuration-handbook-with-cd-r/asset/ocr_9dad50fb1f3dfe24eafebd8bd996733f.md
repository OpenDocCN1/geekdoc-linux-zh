+   - I/O port = 220 as in line
+   - I/O port midi= 330 as in line
+   - I/O MPU port= 388 as in line

**TIP** You'll find all the possible combinations of configurations that your sound card can take in the file `/etc/isapnp.conf`. You can comment out all the configurations, and then pick up a different one that has different resources and uncomment the lines that specify the correct configuration that you want your card to be set up to.

When you're done, issue the `isapnp` command again and check for the output message. Try different configurations until you get no error messages. If you still get warning messages, check the conflicts using the following commands:

+   - To check on IRQ conflicts, enter the following:
+     `bash#cat /proc/interrupts`
+   - To check on DMA conflicts, enter the following:
+     `bash#cat /proc/dma`
+   - To check on I/O ports conflicts, enter the following:
+     `bash#cat /proc/ioports`

Notice that `isapnp` can generate an error when trying to assign the interrupt to its owner if its owner already has it. In other words, suppose that the card is already set up to use IRQ 5. If you run `isapnp` again, it will generate an error because IRQ 5 is already taken. Reboot and check the `isapnp` output at system start up; if all goes smoothly, your system is fine. If you get any fatal error conflicts, you should do one of the following:

+   - If you are absolutely sure that the error mentioned is not fatal, then edit the `isapnp.conf` file and modify the conflict line from
+     `(CONFLICT (IO FATAL) (IRQ FATAL) (DMA FATAL) (MEM FATAL))`
+     to
+     `(CONFLICT (IRQ WARNING) (DMA WARNING) (MEM WARNING))`
+     In this example, you force `isapnp` to generate a warning message instead of a fatal error message. You also force it not to complain at all for I/O conflicts.
+   - If there are conflicts you want to get rid of, then edit the `isapnp.conf` file and pick up a different configuration.