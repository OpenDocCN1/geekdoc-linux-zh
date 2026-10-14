
# Part 2: Starting Out with Ubuntu

When importing, F-Spot allows you to specify a tag to identify all of the photos as a group. You can use this tag to easily find the photos in your album.

To complete the import, click the Import button.

> **Secret**
> 
> When you import images from a digital camera or external storage device, F-Spot always copies the image and leaves the original. Likewise, when you import images from a folder, F-Spot copies the image and leaves the original, but you can change that in the Preference settings.
> 
> F-Spot stores images in the Photos folder under your home folder. F-Spot keeps photo information (such as file location and tags) in a separate database file, also located in your home folder. Look for the file `.gnome2/f-spot/photos.db` in your home folder. You can access this database using the sqlite3 command-line program in a Terminal window, but be careful not to delete or modify the file—F-Spot won’t be able to track the photo information.

Once you’ve imported the images, they appear as an *import roll* in the main F-Spot viewing window, shown in Figure 10-13.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_299_0.png)

**Figure 10-13:** The main F-Spot viewing window.

The F-Spot viewing window consists of five areas:

- ♦ The menu bar
- ♦ The toolbar
- ♦ The sidebar
- ♦ The viewing area
- ♦ The status bar

The following sections walk through each of these areas in F-Spot.

## The Menu Bar

The menu bar contains all of the options for you to view, manage, and manipulate images in the F-Spot library. It consists of the following menu items:

- ♦ Photo: Import new images, manage image versions, export images to another application, print them, or send them via email.
- ♦ Edit: Modify a selected image in the viewing area. You can rotate, adjust the color, change the timestamp of the image, add or remove tags assigned to the image, and delete the image from the F-Spot library. This menu also contains entries to set the preferences for F-Spot and to install additional plug-in modules.
- ♦ View: Start a slideshow of the current images, view images in Full-Screen mode, alter the layout of the images in the viewer, and zoom in or out from the image. You can also set what image elements appear in the viewing window, as well as what window areas appear.
- ♦ Find: Find a specific image or group of images based on tags, assigned ratings, dates, or when imported.
- ♦ Tags: Add and remove tags from individual images or groups of images, as well as create new tag names.
- ♦ Help: Display the help manual for F-Spot.

F-Spot allows you to easily print images or send them via email from the Photo menu area. You can also select the Export To option to export selected images to a CD for burning or to any of several online image-storage applications, such as Flickr, PicasaWeb, and 23hq.

## The Toolbar

The toolbar provides quick access to several common features in F-Spot:

- ♦ Import: Retrieve images from a folder or external digital camera and place them in the F-Spot library.
- ♦ Rotate Left: Rotate the selected image or images counterclockwise 90 degrees.
- ♦ Rotate Right: Rotate the selected image or images clockwise 90 degrees.
- ♦ Browse Mode: The default mode. Display thumbnails of all the images in the library, or all of the images selected by a specified filter.
- ♦ Edit Image: Open an image in the Image Editor, which allows you to crop the image and apply effects to it.
- ♦ Switch to Full-Screen Mode: Display the image in Full-Screen mode.
- ♦ Switch to Slideshow Mode: Single-step through the images one at a time as a slideshow.

The Slideshow mode allows you to automatically display all of the images in the Browse window in order, which is perfect for presentations or displaying your photos to others. In Full-Screen mode, F-Spot enlarges the image to fill the entire screen.

## The Sidebar

The sidebar area contains two sections:

- The Tag Selector area
- The Image Information area

The Tag Selector allows you to quickly view all images with a specific tag. F-Spot includes several default tags that you can apply to your images, such as favorites, hidden, people, places, and events.

If you assign tags when you import a group of images, F-Spot adds those tags to the Tag Selector area so you can easily and quickly access those images.

The Image Information area provides basic information about the image selected in the viewer window. If there are multiple versions of the image available (see "Using the F-Spot Editor" later in this chapter), you can select which version of the image to view.

## The Viewing Area

The viewing area is divided into two sections. The top section contains the Arrange By tool. The Arrange By tool allows you to quickly locate an image based on one of two criteria:

- The image date
- The image location

You can toggle the criteria used by the View menu bar option. Just select the Arrange By item and select either month or folder.

Under the Arrange By tool is the main viewing area. F-Spot opens in Browse mode, which displays thumbnails of all the images in the library. You can specify which images appear in the Browse mode by selecting a tag from the Tag Selector area in the sidebar. When you do that, the find bar appears at the top of the viewing area, shown in Figure 10-14.

You can combine tags in the find bar by simply selecting another tag from the Tag Selector. You can also right-click on the tag in the find bar to remove it from the find filter or negate it in the find filter. Negating a tag displays all images in the library that do not have a specific tag.

## The Status Bar

The status bar, located at the bottom of the F-Spot display window, shows the status of the photos displayed in the viewing area. If F-Spot displays all of the photos from the library, the status bar shows the total number of images. If you select images, the status bar indicates how many images have been selected. If you use the find bar to filter images, the status bar indicates how many images are being displayed to the total number of images in the library.

The other element in the status bar is the Quick Zoom tool. This tool allows you to change the zoom level in the viewing area. You can quickly increase or decrease the size of the thumbnail images using this tool.
