
# postmd

# 1073

## Description

The postmd filter reads a series of floating-point numbers from files, translates them into a PostScript grayscale image, and writes the results to the output. In a typical application the numbers might be the elements of a large matrix written in row major order, while the printed image could help locate patterns in the matrix. If you specify no files or if - is one of the input files, the standard input is used.

## Notes

Using white (that is, 255) in a grayscale list is not recommended. It does not show in the legend and band graph that postmd displays below each image.

## Options

- - b num Pack the bitmap in the output file, using num patterns. A value of 0 turning off all copying of the output file. By default, num is 6.
- - c num Print num copies of each page. By default, only one copy is printed.
- - d dimer Set the matrix dimensions for all input files to dimer. You can give the dimer string as rows or rows columns. If you omit the columns value, set it to rows. By default, postmd assumes each matrix is square and sets the number of rows and columns to the square root of the number of elements in each input file.
- - g list Use a list, comma- or space-separated string of integers each lying between 0 and 255, to assign PostScript grayscale to the regions of the real line chosen by the -l option. 255 corresponds to white, and 0, to black. The postmd filter assigns a default grayscale that omits white (that is, 255) and gets darker as the moves from left to right along the real line.
- - i list Use a list, comma- or slash- (/) separated string of N floating-point numbers to partition the real line into 2N-1 regions. Specify the list in increasing numerical order. The partitions are used to map floating-point numbers from the input files into grayscale integers that are either assigned automatically by postmd or that are arbitrarily chosen using the -g option. The default interval list is -1,0,1, which partitions the real line into seven regions.
- - m num Magnify each logical page by the factor num Scale pages uniformly about the origin which, by default, is located at the center of each page. The default magnification is 1.0.
- - n num Print num logical pages on each piece of paper, where num can be any positive integer. By default, num is set to 1.

# 1074

## postmd

- o list Print pages whose numbers are given in the comma-separated list which contains single numbers and ranges N1-N2. A missing N1 means the lowest-numbered page, a missing N2 means the highest. The page range is an expression of logical pages instead of physical sheets of paper. For example, if you are printing two logical pages to a sheet and you specified a range of 4, two sheets of paper containing four page layouts would print. If you specified a range of 3-4 when requesting two logical pages to a sheet, then only 3 and 4 layouts would print and they would appear on one physical sheet of paper.

-o list Print files in either p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is portrait.
- -w window Use window, comma-, or space-separated list of four positive integers, to choose the upper-left and lower-right corners of a submatrix from each of the input files. Row and column indices start at 1 in the upper-left corner and the numbers in the input files are assumed to be written in row order. By default, the matrix is displayed.
- -x num Translate the origin inches along the positive x axis. The default coordinate system is the origin fixed at the center of the page with x to the right and y up the page. Positive num moves everything up the page. The default offset is 0 inches.
- -y num One matrix only is displayed on each logical page, and each of the input files makes complete descriptions of exactly one matrix. Matrix elements are floating-numbers arranged in row order in each input file. White space, including newlines, is not used to determine matrix dimensions. By default, postmd assumes the matrix is square and sets the set of rows and columns to the square root of the number of elements in the input file. Supplying default dimensions on the command line with the -d option overrides this behavior, and in that case, the dimensions apply to all input files.

You can supply an optional header with each input file to set the matrix dimensions, the partition of the real line, the grayscale mode, and a window into the header. The header contains keyword/value pairs, each on a separate line. It begins on the first line of each input file and ends with the first unrecognized string, which should be the first matrix element. Values in the header take precedence but apply only to the current input file. Recognized keywords are dimension, interval, grayscale, and window. The syntax of the value string that follows keyword parallels what is accepted by the -d, -i, and -w options.

## Examples

Suppose file initially contains the 1,000 numbers in a 20 x 50 matrix. Then, you can produce the same output by completing three steps. First, issue the following command.

```
castle% postmd -d20x50 -i"-100 100" -g0,128,254,128,0 file
```

Next, prepend the following header to file.

# postplot 1075

dimension 20x50
interval -100.0 .100e+3
grayscale 0 128 254 128 254

Then, issue the following command.
```
caste% postmd file
```

The interval list partitions the real line into five regions, and the grayscale list maps numbers less than -100 or greater than 100 into 0 (that is, black), numbers equal to -100 or 100 into 128 (that is, 50 percent black), and numbers between -100 and 100 into 254 (that is, almost white).

## Files

- - /usr/lib/lp/postscript/forms.ps
- /usr/lib/lp/postscript/ps.requests

## Exit Status

- - 0 Successful completion.
- non-zero An error occurred.

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNpsf |

## See Also

dpost(1), postdaisy(1), postmd(1)

# 1076

## postscript

## Options

- - c num Print num copies of each page. By default, only one copy is printed.
- - f name Print text, using font name. You can use any PostScript font, although the best results are obtained with constant-width fonts. The default is Courier.
- - m num Magnify each logical page by the factor num Scale pages uniformly about the origin which, by default, is located at the center of each page. The default magnification is 1.0.
- - n num Print num logical pages on each piece of paper, where num can be any positive integer. By default, num is set to 1.
- - o list Print pages whose numbers are given in the comma-separated list. The list contains single numbers and ranges N1-N2. A missing N1 means the lowest-numbered page, a missing N2 means the highest.
- - p mode Print file names in either p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is landscape.
- - w num Set the line width used for graphics to num points, where a point is approximately 1/72 of an inch. By default, num is set to 0 points, which forces lines to be pixel wide.
- - x num Translate the origin inches along the x axis. The default coordinate system has the origin fixed at the center of the page with x to the right and y up the page. Positive num moves everything right. The default offset is 0.0 inches.
- - y num Translate the origin inches along the positive y axis. Positive num moves everything up the page. The default offset is 0.0.

## Files

```
/usr/lib/lp/postscript/forms.ps
```

```
/usr/lib/lp/postscript/postplot.ps
```

```
/usr/lib/lp/postscript/ps.requests
```

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwidth |

## See Also

download(1), dpost(1), postdaisy(1), postdam(1), postio(1), postmd(1), postprint(1), postreverse(1), plot(1B), attributes(5)

## Diagnostics

An exit status of 0 is returned if file names were successfully processed.
