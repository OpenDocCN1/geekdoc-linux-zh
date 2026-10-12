# Creating an Image Gallery with Konqueror

There's a neat feature in Konqueror that lets you create a quick image gallery. The feature takes a directory of images, creates thumbnails for each one, and generates an HTML (Web) page. The HTML page includes a title you choose, all image thumbnails arranged on a page, and links to the larger images. Here's how you do it:

+   1.  Add images you want in your gallery to any folder (for example, `/home/jake/images`). Make sure they are sized, rotated, and cropped the way you like before beginning. (Try *The Gimp* for manipulating your images by typing **gimp** & from a Terminal.)
+   2.  Open the folder in Konqueror (for example, type `/home/jake/images` in the Location box).
+   3.  Click Tools → Create Image Gallery. The Create Image Gallery window appears.
+   4.  Type a title for the image gallery into the Page Title box. You can also select other attributes of the gallery, such as the number of rows, information about the image to appear on the page (name, size, and dimension), the fonts, and the colors to use.
+   5.  Click OK.

Konqueror generates the thumbnails and adds them to the thumbs directory. The image gallery page itself opens and is saved to the `images.html` file. (Select the Folders button to save the gallery under a different name. You can also have Konqueror create galleries in recursive subfolders to a depth you choose.) You can now copy the entire contents of this directory to a Web server and publish your pictures on the Internet. Figure 3-18 shows an example of a Konqueror image gallery.

![](bbox=[0.12, 0.6, 0.55, 0.79])

**Figure 3-18**: Create an image gallery in Konqueror.