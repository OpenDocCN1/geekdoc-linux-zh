# Chapter 9

Graphic Files

+   **Key Topics:**
+   - Bitmapped and vectored graphics
+   - Anatomy of a graphic file
+   - Liblug
+   - Screen shots
+   - Gifs ave
+   - Raw keyboard mode

Thus far, I've shown you how to draw a number of images on the screen. That's okay for your own personal usage. Sometimes, though, it'd be nice to capture these images to show others, especially if they don't use Linux or SVGA1ib. It'd also be nice to be able to view images that others have given you.

To accomplish this, we have the graphic file. Graphic files are binary files that contain image data. The standard formats are cross-platform, and they're often compressed to save space. Some common formats are GIF, JPG (or JPEG), and BMP.

Like fonts, graphic files come in two formats: bitmapped and vectored. A bitmapped image is made up of a grid, much like a screen matrix, whereas a vector format utilizes mathematical equations to record image data. The vector format corresponds with a vector font and often allows for a smaller file than a bitmap of the same image would.

Graphic files consist of header information, meaning the file format, as well as size and color information, which is then followed by the actual image data. The image data can be as small as one pixel or as large as your computer's memory will allow.

You may have worked with text files in C before; examples include /etc/passwd and even /etc/vga/libvga.config. Here's how you might print libvga.config to the screen:

```
```
char line[256];
FILE *myfile;
```
```