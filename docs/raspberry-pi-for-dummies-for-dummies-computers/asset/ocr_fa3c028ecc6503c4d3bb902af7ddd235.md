| Symptom or Issue | Setting to Change | Values to Use |


| Picture is stretched or squashed on TV. Aspect ratio looks wrong. | sdtv_aspect | The aspect ratio of the image is the ratio between the width and height of the image. There are three valid values for this setting: 1 (for the aspect ratio 4:3), 2 (for the aspect ratio 14:9), and 3 (for the aspect ratio 16:9). Usage example: sdtv_aspect=2.

| HDMI screen is blank. | hdmi_force_hotplug | If the Raspberry Pi can't detect a HDMI monitor, you can force it out through the HDMI connector by setting this value to 1, like: hdmi_force_hotplug=1.|

| DVI monitor is snowy or blown out. | hdmi_drive | This setting adjusts the output of the HDMI port. If you're using a DVI monitor, try a value of 1. If you're using an HDMI monitor, use a value of 2. Example: hdmi_drive=1.|

| No audio through computer monitor. | hdmi_drive | Use value of 2 for HDMI mode and define how audio down the HDMI cable, like: hdmi_drive=2.|

| Picture blanks, interference, or is missing. | config_hdmi_boost | Typical ranges from 1 to 7 and define how much power is output through the HDMI port. Increasing the value progressively. The HDMI safe mode uses a value of 4 for this setting. If you're using a long cable, you can use the maximum value of 11, avoid using high values unless strictly required. Usage example:config_hdmi_boost=4.|

| Any problems using HDMI monitor. | hdmi_safe | If you experience problems using an HDMI monitor, try using Safe Mode. Set hdmi_force_hotplug to 0 to force output to the HDMI port, set config_hdmi_boost to 4 to boost the power, and set the hdmi_mode and hdmi_group settings to a generally safe combination. These settings are used to override the HDMI screen resolution. For more details on the settings, use http://elinux.org/RPI_config.txt. To enable HDMI Safe mode, use: hdmi_safe=1.|

![](bbox=[0.175, 0.715, 0.235, 0.765])

You can change multiple settings at the same time, but each setting must be on its line. Most of these settings have text you can edit in config.txt already, don't forget to remember the # symbol.

![](bbox=[0.175, 0.785, 0.235, 0.835])

We're assuming here that the screen is plugged in, switched on, and tuned correctly. Before changing configuration settings, it's always a good idea to double-check that.

# APPENDIX A Troubleshooting and Configuring the Raspberry Pi 453