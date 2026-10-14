+   - **Rotate image:** Three buttons that allow you to rotate the image 90, 180, and 270 degrees.
+   - **Mirror image:** Two buttons that mirror the image using the horizontal or vertical axis.
+   - **Zoom:** Zoom in to or out from the image in the Viewer window.

If you set the filename and extension of the file in the Main window, the Viewer automatically saves the image using that file type and name. If not, the Viewer provides a Save As dialog box that allows you to set these values. XSane supports saving images using the file types shown in Table 15-3.

| Table 15-3: XSane Image File Types |
|---|---| 
| File Type | Description |
| JPEG | A standard compressed image format defined by the Joint Photographic Experts Group |
| PNM | Portable anymap image format |
| PNG | Portable network graphics format, a standard open-source compressed image format |
| TIFF | Tagged image file format, an uncompressed image format controlled by Adobe |
| PostScript | A standard programming language that uses text commands to draw an image; popular in the UNIX world |
| PDF | Portable document format, a standard image format created and controlled by Adobe |
| TXT | Standard text file format, used only when operating XSane in optical character recognition (OCR) mode for saving text found in the scanned image |

XSane provides a wide selection of standard file formats for storing your image file. Images saved as PDF files are compatible with Adobe Acrobat Reader applications on the Microsoft Windows platform, which is a great feature of XSane.

# Digital Cameras

Chapter 10, "Image Manipulation," discussed the F-Spot Photo Manager software package. F-Spot is the default application Ubuntu uses when you connect a digital camera to your Ubuntu workstation.

When Ubuntu detects that you've connected a digital camera to your workstation, it starts the F-Spot Photo Manager, which queries you for the device to connect to, as shown in Figure 15-11.

You may have to experiment with which option to select. For example, when I selected the Olympus entry (which is the make of my digital camera) I received an error that F-Spot couldn't communicate with my camera. When I selected the Mass Storage Camera entry, it worked just fine.