
```
PRINTCAPS = printserver generic-lprng generic-lpd papd.conf \
 samba-printcap make-spool-script
```

要将 `mikado` 添加到列表中，将其更改为

```
PRINTCAPS = printserver mikado generic-lprng generic-lpd papd.conf \
 samba-printcap make-spool-script
```

然后在以 `printserver` 开头的行之后添加

```
mikado: $(STD_DEPS)
```

否则，其他所有内容保持不变。现在，`make` 也将生成一个名为 `mikado` 的新文件。

> NOTE
>
> 该系统绝非一成不变。它是用 `m4` 编写的，以提供灵活性。例如，如果你需要对打印机进行分组并仅在某些主机上使某些打印机可见，你可以通过拆分 `printer-list.m4` 并在需要时包含所需部分来实现。

## 5.6 Utilities

每个系统管理员都应该了解一些有用的打印工具。

### a2ps

简写为 ASCII to PostScript，这是将 ASCII 文本文件转换为 PostScript 的当前最先进技术。它不随某些主要发行版提供。

### enscript

与 `a2ps` 类似，它的功能没有那么多。它随主要发行版标准提供。以下是其使用示例：

```
$ enscript -2r textfile
```

## wordlist

Figure 5.1: Saving paper with enscript

This takes *textfile* and prints what would normally be two pages onto one, as in Figure 5-1.

## gv

A GUI front end for previewing files with Ghostscript.

## psnup

A tool for printing multiple pages on one page. From time to time, psnup encounters a file that’s difficult to parse. Using Ghostscript to filter the file (later in this section) can help. While we mention it here as a separate utility, you probably don’t need to install psnup because a2ps has a psnup mode, too:

```
$ a2ps -4 -o out.ps in.ps
```

This example takes the file *in.ps* and outputs it on four sides per page in *out.ps*.

## Additional Ghostscript Utilities

Ghostscript also offers filters useful for calming down rogue PostScript files. In particular, you can turn a PostScript file into an Encapsulated PostScript (EPS) file with the following:

```
$ gs -q -dBATCH -dNOPAUSE -sDEVICE=epswrite -sOutputFile=name.eps name.ps
```

The input and output files are *name.ps* and *name.eps*. You will come across this mostly when users are attempting to include a file in their documents. Ghostscript also has PDF and non-EPS drivers—`pdfwrite` and `pswrite`.

## Converting PostScript to a Bitmapped Format

Ghostscript can convert PostScript to bitmaps in the same way it allows use of non-PostScript printers. This feature is particularly useful for Web site graphics, occasional presentations, and some other miscellaneous applications.

Depending on how you installed Ghostscript, it may offer a number of graphics format drivers along with its printer drivers, so a command such as

```
$ gs -q -dBATCH -dNOPAUSE -sDEVICE=jpeg -sOutputFile=name.jpg name.ps
```

will create the jpeg file *name.jpg* from *name.ps*. (Most distributions outfit Ghostscript with quite a few graphics format drivers, including `ppm`, `tiff`, `jpeg`, and `png`.)

## Improving Your Conversions

The results of this conversion may not look anywhere close to optimal, since they get rasterized at whatever resolution you pick with the `-r` option, and therefore exhibit jaggies and font problems. You can improve on this by antialiasing; here is one way to do so with a jpeg file:

```
$ gs -r300 -q -dBATCH -dNOPAUSE -sDEVICE=ppmraw -sOutputFile=- name.ps | \ pnmscale -xscale .2 -yscale .2 | cjpeg -quality 75 > name.jpg
```

Here, we're first rasterizing the PostScript file at 300 dpi, creating ppm output, then sending that to a program called `pnmscale`, which reduces the size here to a fifth of the original, antialiasing in the process. Finally, the file goes to `cjpeg`, which creates a jpeg file with the quality set to 75 percent. The `pnmscale` comes from the `pbmplus` toolkit (included in Red Hat 6.x). To create other formats, replace the `cjpeg` portion of the command with something like this:

```
$ pnmtopng > name.png
```

or

```
$ pnmtotiff > name.tiff
```

You'll usually have to tinker a little with options to get the best results. Finally, while the `pbmplus` toolkit is quite good at batch processing, you may still find a program like `gimp` very helpful for manual manipulation. Relevant man pages: `gs` (1), `cjpeg` (1), `pnmtopnm` (1), `ppm` (1)

## 5.7 Troubleshooting
