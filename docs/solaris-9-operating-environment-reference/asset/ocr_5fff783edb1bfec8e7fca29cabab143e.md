# 876 mp

# Operands

filename The name of the file to be read.

# Environment Variables

XPDISLAY Used with option -D or -P to determine the X Print Display to which the client connects.

MP_PROLOGUE Used to determine the directory in which the page formatting files (.xpr or .ps) are kept. These files determine characteristics such as page decorations, number of logical pages per physical page, and landscape or portrait format. In the absence of MP_PROLOGUE, the default location of the directory is /usr/lib/lp/locale/C/mp.

MP_LANG If you specify neither the -D nor -P option, a prologue file called as /usr/openwin/lib/local/locename/print/prolog.ps or /usr/lib/lp/locale/locename/mp/prolog.ps, where locename is the value of the MP_LANG environment variable, if present, is prepended to the output to be printed. If both are present, then prolog.ps is given preference for backward compatibility. If either of these files is not present and you do not specify the -D option, a configuration file of the locale called /usr/lib/lp/locale/locename/mp/mp.conf is used as the source of the configuration information that substitutes the prologue for printing. The prolog.ps disables mp.conf for backward compatibility.

# Exit Status

+   0 Successful completion.
1 An error occurred.

# Supplied Prolog Files

The following files are provided. Files with .ps extensions are for the PostScript output; files with .xpr extensions are for the X Print Server client. .xpr files are created for 300dpi printers and scale to other resolution values.

mp.com.ps Common prologue file for all other .ps files in this directory.

mp.pro.psmp.pro.xpr Used by default.

mp.pro.ff.psmp.pro.ff.xpr Used with the -ff option.

mp.pro.fp.psmp.pro.fp.xpr Used with the -fp option.