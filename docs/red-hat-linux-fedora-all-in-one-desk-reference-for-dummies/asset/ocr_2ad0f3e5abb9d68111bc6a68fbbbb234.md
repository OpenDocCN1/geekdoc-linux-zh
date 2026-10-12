All the lines starting with the second T: line pertain to the Nikon Coolpix 2500 camera. You can see some of the details in the output, such as manufacturer name and camera model.

# 4. Mount the camera's storage media by typing the following command:

```
mount /mnt/camera
```

A camera icon appears on the GNOME desktop.

# 5. Double-click the camera icon on the GNOME desktop.

The camera's contents appear in a Nautilus file manager window. You can double-click the folders and find the one that contains the photos. Typically, these digital photos are JPEG files with cryptic filenames that carry the .jpg extension. In the default view, Nautilus displays thumbnails of the photos, so you don't have to worry about the cryptic file names. Figure 5-3 shows the GNOME desktop with the camera icon and the Nautilus window showing the photos from my Nikon Coolpix 2500.

# 6. Click to select photos and copy them to your hard disk.

You can also type the cp command in a terminal window to copy all or selected images to a directory on your hard disk. For example, to copy all JPEG photos from the camera to the current directory, type:

```
cp /mnt/camera/*.jpg .
```

Figure 5-3: You can access the digital photos in your digital camera as a USB mass storage device.

![](bbox=[0.22, 0.63, 0.9, 0.93])