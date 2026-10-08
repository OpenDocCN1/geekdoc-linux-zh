# Printing in the UNIX Environment

network driver: /usr/local/lib/lp/lpnc
ditroff filter: /usr/local/lib/devps/devps
print formats: graphics, ditroff, use pr, proff
queue ordering: age
host attachment: server.utech.edu
spooling directory: server/spool/lp/mathlw
location: MATH 734
description: multiple AppleLaserWriter INT

+   5. The lpinfo command can also show you a list of what printers are available, but I
the output format considerably more difficult to understand than lpinfo:
% lpinfo -a head -15
glw: server.utech.edu; AG 23; multiple Apple LaserWriter INT
glw1: server.utech.edu; AG 23; Apple LaserWriter INT
glw2: server.utech.edu; AG 23; Apple LaserWriter INT
glw3: server.utech.edu; AG 23; Apple LaserWriter INT
alpsw: sentinel.utech.edu; 111; Apple LaserWriter INT
bio: ace.utech.edu; COM B117; DataPrinter (self-service)
cary: franklin.utech.edu; Cuad (NE-87); IBM 4019 Laser Printer
cslw: server.utech.edu; CS 2249; Apple LaserWriter HTX
cs115w1: expert.utech.edu; IBM 4019 LaserPrinter (for CS1800)
cs115w2: expert.utech.edu; CS 115; IBM 4019 LaserPrinter (for CS1800)
csg40w1: franklin.utech.edu; CS 0040; IBM 4019 LaserPrinter
csg50w1: expert.utech.edu; CS 0050; IBM 4019 LaserPrinter
cspl1: expert.utech.edu; CS 073; C.Itoh, white paper (self-service)
eng130w2: age.utech.edu; ENG 130; C.Itoh, white paper (self-service)

If you find this readable, you're undoubtedly making a real UNIX!
Broken pipe

The output of the printers command specifies the location of the printer that printed
tfile, I need to go to another building to pick up my hard copy. (The location is
specific in the output of the printers command).

# Task 18.3: Formatting Print Jobs with pr

The Printer it generated looked good, but, I would like to have a running
header on each page that shows the name of the file and the page number. I'd also
ave to have a bit more control over some other formatting characteristics. This is exactly
where the pr command comes in handy. Not intended for printing, pr is a general
pagination and formatting command that can be used to display information on the screen.
Ever better, pr is available on BSD and System V UNIX.

The program is loaded with options, which are quite useful at times. For example,
-2 makes the output two columns, which is useful for printing results of the which command
landscape mode! The most useful options are presented in Table 18.3.