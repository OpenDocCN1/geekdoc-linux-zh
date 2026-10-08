# lpr — Submit BSD Print Requests

# Synopsis

/usr/ucb/lpr [-P destination] [-# number] [-C class] [-J job]
[-T title] [-i [indent]] [-1|-2|-3|-4 font] [-w cols] [-m] [-h] [-s]
[-filter-option] [file...]

# Description

The lpr command submits print requests to a destination. lpr prints files (file) and associated information, collectively called a print request. If you do not specify file, lpr assumes the standard input.

The print commands locate destination information in a specific order. See printers(4) and printers.conf(4) for details.

Print requests with more than 52 files specified are truncated to 52 files. lpr displays a warning message.

> Note — Print jobs are assumed to contain one type of data. That type of data is either specified on the command line or autodetected (simple, PostScript) according to the contents of the first file in the job.

# Options

+   -p number Print a specific number of copies. Specify number as a positive integer. The default for number is 1.

+   -1|-2|-3|-4 font Mount the specified font in the font position 1, 2, 3, or 4. Specify font as a valid font name.

+   -C class Print class as the job classification on the banner page of the output. Enclose class in double quotes if it contains blanks. If you do not specify class, the name of the system (returned by hostname) as the job classification. See hostname(1).

+   -h Suppress printing of the banner page of the output.

+   -i [indent] Indent the output a specific number of space characters. Use indent to indicate the number of space characters to be indented. Specify indent as a positive integer. Eight space characters is the default. The -i option is ignored unless you specify it with the -p filter option.

+   -J job Print job name on the banner page of the output. Enclose job in double quotes if it contains blanks. If you do not specify job file (or the case of multiple files, the first file specified on the command line) as the job name on the banner page of the output.

+   -m Send mail after file is printed (mail(1)). By default, no mail sent on normal completion of a print request.