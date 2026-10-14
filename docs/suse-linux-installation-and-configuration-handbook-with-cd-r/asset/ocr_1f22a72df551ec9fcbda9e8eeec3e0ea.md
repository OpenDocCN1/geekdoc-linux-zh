+   - **IO Port**—The same I/O port that you set in your `/etc/isapnp.conf`. Check the line in your `isapnp.conf` that represents `(IO 0 (BASE 0x0220))`, which indicates a value of 220.
+   - **MPU IO Port**—The MPU IO port of your sound card. You can get this by checking the line in your `isapnp.conf` that represents `(IO 1 (BASE 0x0330))`, which indicates the value 330. If your sound card does not support MPU, use -1.
+   - **IRQ**—The IRQ of your sound card. Check the line in your `isapnp.conf` that represents `(INT 0 (IRQ 5 (MODE +E)))`, which indicates a value of 5.
+   - **8-Bit DMA**—In DOS and Windows it is called *low DMA*. Check the line in your `isapnp.conf` that represents `(DMA 0 (CHANNEL 1))`, which indicates the value 1.
+   - **Max 8-Bit DMA size in KB**—You should get this from your sound card manual if you don't have a PnP sound card. If you have a PnP sound card, check your `/etc/isapnp.conf` file. If you don't find this piece of information in the manual or the `/etc/isapnp.conf`, try a value in between the range given to you and use the trial and error technique.
+   - **16-Bit DMA**—In DOS and Windows it is referred to as *high DMA*. Check the line in your `isapnp.conf` that represents `(DMA 1 (CHANNEL 5))`, which indicates the value 5.
+   - **Max 16-Bit DMA**—Use the same steps as Max 8-Bit DMA Size in KB.
+   - **Mic Auto Gain Control**—Enable this if you want microphone gain control.

Pressing Enter takes you back to the main screen (see Figure 10.6). If you are finished setting up all your system's sound cards, choose no more sound cards. You will be asked if you'd like to modify your `/etc/modules.conf`. Answer Yes. The configuration is saved and you're done with the first step. Finally, start the ALSA driver by issuing the following command:

```
#/sbin/init.d/alsasound start
```

# FIGURE 10.6

You can set up more sound cards and non-PnP sound cards directly from the alsaconf script menu.

![](bbox=[0.3, 0.78, 0.85, 0.98])