+   3. Read the license when the WinPac2 Setup: License Agreement window opens.
+   4. Click the I agree button.
+   
+   The WinPac 2 Setup: Installation Options window opens and shows the typical installation options.
+   
+   5. Click the Next> button.
+   
+   The WinPac 2 Setup: Installation Direction dialog box opens.
+   
+   6. Click the Install button.
+   
+   The WinPac 2 Setup: Completed window shows that the installation is complete.
+   
+   7. Click the Close button.

![](bbox=[0.05, 0.36, 0.13, 0.45])

The `C:\` symbol is an alias for the `/.wine/c` directory in your home directory. If your home directory is `/home/gabe`, for example, `C:` corresponds to `/home/gabe/.wine/c`.

You have several ways to start a Wine-based application:

☑ **Manually, by using a terminal emulator**: Open a terminal emulator window in the usual way and enter this command:

`wine "C:\Program Files\WinPac 2\WinPac2.exe"`

☑ **By using the GNOME Run utility**: Open the GNOME Run utility and enter this command:

`wine "C:\Program Files\WinPac 2\WinPac2.exe"`

☑ **By creating and clicking a GNOME icon**: This method is described in the set of steps immediately following. If you want to make the game easier to use (and who needs extra work?), create a GNOME icon. These steps describe the process:

+   1. Right-click anywhere on the **GNOME Panel** and choose **Add to Panel** > Launcher.
+   
+   The Create Launcher window opens.
+   
+   2. Enter **WinPac2** in the **Name** text box and enter this command in the **Command** text box:
+   
+   `wine "C:\Program Files\WinPac 2\WinPac2.exe"`
+   
+   3. Click the **Icon** button and select an image from the **Browse icons** windows that opens.
+   
+   For example, select the **Apple** icon.
+   
+   4. Click the **OK** button and the icon is created on the **Panel**.
+   
+   5. Click the new **WinPac2** icon and the game starts, as shown in Figure 14-1.