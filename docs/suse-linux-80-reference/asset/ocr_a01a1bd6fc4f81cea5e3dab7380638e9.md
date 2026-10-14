A good indication of a programmable clock chip (and the problems this might entail) is the multiple zeros or repeating timing values. Absolutely, under no circumstances, ever write such values to `XF86Config`.

To configure clock chips, follow these steps:

+   - The best way is to enter an existing *(programmable)* clock chip if there is one. It will be programmed according to your `XF86Config` and will not contain clock lines. Compare chips on the card with the chips offered in the menu. Most newer S3 cards have a programmable clock chip.
+   
+   - If you do not have a programmable clock chip, you should launch X-probeonly and compare these values with those in the manual. If these values correspond (±2), enter them in `XF86Config`.
+   
+     Unless the manual offers some pertinent advice, the values are determined by running X-probeonly (this works best on an unloaded machine). Check whether the values are accurate, since clock values cannot be determined for every card. (Many zeros or repeating values are a sign of invalid settings.) Enter the correct values into `XF86Config`. Do not omit any values. Do not try to rearrange them or change them in any way. The values have to be entered in their exact order.
+   
+     If the P9000 server is used, the order is irrelevant; just enter the modes for the desired clock in the *clocks line*.
+   
+   - In general: if there is a programmable clock chip, there should be no clocks line in `XF86Config` (exception, P9000). For cards without a programmable clock chip, there should be a clocks line in `XF86Config`. This avoids tedious (and sometimes even risky) clock probe at each start. Furthermore, for cards with unreadable values, there are no invalid values and there is no risk to your monitor.

After having read the previous section, if you want to let clocks be recognized automatically, just answer ‘y’ to the following question:

> Do you want me to run “X -probeonly” now?

Now the screen will turn black before the list of probed clocks appears or a message will appear that no clocks could be found. If you have selected a clock chip, this question will not appear, since the clocks will then be programmed automatically. If this is the case, this section will be skipped.

> **Caution**
> 
> If the previous question has been answered with ‘y’ and the screen remains black for more than 30 seconds, cancel testing immediately with `Ctrl` + `Alt` + `F1`, or `Ctrl` + `C`. If this does not work, switch off the monitor and the computer to prevent damage to your hardware.