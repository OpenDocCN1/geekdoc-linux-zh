# Extra

When you load an image into a PictureBox control, it saves the image into the executable, which can balloon in size unnecessarily in an application where a variety of forms may include the same image. To prevent this, you can use a resource file to store only a single copy of the file in the executable. You can then load the appropriate resource image into the PictureBox control in the Form_Load procedure. The ResourceManager class contains the necessary functions to access a resource file. For more information on creating a resource file and loading resources into it, search Visual Basic .NET help for Resource Editors. Once you connect to a resource file, use a line similar to the one below to read the image out and load it into a PictureBox.

# Example:

```
PictureBox1.Image = CType(ResourceManager.GetObject("flag"), System.Drawing.Image)
```

The PictureBox control accepts drawing commands like the Form and many other controls. This means the tasks later in the chapter explaining the Graphics object work using a PictureBox as well. Just place the code from a Form_Paint routine into a PictureBox_Paint routine. The PictureBox contains all the same drawing methods and properties.

![](bbox=[0.06, 0.56, 0.48, 0.78])

![](bbox=[0.52, 0.56, 0.94, 0.78])

+   The Open dialog box appears.

+   7 Click an image file from disk.

+   8 Click Open to load the image into the control.

+   The example sets SizeMode to CenterImage.

+   9 Press F5 to run the project.

+   The PictureBox control displays the picture file appropriately.