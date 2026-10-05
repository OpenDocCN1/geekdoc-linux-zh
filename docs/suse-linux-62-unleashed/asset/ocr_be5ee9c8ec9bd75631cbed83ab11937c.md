# SuSE System Administration
PART III

```
if [string match "/dev/hd**" $device] {
  exit 0
}
if [string match "/dev/sd**" $device] {
  exit 0
}
```

FIGURE 20.4
To configure a new backup device for BRU-2000, select the Devices tab in its Configuration dialog box.

![](bbox=[0.31355, 0.25355, 0.76642, 0.49355])

Select the Devices tab and then select the New button. A New Device window appears, as shown in Figure 20.5. Type in the name of your Zip disk's device (for example, /dev/sda4), select the device type as OTHER, and click the Create button. You can then type in a description of your Zip drive in the Device Name field and set the size of the device as 95MB. Click the Save button, followed by the Exit button.

FIGURE 20.5
The New Device dialog box is used to select a new backup device or create a new one for BRU-2000.

![](bbox=[0.31355, 0.66355, 0.76642, 0.8735499999999999])