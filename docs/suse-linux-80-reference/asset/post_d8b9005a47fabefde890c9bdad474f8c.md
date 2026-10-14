
Manually adjust the print filter configuration files to add any special settings. Every queue has its own separate configuration file `/etc/lpdfilter/queue/conf` (replace queue here with the actual queue name), which also contains information on each option.

## Adding Special Settings to the Print Filter

1. If the print data is not in PostScript format, it is, by default, converted to PostScript using `/usr/lib/lpdfilter/filter/type2ps` (replace type with the actual type of data to be printed). If there is an appropriate script saved to `/etc/lpdfilter/queue/type2ps` (replace queue with the actual queue name and type with the actual type of data to be printed), the script will be used to convert the data to PostScript. This script receives the print data from stdin and sends PostScript to stdout.

2. The PostScript data can be reformatted if there is an appropriate script in `/etc/lpdfilter/queue/pre`. You can also add your own PostScript preloads using a script for this purpose. This script receives PostScript data from stdin and sends the PostScript output to stdout. Programs for reformatting PostScript data can be found in the package `psutils`. `pstops`, in particular, features extensive reformatting functions. Refer to the man page for pstops (man `pstops`) for more information on this.

3. Special Ghostscript parameters: The parameters for running Ghostscript are saved to the `/etc/lpdfilter/queue/upp` file when configuring with YaST2. Special Ghostscript parameters can also be added manually to this file. See Section *A Little About Ghostscript* on page 215 for more information about Ghostscript parameters.

4. The output of Ghostscript can also be reformatted if an appropriate script is located in `/etc/lpdfilter/queue/post`. This script receives the Ghostscript output from stdin and sends the printer-specific data to stdout.

## A Hardware-Independent Example

Suppose you want a queue called `test` to print out ASCII text with numbered lines and with two pages reduced to fit on one. Then, you could create the scripts `/etc/lpdfilter/test/ascii2ps` and `/etc/lpdfilter/test/pre`:

```bash
#!/bin/bash
cat -n - | a2ps -1 --stdin=',' -o -
```

*File 18: `/etc/lpdfilter/test/ascii2ps`: ASCII to PostScript conversion*

```bash
#!/bin/bash
pstops -q '2:0L0.6(20cm,2cm)+1L0.6(20cm,15cm)'
```

*File 19: `/etc/lpdfilter/test/pre`: Reformatting PostScript*

These scripts must be executable for all users, which is accomplished with

```shell
earth:  # chmod -v a+rx /etc/lpdfilter/test/ascii2ps
earth:  # chmod -v a+rx /etc/lpdfilter/test/pre
```

The pstops command only works for PostScript files created in such a way that they can be reformatted at all (which is usually the case).

## Using Custom PostScript Preloads

PostScript preloads are small PostScript files containing special PostScript commands. They can be upstreamed before the actual print data to initialize a PostScript printer or Ghostscript.

Typically, PostScript preloads are used to activate duplex printing or special paper trays in PostScript printers or to set Ghostscript margin settings and gamma correction accordingly.

First, the PostScript printer or Ghostscript must be able to process the special PostScript commands listed below properly (Ghostscript does not react to duplex print or paper tray commands).

Suppose the queue in question is called test.

**Duplex printing** — To enable or disable duplex printing, create the files `/etc/lpdfilter/test/duplexon.ps` and `/etc/lpdfilter/test/duplexoff.ps` as follows:

```postscript
%!PS
statusdict /setduplexmode known
statusdict begin true setduplexmode end if pop
```

*File 20: `/etc/lpdfilter/test/duplexon.ps`: Enable Duplex Printing*

```postscript
%!PS
statusdict /setduplexmode known
statusdict begin false setduplexmode end if pop
```

*File 21: `/etc/lpdfilter/test/duplexoff.ps`: Disable Duplex Printing*

**Paper tray selection** — To activate the default paper tray with 0 or the paper tray with the number 2, for example, create the files `/etc/lpdfilter/test/tray0.ps` and `/etc/lpdfilter/test/tray2.ps` as follows:

```postscript
%!PS
statusdict /setpapertray known
statusdict begin 0 setpapertray end if pop
```

*File 22: `/etc/lpdfilter/test/tray0.ps`: Activating Paper Tray 0*

