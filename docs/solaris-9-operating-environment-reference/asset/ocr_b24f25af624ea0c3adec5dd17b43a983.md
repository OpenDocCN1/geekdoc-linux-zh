# 1076

# postscript

# Options

+   - c num num copies of each page. By default, only one copy is printed.

+   - f name Print text, using font name. You can use any PostScript font, although the best results are obtained with constant-width fonts. The default is Courier.

+   - m num Magnify each logical page by the factor num Scale pages uniformly over the origin, which by default, is located at the center of each page. The default magnification is 1.0.

+   - n num Print num logical pages on each piece of paper, where num can be any positive integer. By default, num is set to 1.

+   - o list Print pages whose numbers are given in the comma-separated list. The list contains single numbers N and ranges N1-N2. A missing N means the lowest-numbered page, a missing N2 means the highest.

+   - p mode Print file names in either p (portrait) or l (landscape) mode. Only the first character of mode is significant. The default mode is landscape.

+   - w num Set the line width used for graphics to num points, where a point is approximately 1/72 of an inch. By default, num is set to 0 points, which forces lines to be one pixel wide.

+   - x num Translate the origin inches along the x axis. The default coordinate system has the origin fixed at the center of the page with x to the right and y up the page. Positive num moves everything right. The default offset is 0.0 inches.

+   - y num Translate the origin inches along the positive y axis. Positive num moves everything up the page. The default offset is 0.0.

# Files

```
/usr/lib/lp/postscript/forms.ps
```

```
/usr/lib/lp/postscript/postplot.ps
```

```
/usr/lib/lp/postscript/ps.requests
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |

| Availability | SUNwidth |

# See Also

download(1), dpost(1), postdaisy(1), postdam(1), postio(1), postmd(1), postprint(1), postreverse(1), plot(1B), attributes(5)

# Diagnostics

An exit status of 0 is returned if file names were successfully processed.