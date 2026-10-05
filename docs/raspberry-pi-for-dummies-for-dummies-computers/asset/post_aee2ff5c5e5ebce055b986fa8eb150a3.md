
Chromium, hover over Bookmarks, and select Show Bookmarks Bar from the options that appear. There's a keyboard shortcut: Ctrl-Shift-B.

To add the bookmark, you click the Finished button. (See Figure 4–10.)

Figure 4-10: Adding a bookmark in Chromium.

![](img/df9a01bf057d58c2401b5edabd6e8829_92_0.png)

To access your bookmarks while you're browsing, click the Menu button in the top right (refer Figure 4–9) and choose Bookmarks. The bookmarks on Bookmarks bar are shown on this menu. This opens, and others can be found by hovering over Other Bookmarks on this menu. You can visit a website on the Bookmarks by displaying the bar (Ctrl-Shift-B) and clicking its entry on the bar, and there is easy access to your other bookmarks on the right of this bar, in the Other Bookmarks folder.

To manage your bookmarks, go to the Bookmarks manager with Ctrl-Shift-O. Hover over a bookmark, and click the menu button on the right of it to see options to edit or delete the bookmark.

If you sign in Google while using Chromium on your Raspberry Pi, you can synchronize your bookmarks across your different devices.

One of the best Chromium features is the ability to save all open pages into bookmarks, in their order. It's handy if you're doing some research in different tabs to be able to store all the pages you're looking at in one place. To do this, open the Chromium menu, hover over Bookmarks, and select Bookmark Open Pages from the menu that appears. You can enter a new name for the folder, and then click Save.

![](img/df9a01bf057d58c2401b5edabd6e8829_92_1.png)

## Protecting your privacy

As you know, browsers store the history of web pages you visit. If you want to make a visit to a website without any traces left in the browser—perhaps to plan your Christmas shopping without the risk of other family members coming across the websites you've visited — open a new, incognito window first. You do this from the menu in the top right. When you close the private browsing window, your secret session stops.

When information has already been stored in the browser, you can delete it by opening the Chromium menu in the top right and clicking Settings. Scroll down and then show Advanced Settings, and there is an option to clear your browsing data. From the menu in the top right, you can also visit your browser history and delete any entries.

## Sending and Receiving Email with Claws Mail

Claws Mail is an open source program that is preinstalled on your Raspberry Pi. Find it in the Internet category of the Applications menu.

If you want to use your email on your Raspberry Pi, you need to know the details of the server for sending and receiving your email. Your email provider likely publishes this information on its website. You also need to know your user ID and password, which are likely to be the same as you use when logging in on webmail.

When you start Claws Mail for the first time, it walks you through a configuration wizard to add an account. If you experience any difficulties, you can edit the account settings, delete an account, or add a new account using the Configuration menu. There is an Auto-configure option, but this didn't work for our account when we tried, so be prepared for the extra work of putting all the information in the boxes manually if it doesn't work for you, either.

When you're set up, click the Get Mail button in the top to download your email. Claws Mail is similar to many other email clients, Thunderbird and Outlook. Your mail folders are shown on the left, and your messages are listed on the right, at the top. You can use the message preview pane at the bottom right to read messages, or you can double-click a message to open it in its own window.

Across the top is a menu bar with options for composing a new message, replying to a message, replying to all people copied that message, and forwarding the message. There's also a Wastebin button you can use to delete a message.

## Using the Image Viewer

It's easy to look at your digital photos and other images using PIXEL. Among the accessories on the Applications menu is the Image Viewer. You can start it from the menu (in the Accessories folder) or by double-clicking or right-clicking an image file.

The Image Viewer displays the picture, with a toolbar underneath it, as you can see in Figure 4–11. From left to right, this is the buttons:

- **Previous:** Goes to the previous photo in the folder. Note that any unsaved changes (such as rotation) are lost. You can also use the left-arrow key on the keyboard.
- **Next:** Goes to the next photo in the folder. With the Previous button, clicking this discards any unchanged changes you've made to the current photo. You can also use the right-arrow key on the keyboard.
- **Start slide:** Begins a slide of all photos in the folder. The interval between photos is set at 5 seconds, but you can change it in the preferences. You can also press the W key to start a slide show. There might be a short delay before the slide begins.
- **Zoom Out:** Reduces the magnification of the image. The keyboard shortcut is the Minus (-) key.
- **Zoom In:** Increases the magnification of the image. Scroll bars appear if the image becomes too big to fit in the Image Viewer, and you can use these to see different parts of the picture. The keyboard shortcut is the plus (+), with no need to use Shift.
- **Go to Original Size:** Resets any zooming to its full original size. This might be bigger than the Image Viewer, in which scroll bars appear, enabling you to move around the image. The keyboard shortcut is G.
- **Full Screen:** Expands the image to fill the monitor, so you lose the Image Viewer controls. Right-click the image to open a menu with all the same options. To revert to using the Image Viewer in a window, choose Full Screen from the menu or press ESC. You can also use the F11 key to switch the screen on and off.

FIGURE 4-11:
Sean in China, as seen through the Image Viewer.

GpicView, written by Hong Jen Yee / Raspberry Pi Foundation

- **Rotate Left:** Rotates the image 90 degrees counterclockwise. The shortcut is L.
- **Rotate Right:** Rotates the image 90 degrees clockwise. The shortcut is R.
- **Flip Horizontally:** Mirrors the image horizontally and can also be done with the H key.
- **Flip Vertically:** Turns the image upside down. The V key does the same.
- **Open File:** Opens a new file. You can also drag and drop an image from File Manager.
- **Save File:** Saves the image (including any rotations you have done) and replaces the original image. You get a warning before it happens. Keyboard shortcut: S.
- **Save File As:** Saves the image with a new filename so that it doesn't overwrite the original. (You can also press A to do this.)
- **Delete:** Deletes an image from your storage device. If you delete an image, it's not sent to the basket: You get one warning, but then it's toast! You can also use the Delete key.
- **Preferences:** Holds the settings you can change for Image Viewer so that you can customize it. You can turn off the warnings you get before overwriting or deleting an image, set Image Viewer to automatically save rotated images, change background colors of Image Viewer, and change slide show interval. There's also option to rotate images by changing their orientation value in the EXIF tag, which changes which way the camera was, instead of actually rotating the image content. It's okay to keep this selected, but this is where you disable it.
- **Exit Image Viewer:** Closes the Image Viewer application. You can also close the window by clicking the X in the top right as you would with any other window.

## Using the Text Editor

Among the accessories on the Applications menu is Leafpad, which is a simple text editor. (See Figure 4-12). To find it, click Text Editor in the Accessories part of the Applications menu.

The menus are logically organized, and if you've ever used a text editor on another computer, you'll find your way around in Leafpad easily.

The File menu is used to start new documents and open, save, and print files. There's also an option to quit here, although you can just close the Leafpad window.

The Edit menu gives you tools for undoing and redoing your work and for cutting, copying, pasting, deleting, and selecting all your text. Leafpad uses Windows shortcuts, too so you can use Ctrl+C to copy, Ctrl+V to paste, Ctrl+X to cut, and Ctrl+A to select all text.
