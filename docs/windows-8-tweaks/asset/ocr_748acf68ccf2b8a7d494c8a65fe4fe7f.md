is very safe because you don't need to alter your Windows 7 partition or install. When you are finished, the Windows 8 drive will be virtualized into a single file on your Windows 7 partition and will show up in the boot menu just as if it was installed on raw disk.

# Creating the VHD File on Windows 7

The first step to dual-booting Windows 8 and Windows 7 is to create the VHD file to hold the Windows 8 installation. Open up Disk Management on Windows 7 to create the file:

+   1. Click the Start button in Windows 7, type in **diskmgmt.msc**, and hit Enter. The Disk Management utility should load.

+   2. Click the **Action** menu and select **Create VHD**.

+   3. Enter a location, such as `C:\VHD\Win8.vhd`. Set the size—I suggest 40 GB—and select the Dynamically expanding format to save your disk space. Dynamic VHD files start out small and only grow with data written to the virtual disk. When your screen looks like Figure 2-10, click OK and the file is created.

![](bbox=[0.18, 0.51, 0.83, 0.94])