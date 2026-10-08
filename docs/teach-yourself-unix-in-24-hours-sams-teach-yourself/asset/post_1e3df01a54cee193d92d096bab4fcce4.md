
# Printing in the UNIX Environment

## ACTION

- 1. To start, take a quick look at the contents of the /etc/printcap file:

```bash
% head -23 /etc/printcap
# $Header:/usr/msrc/usr/etc/printcap/RCS/printcap,v 1.235 93/11/04
=10:55:21 mn
Exp Locker: mm $
naglw:
  <dr=/usr/local/lib/ip/pmq:
  -pc=occl:
  -if=/usr/pool/lpr/aglw/logfile:
  -lo=/usr/pool/lpr/aglw/lock:ip=/dev/null:
  mj=25:mx3000:nd=/usr/local/lib/ip/ipnc:
  -cp=png:
  -rm=server.utech.edu.cwd:sd=/usr/pool/lpr/aglw:sh:
  -gf=/usr/lib/bispot:
  -nf=/usr/local/lib/devps/devps:
  zq=aqmq:aglw1,agl2,agl3,agl4:mu:
  tw=23:wk=Apple LaserWriter INT:
aglw1:
  <dr=/usr/local/lib/ip.sh:
  -if=/usr/pool/lpr/aglw/logfile:
  -lo=/usr/pool/lpr/aglw/lock:ip=/dev/null:
  mj=25:mx3000:nd=/usr/local/lib/ip/ipnc:
  -cp=png:
  -rm=server.utech.edu.cwd:sd=/usr/pool/lpr/aglw:sh:
  -gf=/usr/lib/bispot:
  -nf=/usr/local/lib/devps/devps:
  tw=23:wk=Apple LaserWriter INT:
```

I won't go into exhaust detail about the meaning of each field in this list. It suffices to say that the first line in each entry lists the name of the printer, a character, and other possible names for the printer. Each field following the printer is surrounded by commas and has a two-letter field name (for example, dr, nf), followed by the value of that particular field or setting. The fields of interest are the printer name; the wi field, which indicates the location of the printer; and the wk field, which indicates the type of printer.

- 2. There are no UNIX units to keep you from to slog through this configuration file. I have written a short, yet powerful, C shell script printers to get the desired information in a readable format. Notice the use of a here document to create the awk script and the multiple-line pipeline at the end of the script that does all the actual work.

```bash
% cat bin/printers
# printers - create a simple list of printers from the /etc/printcap
# file on the system.

# From
# Teach Yourself UNIX in 24 Hours
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_389_0.png)

# 382 Hour 18

```bash
set printcap=/etc/printcap
set awkscript=/tmp/awkscript.$$

/bin/rm -f $awkscript

cat << 'EOF' > $awkscript
NF == 2 { split($1, words, ";");
prname=words[1]
}
NF > 2 { printf("%-10s %s\n", prname, $0) }
'EOF'

egrep "^([A-Za-z]|:wi)" $printcap |
sed '/\:/g' | |
awk -f $awkscript |
sed "s/wi=\;s/(;)/$/" | |
more
/bin/rm -f $awkscript
```

Some of this is beyond what you have learned in this book about commands of scripts. In particular, the awk script, although only four lines long, shows some of the more powerful features of the program. Enter this as shown, but be careful to match the quotes and slash characters.

- 3. Once you've entered this script, enter the following:
```bash
% chmod +x bin/printers
```
That will ensure it's an executable script. Next, you need to inform the C shell, that you have added a new command, to the search path. rehash. Then you can run your new script:

```bash
% rehash
% printers | head -15
aglw AG 23 (multiple Apple LaserWriter Tint)
aglw1 AG 23 (Apple LaserWriter Tint)
aglw2 AG 23 (Apple LaserWriter Tint)
aglw3 AG 23 (Apple LaserWriter Tint)
aglw4 AG 23 (Apple LaserWriter Tint)
alpsw LIB 111 (Apple LaserWriter INTX)
bio COM BIT 28 (GraphPrinter (self-service))
cary Coudat (NE 37) (IBM 4019 Laser Printer)
cary CS 2249 (IBM 4019 LaserWriter lg)
c115w CS 115 (IBM 4019 Laser Printer (for CS180))
c115w CS 115 (IBM 4019 Laser Printer (for CS180))
csg40w CS 6040 (IBM 4019 Laser Printer )
csg50w CS 6050 (IBM 4019 Laser Printer )
csg1p CS 673 (C. Ito, white paper (self-service))
eng130c 130 (C. Ito, white paper (self-service))
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_390_0.png)

# Printing in the UNIX Environment

You can use this script to find printers of a certain type or in specific location, if the descriptions in your /etc/printcap are configured in the correct manner:

