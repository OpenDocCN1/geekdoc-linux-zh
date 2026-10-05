# 2. Start chopping the clothes.

Use GIMP's Select rectangle to pick each piece, and choose Edit: Copy from the main menu. Don't worry if adjacent bits of graphics are also included at this stage. Then File: Create: From Clipboard to get that piece on its. Work on the image with a square paintbrush, remove any tabs and other bits of image until it sits in a white background. Next, use the Fuzzy Selection tool to select this white background. Choose Transparency: Add Alpha Channel from the main menu, and choose Edit: Clear. Finally, File: Export As to save as a .png file, using the default ticked options. Finally, close the image window and click the Discard options.

+   3. Repeat this process until the doll and all the accessories have been saved in separate .png files in a folder doll, which you have created inside your working RFID folder.

# 4. Rename the doll file to start with an ampersand.

This is important because the ampersand ensures that this file appears first in an alphabetically ordered list. We use this so that the program knows it's the doll.

Now it's time to enroll the RFID cards. We use two blocks here — one to hold the filename and the other to hold the position for drawing the file on screen. Now type and run the code in Listing 18-5.

If the graphics are put through a network or downloaded, some computers can place invisible files into folders that the program here might mistake for a graphics file and try to load. The Macintosh puts a file called .DS_Store and a folder called AppleDouble in every folder it sees. On an enroll program, this file will produce an error message saying unsupported image format. If this happens, use the File Manager to navigate to the folder, then go to the View menu and turn on the Show Hidden option. You can then delete this normally hidden file — the hidden does no harm.

![](bbox=[0.173, 0.546, 0.223, 0.616])

# Listing 18-5: Dress Up Doll Enroll

```
#!/usr/bin/python3
# Dress Up Enroll by Mike Count

from rc522rfid import Rc522rfid
import pygame
import os
```

402 PART 5 Exploring Electronics with the Raspberry Pi