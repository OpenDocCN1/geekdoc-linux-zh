# Extra

# WORK WITH CONTROLS

You can specify a transparency color for the images in the control. The default setting for the TransparentColor property is Transparent, meaning it reads the transparency color from the image file, if the file type supports transparency. Icon files (ICO) and Graphics Interchange format (GIF) support transparency. If you load a collection of Windows bitmap (BMP) files into the ImageList control, set the TransparentColor to the appropriate background color of the images.

You can add images to the ImageList control at run-time using the Add method of the Images collection. Supply an Image object as the only parameter to the method.

```
**Example:**

```vb
' Visual Basic
' Replace string with valid image file path:
Dim myImage As System.Drawing.Image = _
    Image.FromFile("C:\sample.gif")
ImageList1.Images.Add(myImage)
```
```

![](bbox=[0.072, 0.514, 0.944, 0.802])

+   8. Add a control to display an image.
+   
+   - Controls such as the Button and Label control offer support for loading images from the ImageList control. The example adds a Button control.

+   9. In the Properties window, click the ImageList property and select the ImageList control.
+   
+   - You can clear the Text property to make the button appear with only an image.

+   10. Click the ImageIndex and select an image to display.

The ImageList provides the image to the control.