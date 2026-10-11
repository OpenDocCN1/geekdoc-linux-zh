| Product   | Country | Foreign | Total | Average |
|:----------|--------:|--------:|------:|--------:|
| binders   |     1024|      576|   1600|       800|
| pencils   |      472|      235|    707|       353|
| rules     |      311|      797|   1108|       554|
| stencils  |      846|      621|   1467|       733|

Total number of products: 4

End of report

# Listing 7.2 report.bash

```
#!/bin/bash
#
# report.bash: simple report formatter
#
# Ken O. Burtch
# CVS: $header$
#
# The report is read from DATA_FILE. It should contain
# the following columns:
#
# Column 1: PRODUCT = Product name
# Column 2: CSALES = Country Sales
# Column 3: PSALES = Foreign Sales
#
# The script will format the data into columns, adding total and
# average sales per item as well as a item count at the end of the
# report.

# Some Linux systems use USER instead of LOGNAME
if [ -z "$LOGNAME" ] ; then # No login name?
declare -rx LOGNAME="$USER" # probably in USER
fi
shopt -s -o nounset

# Global Declarations

declare -rx SCRIPT=$0###/ # SCRIPT is the name of this script
declare -rx DATA_FILE="report.txt" # this is raw data for the report
declare -i ITEMS=0 # number of report items
declare -i LINE_TOTAL=0 # line totals
declare -i LINE_AVG=0 # line average
```