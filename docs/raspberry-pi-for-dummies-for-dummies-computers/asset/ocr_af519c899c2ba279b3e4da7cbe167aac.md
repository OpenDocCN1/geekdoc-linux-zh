# Troubleshooting screen display issues

The Raspberry PI can be used with a wide variety of TVs and monitors, that wide compatibility means you might need to tinker with the settings to get your PI working with your choice of display. The computer should automatically adjust its output to the screen, but there might be times when you want to fine-tune its settings, override its defaults, or force your preference.

If you're experiencing difficulties getting a consistent and clear image, try adjusting one or more of the settings in Table A-1.

Table A-1 Troubleshooting Screen Display Issues

| Symptom or Issue | Setting to Change | Values to Use |
| --- | --- | --- |
| Image spills off left of screen. | overscan_left | Overscan is a feature that changes the size of the image to fill the screen. The overscan settings are all set using pixels, the smallest dots display recognizes. For example, overscan_left=0 |
| Image spills off right of screen. | overscan_right | The overscan is using pixels. For example, overscan_right=50. |
| Image spills off top of screen. | overscan_top | The overscan is using pixels. For example, overscan_top=50. |
| Image spills off bottom of screen. | overscan_bottom | The overscan is using pixels. For example, overscan_bottom=50. |
| Image has a black border around it. | disable_overscan | Use a value of 1 to disable overscan, like this: disable_overscan=1. |

You can use negative numbers over overscan_left, and other options above to adjust the border on each side.

See "Adjusting the screen display," later in this appendix.

Text or other content is too small. | framebuffer_width / framebuffer_height | See "Adjusting the screen display," later in this appendix.

Text or other content is too big. | framebuffer_width / framebuffer_height | See "Adjusting the screen display," later in this appendix.

Picture fails when using an analog TV. | stv_mode | The composite video output is NTSC by default, which is used in North America. You may need to change this setting for use in other regions. Valid values are 0 for NTSC, 1 for NTSC-j for Japan, 2 for PAL-M (used in the U.K. and most of Europe), or 3 for PAL-M (used in Brazil). For example, sdt_mode=2.

452 Raspberry Pi For Dummies