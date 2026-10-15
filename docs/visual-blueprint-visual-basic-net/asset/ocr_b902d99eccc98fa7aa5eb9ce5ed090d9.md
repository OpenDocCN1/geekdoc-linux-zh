# ADD A PICTURE TO A FORM

Many Windows applications use pictures to make a window more attractive and easier to understand. You can add a picture to a Windows Form with the PictureBox control.

The PictureBox control appears in the Windows Forms section of the Toolbox. After adding it to the form, you can assign a single picture file to its Image property. Use the SizeMode property to determine how the control draws the image. Normal makes the PictureBox draw the image in its actual size at the top, left corner of the control. For SizeMode equal to StretchImage, the control stretches the image to fill the entire control space. AutoSize makes the control size to the actual image size. When you set SizeMode to AutoSize, you can no longer resize the control. CenterImage draws the image at actual size in the center of the control.

The PictureBox control also allows you to place a border around the edge. Set BorderStyle to FixedSingle to draw a one-pixel black border. Use Fixed3D to draw a more traditional 3D sunken border around the control. None removes the borders completely. You can also load another image into the control using the standard control property BackgroundImage. Because VB.NET does not allow you to align the foreground image like many other controls, you may not find this property useful. You can use BackgroundImage to draw a frame around an image with SizeMode set to CenterImage.

You can use standard control events with the PictureBox, like Click, MouseDown, MouseMove, and others to respond to actions of the user. Use the Paint event to draw onto the control. If you need to create an interactive picture control, a Button control allows you to use an image and provide interactive cues. For more information on the Button control, see Chapter 3.

# ADD A PICTURE TO A FORM

![](bbox=[0.06, 0.62, 0.48, 0.78])

![](bbox=[0.52, 0.62, 0.94, 0.78])

+   1. Create a new Windows Application project or open an existing project and create or open the form to load onto the control.

+   2. In the Toolbox, click the PictureBox control.

+   3. Drag the control to the form.

+   4. Edit any necessary properties.

+   5. In the Properties Window, click the Image property.

+   6. Click the link button.

Note: See Chapter 3 to edit properties.