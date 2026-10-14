"Device.kdelnk" with a name to represent your floppy drive, such as "Floppy.kdelnk." A new icon will appear on your desktop; the icon will be a question mark to indicate that the new device is not yet configured.

To configure the device, right-click on the icon and select Properties from the popup menu. This will cause KFM to display its window for configuring .kdelnk files. Select the Device tab at the top of the window to display options pertaining to mounting. In the box labeled Device, type /dev/fd0, but don’t press Enter yet. Don’t enter anything into the Mount Point or Filesystems boxes.

![](bbox=[0.22, 0.29, 0.35, 0.44])

The new device icon must be configured before it will work. Since it hasn’t been configured yet, it appears as a question mark.

![](bbox=[0.22, 0.55, 0.35, 0.7])

KFM uses a special window to configure .kdelnk files.

To configure a device icon:

+   - Select the Device tab at the top of the window.
+   - Enter the device filename in the Device box.
+   - Select an icon for the device while mounted.
+   - Select an icon for the device while not mounted.

You need to select two new icons for the device: one which will show when your floppy drive is mounted and another which will show when it is not. To select the icons, click on the button labeled Mounted Icon. Choose the icon that looks like a floppy disk with a little green light next to it, and click Ok. Now, click on the button labeled Unmounted Icon. This time, choose the icon which looks like a floppy disk without a little green light next to it, and click OK. Now, click the OK button at the bottom of the KFM window to accept your changes. On your desktop, you should see an icon that looks like a floppy disk.

![](bbox=[0.22, 0.82, 0.38, 0.95])

Select Icon window. When you click on a button to select icons, KDE presents you with a panel where you can select an icon to represent your device. Typically there will be two icons per type. Icons with a green square next to them represent active devices. If you assign the pair, KDE will change the icon to provide visual feedback on mounted devices.