```postscript
%!PS
statusdict /setpapertray known
statusdict begin 2 setpapertray end if pop
```

*File 23: `/etc/lpdfilter/test/tray2.ps`: Activating Paper Tray 2*

**Margin settings** — To change the margin settings, create the file `/etc/lpdfilter/test/margin.ps` as follows:

```postscript
%!PS
<<
/.HWMargins [left bottom right top]
/PageSize [width height]
/Margins [left-offset top-offset]
>>
setpagedevice
```

*File 24: `/etc/lpdfilter/test/margin.ps`: Margin Settings*

The margin settings left, bottom, right, and top and the paper size width and height must be specified in dots, where one dot is 1/72 inches (approx. 0.35 mm). The margin offsets left-offset and top-offset, on the other hand, should be specified in dot matrices, depending on the resolution.

If only the position of the printout should be shifted on the paper, the following file is sufficient: `/etc/lpdfilter/test/offset.ps`

```postscript
%!PS
<< /Margins [left-offset top-offset] >> setpagedevice
```

*File 25: `/etc/lpdfilter/test/offset.ps`: Position of the Printout*

## Gamma correction

To modify the brightness range of the colors, create the files `/etc/lpdfilter/test/cmyk.ps` and `/etc/lpdfilter/test/rgb.ps` as follows:

```postscript
%!PS
cyan exp magenta exp yellow exp black exp setcolortransfer
```

*File 26: `/etc/lpdfilter/test/cmyk.ps`: CMYK Gamma Correction*

```postscript
%!PS
red exp green exp blue exp currenttransfer setcolortransfer
```

*File 27: `/etc/lpdfilter/test/rgb.ps`: RGB Gamma Correction*

The color model (CMYK or RGB) must be compatible to your printer. The values set for cyan, magenta, yellow, black, red, green and blue must be between 0.001 and 0.999.

You can get an overall impression of how the above files will take effect in the graphical interface using the following commands (without gamma correction):

```shell
earth:  # gs -r60 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps
```

(with gamma correction, any one of these following examples):

```shell
earth:  # gs -r60 /etc/lpdfilter/test/cmyk.ps \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps

earth:  # gs -r60 /etc/lpdfilter/test/rgb.ps \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps
```

Exit with `Ctrl` + `C`.

## Resetting the printer

To restore basic printer settings, create the file `/etc/lpdfilter/test/reset.ps` as follows:

```postscript
%!PS
serverdict begin 0 exitserver
```

*File 28: `/etc/lpdfilter/test/reset.ps`: Resetting the Printer*

To activate a PostScript preload file, create the script `/etc/lpdfilter/test/pre` as follows:

```bash
#!/bin/bash
cat /etc/lpdfilter/test/preload.ps -
```

*File 29: `/etc/lpdfilter/test/pre`: Loading PostScript Preload*

Replace preload with the actual preload file name. The script must be executable and readable for all users, which is accomplished with chmod:

```shell
earth:  # chmod -v a+rx /etc/lpdfilter/test/pre
earth:  # chmod -v a+r /etc/lpdfilter/test/preload.ps
```

The same mechanism can also be used to send a PostScript file to the printer after the actual PostScript print data. To restore the original settings of a printer after a print job is completed, create the script `/etc/lpdfilter/test/pre` as follows:

```bash
#!/bin/bash
cat /etc/lpdfilter/test/preload.ps - /etc/lpdfilter/test/reset.ps
```

*File 30: `/etc/lpdfilter/test/pre`: PostScript Preload and PostScript Reset*

## Example for Configuring a GDI Printer

GDI printers cannot usually be used in Linux. See Section *GDI Printers* on page 192. However, special driver applications exist for some GDI printers. These driver applications usually supplement Ghostscript by converting the Ghostscript output to a printer-specific format. Such driver applications often only allow for limited print options, such as black-and-white only. Ghostscript and the driver application thus work together as described in the following (see also Section *A Little About Ghostscript* on page 215):

1. Ghostscript resolves the PostScript data into a matrix containing individual pixels. The matrix data is then relayed to the appropriate Ghostscript driver in suitable format and resolution.

2. The matrix data is then converted to the printer-specific format by the driver application.