```bash
% printers -l plotter
knox 3164 (Hewlett Packard 7550 Plotter)
cp 6109 (CALCOMP 1073 Plotter)
cvp 6109 (VERSATEC-80 Plotter)
% printers -i grep
twi186 (Apple LaserWriter INT (private))
mathci 899 (C. Ito, white paper (self-service))
mathw 734 (multiple Apple LaserWriter INT)
mathw1 734 (Apple LaserWriter INT)
mathw2 734 (Apple LaserWriter INT)
cci 734 (C. Ito, white paper printer)
cp 6109 (IBM 4019 Laser Printer)
cvp 6109 (VERSATEC-80 Plotter)
```

- 4. Now you should be able to choose a printer that's most convenient for your location. Setting the environment variable PRINTER to that value. You might also want to tuck that into the last line of .login so that next time you log in, the system will remember your printer.

```bash
% setenv PRINTER mathw
% vi .login
```

If your printer is not responding to what you set the PRINTER variable to, especially on System V:

```bash
setenv PRINTER "David Taylor"
setenv BIN "889"
setenv PRINTER mathw
```

The first, and perhaps biggest, hurdle for printing on UNIX has been solved: figuring out what the system calls the printer. Not only do you have a new command, printers, for your UNIX system, but you can see how you can customize UNIX to meet your needs by creating aliases and shell scripts.

## Task 18.2: Printing Files with lpr or ip

### DESCRIPTION

Now that you have identified the name of the printer to use, how about sending information to the printer? If you are on a BSD system, the command to do this is lpr. You can print the results of a pipe command by adding lpr at the end of the pipeline, or you can print files directly by specifying them to the program. You can even use < input.

If you’re using System V of UNIX, you will need to use the ip command instead. As you read through this hour, you will see the differences between lpr and ip. Note how the philosophies of the two vary. The flags available for lpr and ip are numerous, and the most valuable ones are listed in Table 18.1 and Table 18.2.

# Table 18.1. Useful flags for lpr.

| Flag | Meaning |
| :--- | :--- |
| -h | Do not print the header page. |
| -i | Indent the entire file eight spaces before printing. |
| -L | Print in landscape (sideways) mode, if the printer is capable of doing so. |
| -Ppr | Send the print job to printer pr. |
| -R | Print pages in reverse order. |

# Table 18.2. Useful flags for ip.

| Flag | Meaning |
| :--- | :--- |
| -dptr | Send the print job to the printer named ptr. |
| -Pn | Print only page n. |
| -title | Use title as the cover page title, where title is any string. |

- 1. Here’s a demonstration of what happens if you try to use ip or lpr without specifying a printer and without having the PRINTER environment variable set. First use the unsetenv command to remove environment variable definitions:

```bash
% unsetenv PRINTER
% who | ip
lpr: No printer specified
Broken pipe
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_392_0.png)

- 2. Some systems default to a printer named lp in this situation, so if you don't get an error message, that's what happened. If you have stat (a command for checking the status of a printer), the -d flag will result in ipstat listing your default printer.

To specify a printer, use the -P flag with ip or the -d flag with ip, followed immediately by the name of the printer:

```bash
% who | lpr -Pmathiw
```

Specifying a printer with the -P flag (or -d with ip) will always override the environment variable specified in PRINTER; however, you can specify the default printer with PRINTER and specify other printers without needing any further work.

Notice that I printed the output of the command but received absolutely no information regarding what printer it sent to. To make life easier, I can redefine PRINTER:

```bash
% setenv PRINTER mathw
```

| Pos | User | Size | Jobname |
| :--- | :--- | :--- | :--- |
| 1 | KOSHIWE | 1024 | KOSHIWE1024 |
| 2 | KOSHIWE | 1024 | KOSHIWE1024 |
| 3 | KOSHIWE | 1024 | KOSHIWE1024 |
| 4 | KOSHIWE | 1024 | KOSHIWE1024 |
| 5 | KOSHIWE | 1024 | KOSHIWE1024 |
| 6 | KOSHIWE | 1024 | KOSHIWE1024 |
| 7 | KOSHIWE | 1024 | KOSHIWE1024 |
| 8 | KOSHIWE | 1024 | KOSHIWE1024 |
| 9 | fueling | 0126 | fueling0216 |
| 10 | zeta | 0042 | zeta0042 |
| 11 | tjared | 0142 | tjared0142 |
| 12 | SUJATHA | 0043 | SUJATHA0043 |
| 13 | SUJATHA | 0043 | SUJATHA0043 |
| 14 | SUJATHA | 0044 | SUJATHA0043 |
| 15 | bee | 0785 | bee0785 |
| 16 | bee | 0785 | bee0785 |
| 17 | bee | 0785 | bee0785 |
| 18 | ssinfo | 0353 | ssinfo0353 |
| 19 | ssinfo | 0353 | ssinfo0353 |
| 20 | ssinfo | 0353 | ssinfo0353 |
| 21 | ssinfo | 0353 | ssinfo0353 |
| 22 | stacysm2 | 0321 | stacysm20321 |

