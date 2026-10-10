![](bbox=[0.17, 0.09, 0.62, 0.53])

Figure 5-5: Set up your Windows applications in Linux from the Wine configuration window.

# **Assigning drive letters**

Before you begin installing Windows applications in WINE, you should become familiar with your WINE environment. Drive letters are assigned in the `$HOME/.wine/dosdevices` directory. Select the Drives tab on the Wine configuration window to see which drive letters are assigned. At least drive C: and drive Z: should be set.

To configure additional drive letters, you can select Add (to add an individual drive) or select Autodetect (to have WINE assign all your partitions to drive letters) in the Windows configuration window.

Within the `$HOME/.wine/drive_c` directory (that is, your C: drive), you should see some things that are familiar to you if you are coming from an older Windows environment: `Program Files` and `windows` directories.