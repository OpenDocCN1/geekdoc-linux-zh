# geniconvtbl

# 421

# geniconvtbl - Generate iconv Code Conversion Tables

# Synopsis

/bin/geniconvtbl [-fnq] [-o outputfile] [-p preprocessor] [-W arg] [-DName] [-Dname=def] [-Idirectory] [-lname] [-infile...]

# Description

The geniconvtbl command, new in the Solaris 8 Operating Environment, accepts code conversion rules defined in flat text file(s) and writes code conversion binary table file(s) that can be used to support user-defined iconv code conversions (see iconv(1) and iconv(3C)) for more detail on the iconv code conversion.

# Options

+   -f Overwrite output file if the output file exists.
-n Do not generate an output file. This option is useful to check the contents of the input file.
-o outfile Specify the name of the output file.
-p preprocessor Use specified preprocessor instead of the default preprocessor, /usr/lib/cpp.
-q Quiet suppress warning and error messages.
-W arg Pass the argument arg to the preprocessor. If you specify this more than once, pass all arguments to the preprocessor.

+   -DName
-Dname=def
-Idirectory
-Uname

Pass these options and their arguments to the preprocessor.

# Operands

+   -infile

A path name of an input file. If you specify no input file, geniconvtbl reads from the standard input stream. You can specify more than one input file.

# Output

Output is from the standard input stream, geniconvtbl writes output to the standard output stream. If you specify one or more input files, geniconvtbl reads from each input file and writes to a corresponding output file. Each of the output file names is the same as the corresponding input file with .bt appended.

You must move the generated output files to the following directory before using the iconv(1) and iconv(3C) code conversions.