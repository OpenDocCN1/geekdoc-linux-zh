# 5.4 Ghostscript for Non-PostScript Printers

Most inexpensive printers do not have built-in PostScript support. These include most inkjets and a few low-end or older laser printers. However, the computer can often interpret and rasterize the file, ultimately sending a finished bitmap to the printer. Ghostscript, developed by Aladdin Enterprises, is a popular free interpreter and rasterizer that comes with most Linux distributions and has most or all of the devices configured.

While Ghostscript supports many printers, the correct options and drivers are not always obvious and its documentation is messy, with information scattered over a number of files. Certain options—those for color inkjets in particular—significantly change output quality. For example, the defaults for an Epson Stylus Color 850 are not the best for transparencies, although the printer is capable of producing very good results (ideally you would want unidirectional printhead movement to reduce streaking and perhaps a different kind of dithering from usual).

You typically integrate Ghostscript into Linux’s print spooling system as a filter. PostScript goes in and printer-ready data comes out and goes to the printer. The filter is usually a shell script, which parses some arguments and then calls Ghostscript with some options. Here is a very simple script:

```
```sh
#!/bin/sh
/usr/bin/gs -q -dNOPAUSE -dBATCH -sOutputDevice=-- -r720x360 -sDEVICE=epson -
```
```

The heart of this is, of course, the call to Ghostscript (gs). When you customize your filter, you will probably invoke gs on the command line to avoid specifying the many parameters that a print filter requires.

To send the output of a run on foo.ps straight to the parallel port, run this:

```
```sh
# gs -q -dNOPAUSE -dBATCH -sOutputDevice=/dev/lp0 -r720x360
- -sDEVICE=epson foo.ps
```
```

# Using the uniprint Driver

You’ll generally want to call the uniprint driver as follows:

```
```sh
# gs @name.upp -q -dNOPAUSE -dBATCH -sOutputDevice=device [files]
```
```

name.upp is actually a parameter file in the Ghostscript library directory. For example, stc800.upp is a 720-by-720-dpi plain-paper mode for the Epson Stylus Color 800. The file itself is a huge listing of options that set uniprint as the driver and tweak the parameters for this particular printer.