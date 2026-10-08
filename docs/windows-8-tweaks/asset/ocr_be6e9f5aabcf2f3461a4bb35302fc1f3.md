from a website that adheres to the RSS enclosures standard and includes images as enclosures in the feed.

You can identify compatible feeds by looking for the enclosure tag in the source of the feed for each <item>. For example, look for <enclosure url="http://www.site.com/image.jpg" type="image/jpeg" />. To learn more about the RSS enclosures standard, check out the Wikipedia entry at http://en.wikipedia.org/wiki/RSS_Enclosures.

Now that you know of some sample feeds and how to identify other feeds, you can get started:

+   1. First, you need to get to the .theme file packed inside the .themetpack or .deskthemetpack file you created earlier or from a file you downloaded online. In order to do that, you must enable viewing file extensions in File Explorer. When File Explorer is open, click on the View tab and then check File name extensions in the show/hide section near the right.

+   2. Navigate to the directory where you saved your .themetpack or .deskthemetpack file and rename the file .cab. A theme pack file is nothing more than a compressed cabinet file.

+   3. After you've renamed it to a cab file, open the file with any compatible compression utility such as WinRAR (www.rarlabs.com) or even with the native Windows Explorer shell and extract the .theme file within.

+   4. After extracting the .theme file, right-click it and select Open With. Deselect the Use this app for all .theme files and then click More options and click Notepad.

+   5. Now you will be able to edit the theme file manually. Scroll through the file and look for the [Slideshow] section. If this section already exists, delete it.

+   6. Create a new [Slideshow] section by entering the following code at the bottom of the file in Notepad:

```
[Slideshow]
Interval=600000
Shuffle=1
RssFeed= http://feeds.feedburner.com/bingimages
```

The value of Interval is listed in milliseconds, so 600000 means the wallpaper will change every 10 minutes. Feel free to change this value. When Shuffle equals 1, shuffle is enabled (0 is disabled). Replace the value of RssFeed with the URL of a compatible RSS enclosure feed.

+   7. Save the changes you made to the new .theme file and close Notepad. Make sure you change the Save As Type on the Save As dialog box to All Files (*.*) before saving so the .txt extension is not appended to the filename.