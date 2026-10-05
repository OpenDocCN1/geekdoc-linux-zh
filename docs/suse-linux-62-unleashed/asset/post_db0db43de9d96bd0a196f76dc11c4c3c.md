
You do not specify a return type for a constructor because the return type is always understood to be a reference to an instance of the class. Also, constructors always have the same name as the class.

## Compiling Java Source Code

Java source code is compiled for the Java platform. The source code needs to be translated into byte code by a Java byte compiler. This is most commonly performed with the Sun JDK byte code compiler. Others are available, like Likes. IDE’s Java Workshop will also do byte compilation for you.

The javac byte compiler included in the JDK takes input files with the *.java extension. To compile the HelloWorld example, you would type on your Linux shell command line:

```
# javac HelloWorld.java
```

> Note
The javac compiler is located under the /usr/lib/jdk1.7/bin directory after install Java for SuSE Linux.

The compiler produces a file called HelloWorld.class in the same directory as the HelloWorld.java file. These are the byte code compiled classes. Java creates a .class file for every class even if one file contains multiple classes or inner classes. You can type the following on your Linux command line shell for quick command-line help on the javac compiler:

```
# javac -h
```

## Creating and Running an Application

Java applications require a special entry point for a class. This entry point is the main method. The Java interpreter calls this method first and passes an array of command-line arguments.

```
public static void main(String args[]) {
  ...
}
```

The Java interpreter (java) runs standalone Java executable programs. Applications normally run from a command line as:

```
# java Options Classname
```

To run the HelloWorld class, run the Java interpreter and indicate the class name of the program you want it to run. The Linux kernel can also be configured to automatically run the interpreter for you.

```
# java HelloWorld
```

> Note
The Java interpreter requires classes with a main method defined. Any class must contain a main method.

## Summary

This chapter presented some basic features of the most popular programming tools for Linux. Each software tool has particular strengths and weaknesses, but nearly all are robust and mature. As you can see, you'll enjoy a wealth of software you can use to develop programs or administer your system.

## CHAPTER 26

## Linux Graphics Applications

IN THIS CHAPTER

- Linux Graphics Applications 818
- Graphics File Formats 818
- Converting Graphics 819
- Editing Graphics 820
- Creating Graphics 827
- Displaying and Printing Graphics 835

The interesting thing about graphics is that it has a broader marketplace than many other Linux applications. The graphics tools range from a straightforward paint program to a highly sophisticated graphics program that rivals or exceeds commercial packages for other operating systems.

This means the Linux graphics environment can help:

- Children learn about colors and how to use simple painting tools
- The small business that needs a tool to produce graphics layouts and brochures
- The serious graphics artist who needs state-of-the-art tools to produce complex works and will not compromise on quality

This chapter covers converting, editing, and creating graphics using popular tools available under Linux. Other tools, such as office suites, are covered only from the perspective of generating a presentation or slideshow. Complete coverage of office suites is available in Chapter 28. "Productivity Clients and Suites for Linux." Most of the graphics packages mentioned in this chapter are SuSE Linux 6.2's six-CD set and can be installed using the YaST tool or the RPM package manager.

## Linux Graphics Applications

There is a special mini-HOWTO on graphics maintained by Michael J. Hammel that is available at http://www.graphics-muse.org/linux/lgh.html. It is not included with most HOWTO distributions because it is very graphics-intensive.

## Graphics File Formats

Linux supports most of the popular graphics formats. The following is a representative list of the supported formats:

- GIF (various formats of GIF)
- JPEG and MPEG
- BMP
- PCX
- Photo CD (PCD)
- XCF (GIMP native format)
- MIFF (ImageMagick native format)
- TIFF
- TARGA or TGA format
- PostScript and Encapsulated PostScript (EPS)
- PNG
- PPM
- PGM

## Converting Graphics

One of the sure bets in the graphics world is that you will have one format and need another to complete the task. Many Web sites use GIF format, while others prefer JPEG format. Linux graphics tools can help convert the image from one format to another. There are both command-line tools and graphical user interface (GUI) tools to convert graphics.

The main issue with converting is that there may or may not be a loss in resolution or clarity when files are converted. This mainly stems from the fact that some image formats are lossy. Lossy means that some of the data is lost as an image is compressed or converted. This lost data usually has no effect on the image's display if you have 100,000 data points in a solid blue box. If 100 data points are lost, it will still look like a solid blue box. The advantage of a lossy format is that it will compress and you will actually save space. A lossless image will not drop datapoints. The good feature is that every data point is still out there. The bad side is that it will be a larger image.

The other conversion is the size of the final file. What started out as a small image in one format may grow into an almost 0.5MB image when you convert to another format. A good example is converting a JPEG file to a PostScript file—it is possible to have a 25K JPEG file convert into a 421KB PostScript file.

## Using convert

convert is a command-line utility that transforms one graphical format to another. convert supports most major types of images, including GIF, JPEG, Photo CD, TIFF, and so on. If you have a file named snapshot1.gif and want to convert it to a JPEG file, use the following command:

```
# convert snapshot1.gif snapshot1.jpg
```

convert is part of the ImageMagick toolset, along with display. display can be used to display the converted image.

```
# display snapshot1.jpg
```

display will bring up the snapshot1.jpg image in a separate window.

## Using xv

xv is one of the standard UNIX tools for converting and viewing images. The xv RPM is approximately 1.1MB in size and the latest update is available at http://www.trilon.com/xv/. xv is released under a shareware arrangement, where the suggested fee for commercial or business use is $25. Additional information about xv is available at http://www.trilon.com/xv/.

xv is an excellent tool for the display and conversion of images. The best part is that xv runs under numerous UNIX and PC platforms. This allows portability between platforms and the ability to utilize the same tool under different environments.

## Command-Line Utilities

Gifftans is a good tool for converting GIF87 to GIF89 images. Its main purpose is to make one color in the GIF file transparent. One example is changing the background color of a GIF file to match the background color of the Web page. This would make the box around the GIF “transparent” or blend into the Web page and highlight the contents of the GIF image.

## Editing Graphics

There are many tools that can be used to edit graphics—some allow basic functionality such as crop and rotate, while others can transform the image using special filters or effects.

## GQview

GQview provides the ability to see and organize existing images. It provides a feature that allows you to see a thumbnail sketch of each image in a file list (see Figure 26.1), and you can display the image on the screen (see Figure 26.2) while also looking at the other images in thumbnail format. GQview also has the capability to zoom in and out to certain portions of the image. Information about GQview can be found at http://qview.netpedia.net/index.html. The latest version is GQview 0.7.0, released July 3, 1999.

GQview works in conjunction with other tools such as xv, GIMP, Electric Eyes, and paint for the editing of images. These tools are on a default menu and additional tools can be added. The editing tool is launched from a pull-down menu, and GQview is still active in the background.
