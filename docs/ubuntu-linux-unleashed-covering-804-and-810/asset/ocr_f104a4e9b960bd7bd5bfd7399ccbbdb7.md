for drivers not yet included, but you must be able to compile the application from source to use them.

Supported USB scanners are automatically detected and the appropriate driver is loaded automatically. The USB devices tell the USB system several pieces of information when they are connected—the most important of which are the vendor ID and the device ID. This identification is used to look up the device in a table and load the appropriate driver. You will find that Ubuntu successfully identifies and configures most modern USB-based scanners.

Many scanners are supported in Linux. If yours is not, it still might be possible to use it. The Kooka and Xsane scanner applications are included with Ubuntu and are fairly straightforward to use. They can both be found in the Graphics menu as the Scanner Tool.

# Working with Graphics Formats

Image file formats are developed to serve a specific technical purpose (lossless compression, for example, where the file size is reduced without sacrificing image quality) or to meet a need for a proprietary format for competitive reasons. Many file formats are covered by one or more patents. For example, the GIF format had fallen into disfavor with the open-source crowd because the patent holder waited a while before deciding to enforce his patent rights rather than being upfront with requests for patent royalties.

If you want to view or manipulate an image, you need to identify the file format to choose the proper tool for working with the image. The file's extension is your first indicator of the file's format. The graphics image formats supported by the applications included with Ubuntu include

+   - .bmp—Bitmapmed graphics, commonly used in Microsoft Windows
+   - .gif—CompuServe Graphics Interchange Format
+   - .jpg—Joint Photographic Experts Group
+   - .pcx—IBM Paintbrush
+   - .png—Portable Network Graphics
+   - .svg—Scalable Vector Graphics
+   - .tif—Tagged Image File format

An extensive list of image file extensions can be found in the man page for ImageMagick, an excellent application included with Ubuntu, which you learn more about in upcoming sections of this chapter.