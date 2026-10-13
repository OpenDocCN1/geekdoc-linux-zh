```
# for historic reasons, since now it is supposed to be a directory
# (unless you have selected some database format other than the
# "text" default)
infofile "/var/adm/amanda/bwc/curinfo"     # database DIRECTORY
logdir   "/var/adm/amanda/bwc"             # log directory
indexdir "/var/adm/amanda/bwc/index"      # index directory
tapelist "/var/adm/amanda/bwc/tapelist"   # list of used tapes
# tapelist is stored, by default, in the directory that contains
# amanda.conf
# tapetypes
# Define the type of tape you use here, and use it in "tapetype"
# above. Some typical types of tapes are included here. The
# tapetype tells amanda how many MB will fit on the tape, how big
# the filemarks are, and how fast the tape device is.
# A filemark is the amount of wasted space every time a tape section
# ends. If you run `make tapetype` in tape-src, you'll get a
# program that generates tapetype entries, but it is slow as hell,
# use it only if you really must and, if you do, make sure you post
# the data to the amanda mailing list, so that others can use what
# you found out by searching the archives.
# For completeness Amanda should calculate the inter-record gaps
# too, but it doesn't. For EXABYTE and DAT tapes this is ok.
# Anyone using 9 tracks for amanda and need IRG calculations? Drop
# me a note if so.
# If you want amanda to print postscript paper tape labels
# add a line after the comment in the tapetype of the format
# lbl-temp1 /pathto/postscript/tapetype/labels.ps
# if you want the label to go to a printer other than the default
# for your system, you can also add a line above for a different
# printer. (I usually add that line after the dumpuser
# specification)
# dumpuser "operator"     # the user to run dumps under
# printer "myspostscript" # printer to print paper label on
# here is an example of my definition for an EXB-8500
# define tapetype EXB-8500 {
# ...
#       lbl-temp1 "/usr/local/amanda/config/lbl.exabyte.ps"
# }
# define tapetype SONY-AIT {
comment "Sony AIT "
length 51783 mbytes
filemark 772 kbytes
speed 6783 kbytes
}
define tapetype QIC-60 {
comment "Archive Viper"
length 60 mbytes
filemark 100 kbytes          # don't know a better value
speed 100 kbytes       # do
}
define tapetype DEC-DLT2000 {
comment "DEC Differential Digital Linear Tape 2000"
length 15000 mbytes
filemark 8 kbytes
speed 1250 kbytes
}
# goluboff@butch.Colorado.EDU
```