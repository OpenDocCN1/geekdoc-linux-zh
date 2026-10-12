Buttons <number> This specifies the number of buttons on the mouse. This entry must immediately follow the Mouse entry in the Xconfig file.

Card <string> This designates the model of the graphics card in use. This is only used by configX.

Chipset <string> This displays the chipset used by the server. Normally configX inserts the correct chipset into the Xconfig file.

Clocks <number> [/<number>...] This contains a list of numbers specifying the frequencies associated with the clock generator on the card. The numbers are specified in MHz.

Depth <number> This references the color depth of the screen, which controls how many colors can be displayed. Different cards and drivers support different depth values: 4, 8, 16, 24, or 32. Depth 4 supports 16 colors and depth 32 supports 16 million colors.

Dimensions <width> <height> This keyword represents the dimensions of the screen in millimeters, which is passed to X clients upon request.

DPMSoffDelay <number> This controls the number of seconds after the last user input before the screen enters DPMS off mode. Off mode provides maximum power reduction. To activate this mode, the X server disables both the horizontal and vertical sync signals to the monitor.

DPMSstandbyDelay <number> This controls the number of seconds after the last user input before the screen enters DPMS standby mode. Standby mode provides minimal power reduction. To activate this mode, the X server disables the horizontal sync signal to the monitor.

DPMSsuspendDelay <number> This controls the number of seconds after the last user input before the screen enters DPMS suspend mode. Suspend mode provides significant power reduction. To activate this mode, the X server disables the vertical sync signal to the monitor.

Driver <string> This references the name of the driver, which usually corresponds to the name of the X server. For example:

```
Driver 8514
```

initiates the section for defining the 8514 driver.

Emulate3Buttons This entry is used when a two-button mouse is emulating a three-button mouse. This entry must immediately follow the Mouse entry