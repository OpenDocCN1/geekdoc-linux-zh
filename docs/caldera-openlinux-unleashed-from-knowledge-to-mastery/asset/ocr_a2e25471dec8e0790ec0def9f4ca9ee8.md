![](bbox=[0.3, 0.1, 0.42, 0.23])

**FIGURE 27.11**
The Commands window just after choosing Region of Interest... in the Image Edit menu and before selecting a region. Note that the title has changed to ROI for Region Of Interest.

![](bbox=[0.3, 0.35, 0.42, 0.62])

**FIGURE 27.12**
The Commands window after selecting a region of the image. Note that the title has changed to Apply, indicating that the selected actions will be applied to the selected region.

Just about anything you can do with xv, you can do with display. display also has some other nice features, however. It has more filters or algorithms than xv does, and it also enables you to draw on the image (in the same ways that convert can draw on an image), place text in the image, and combine images in the same ways as combine. For more information, check the display man page (man display). The online documentation (obtained by clicking the Help button) is also very good.

# identify

identify describes the format and other attributes of one or more image files. It will report a number of facts, including the scene number, the filename, the dimensions in pixels of the image, whether the image has a colormap, the number of colors in the image, the size of the image in bytes, the image format used (GIF, JPEG, and so on), and the number of seconds it took to process the image. identify is purely a command-line tool and has the following syntax: