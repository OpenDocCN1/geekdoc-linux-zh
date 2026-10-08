```
#!/bin/bash
# tohtml.sh [v. 0.2.01, reldate: 04/13/12, a teeny bit less buggy]

# Convert a text file to HTML format.
# Author: Mendel Cooper
# License: GPL3
# Usage: sh tohtml.sh <textfile> target htmlfile
# Script can easily be modified to accept source and filenames.

# Assumptions
# 1) Paragraphs in (target) text file are separated by a blank line.
# 2) Jpeg (.jpg) are located in "images" subdirectory.
# In the target file, the image names are enclosed in square brackets,
# for example, [image01.jpg].
# 3) Emphasized (italic) phrases begin with a space+underscore
# or the first character on the line is an underscore
# and end with underscores+space or underscore+end-of-line.

# Settings
# FNTSIZE=2           # Small-medium font size
# IMGDIR="images"    # Image directory
# Headers
# HDR01="<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 4.01 Transitional//EN">
# HDR02-1="<!-- Converted to HTML by ***tohtml.sh*** script -->"
# HDR03="<!-- script author: Leo Cooper <cooperthegrelabs@gmail.com> -->"
# HDR11="<head>"
# HDR11a="</head>"
# HDR12a="<title>"
# HDR120="</title>"
# HDR121="<meta NAME="GENERATOR" CONTENT="tohtml.sh script">
# HDR13-="<body bgcolor="#dddddd"> # Change background color to size.
# HDR14a="<font size="
# HDR14b="</font>"
# Footers
# FTR10="</body>"
# FTR11="</html>"

# Tags
# BOLD="<b>"
# CENTER="<center>
# END_CENTER="</center>"
# LF="<br>"

write_headers ()
{
echo "$HDR01"
echo
echo "$HDR02"
echo "$HDR03"
echo
echo
echo "$HDR10"
echo "$HDR11"
echo "$HDR121"
echo "$HDR11a"
echo "$HDR13"
echo
echo -n "$HDR14a"
echo -n "$FNTSIZE"
echo "$HDR14b"

```

# Appendix A. Contributed Scripts