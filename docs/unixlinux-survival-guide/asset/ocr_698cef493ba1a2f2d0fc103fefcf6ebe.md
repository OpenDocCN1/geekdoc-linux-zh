![](bbox=[0.22, 0.09, 0.86, 0.42])

# FIGURE 3.4 Graph with the default axis.

```
# $Id: graphcreate.sh,v 1.1 2004/08/26 10:36:57 erikk Exp erikk $
################################################################
#
#   file:        graphcreate.sh
#
#   purpose:     tests if there are files with
#                the extension .plot and feeds
#                them to gnuplot
#
#   author:      Erik Keller
#
#   parameters:  none
#
################################################################

# Variables
MY_DIR=/export/home/users/erikk/work/baselines/plotcmds
GNUPLOT=/usr/local/bin/gnuplot

for THE_PLOTC in $MY_DIR/*.plot; do
    if [ -f $THE_PLOTC ]
    then
        $GNUPLOT $THE_PLOTC
    fi
done
```