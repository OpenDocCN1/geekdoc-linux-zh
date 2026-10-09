
- Developing LSB-Certified Applications (http://www.ibm.com/developerworks/linux/lib1ibrary/l-lsb.html)
- DistroWatch.com (http://www.distrowatch.org/)
- Filesystem Hierarchy Standard (http://www.pathname.com/Fhs/)
- Free Software Directory (http://www.gnu.org/directory/GNU/)
- Free Standards Group (http://www.freestandsards.org/)
- Freeware for Solaris (http://www.sunfreeware.com/)
- FSG Certification (http://www.freestandsards.org/certification)
- FSG GForge (http://gforge.freestandsards.org/)
- GNU make (http://www.gnu.org/software/make/manual/make.html)
- Guide to LSB Certification (http://www.opengroup.org/lsb/cert/docs/LSB_Certification_Guide.html)
- IBM Copyright and Trademark Information (http://www.ibm.com/legal/copytrade.shtml)
- Java API (http://java.sun.com/reference/api/index.html)
- JNI Overview (http://java.sun.com/docs/books/tutorial/native1.1/concepts/index.html)
- Knopper.Net (http://www.knopper.net/)
- Linux Assigned Names And Numbers Authority, The (http://www.lanana.org/)
- Linux Defeats Microsoft Windows in Top 5 (http://www.reallylinux.com/docs/l1winw.html)
- Linux From Scratch (http://www.linuxfromscratch.org/)
- Linux Kernel (http://lwn.net/2001/1220/kernel.php3)
- Linux Online: Distributions and FTP Sites (http://www.linux.org/dist/)
- LSB Buggzilla (http://bugs.linuxbase.org/)
- LSB Certification (http://www.opengroup.org/lsb/cert/)
- LSB Certification: Fee Schedule (http://www.opengroup.org/lsb/cert/docs/LSB_Fee_Schedule.html)
- LSB Certification: Frequently Asked Questions (http://www.opengroup.org/lsb/cert/docs/faq.html)
- LSB Certification: Problem Reporting and Interpretations System (http://www.opengroup.org/lsb/cert/PR/)
- LSB Certification Policy (http://www.opengroup.org/lsb/cert/docs/LSB_Certification_Policy.html)
- LSB Certification Register (http://www.opengroup.org/lsb/cert/register.html)
- LSB Development Environment (http://www.linuxbase.org/build/)
- LSB Futures Candidates (http://www.linuxbase.org/futures/candidates/)
- LSB Futures Selection Criteria (http://www.linuxbase.org/futures/criteria/)
- LSB Product Standards (http://www.opengroup.org/lsb/cert/docs/prodstandards.html)
- LSB Project Downloads (http://www.linuxbase.org/download/)
- LSB Project Proposal and Call for Participation (http://old.lwn.net/1998/0528/a/lsb.html)
- LSB Test Suites (http://www.opengroup.org/lsb/cert/docs/testsuites.html)
- LSB Written Specification (http://www.linuxbase.org/spec/)
- Managing Projects with make (http://www.oreilly.com/catalog/make2/)
- Open Group, The (http://www.opengroup.org/)
- Open Brand—Test Suite Acceptance Criteria, The (http://www.opengroup.org/openbrand/testing/testprocs/accprocs.html)
- Open Internationalization (http://www.openi18n.org/)
- PASC (http://www.pasc.org/)
- RPM Package Manager (http://www.rpm.org/)
- Rsync (http://rsync.samba.org/)
- Sample Implementation Download (http://ftp.freestandards.org/pub/lsb/impl/)
- Single UNIX Specification (http://www.unix.org/version3/)
- Sleepycat Software: Berkeley Database (http://www.sleepycat.com/)
- Solaris-compatible Thread Library (http://sourceforge.net/projects/scl1/)
- Study Shows Broad Use of Linux (http://www.eewek.com/print_article/0,3668,a=43824,00.asp)
- System V Application Binary Interface Group (http://www.caldera.com/developers/gabi/2003-12-17/contents.html)
- Technical Guide for Porting Applications from Solaris to Linux (http://www.ibm.com/developerworks/eserver/articles/porting_linux/)
- TET 3.3 Documentation (http://tetworks.opengroup.org/documents/docs33.html)
- TETware User Guide (http://tetworks.opengroup.org/documents/3.3/uguide.pdf)
- UNIX System, The (http://www.unix-systems.org/)
- Using and Porting the GNU Compiler Collection (GCC) (http://gcc.gnu.org/onlinedocs/gcc-2.95.2/gcc_toc.html)
- What is Copyleft? (http://www.gnu.org/copyright/)

## APPENDIX C

### Book Logistics

#### C.1 READ ONLINE

The current version of this book can be found online in HTML (http://lsbbook.gforge.freestandards.org/) and PDF (http://lsbbook.gforge.freestandards.org/lsb-book.pdf) formats.

#### C.2 REPORT BUGS

The LSB accepts problem reports and suggestions via Bugzilla (http://bugs.linuxbase.org/).

#### C.3 OBTAIN SOURCE

This book is licensed under the GNU Free Documentation License, and its source is available online via CVS:

```
CVSROOT=:pserver:anonymous@cvs.gforge.freestandards.org: \
/cvsroot/lsbbook
cvs -dCVSROOT login
cvs -dCVSROOT -z3 co lsbbook
```

## Index

### Numbers

- 88open, 22

### A

- ABIs (Application Binary Interfaces), xvi, 15
    - candidate, 107
    - changes in, 114
- absolute addresses, 65
- alien, 18, 122, 197
- Alpha architecture, 54
- Anderson, Stuart, xxi
- Apache, 195
    - configuring, 199–201, 209
    - LSB-compliant version of, 209, 212
    - shared libraries in, 205
    - testing, 204
- apachectl, 204
- APIs (Application Programming Interfaces), 9, 38
    - LSB-compliant, 23, 204–206
    - non-LSB, 195
    - standardization of, 19–22
- appbat, see Application Battery
- appeals, 87
- applicants, 225
- Application Battery (appbat), xxii, 11, 84, 107, 116, 169, **193–214**, 230
    - configuring, 199–202
    - downloading, 89, 99, 197, 212
    - installing, 197–199, 211
    - testing, 202–204
    - using LSB Development Environment with, 204–206
- Application Binary Interfaces, see ABIs
- application checker, see lsbappchk
- Application Programming Interfaces, see APIs
- applications
    - add-on, 43
    - certifying, 92–99
    - compatible, 23
    - desktops for, 39
    - documentation for, 43
    - installing, 41–44, 95
    - LSB Certification Ready, 93–95, 195–196
    - LSB-compliant, 199, 206
    - market opportunities for, 9
    - packaging, see packages
    - platform-tuned, 14
    - prerelease versions of, 197
    - shrink-wrapped, 3, 9, 13, 24
    - testing, 9, 155, 163–164
- archLSB, see LSB Written Specification, architecture-specific supplement
- argument types, 206
- Austin Group, The, xxi, xxvi, **22**, 230
- authentication, **30–31**, 130, 147, 200, 214
    - database engines for, 209

### B

- Berkeley Database, 38, 209, 233
- big endian, 58
- bind mounts, 158, 178
- `bindext2xdomain( )`, 28
- Brown, Mark, xxi
- BSD UNIX, 60
- Buggzilla, 164, 231, 235
- byte ordering, 57–60

### C

- C language, 27, 54, 57, 60, 230
- c++, 55
- C++ language, xvii, 11, 27, 54, 56, 230
- C99 standard, 11
- candidates
    - identification of, 107–109
    - selection criteria for, 38, **104–110**, 209, 232
    - testing, 116
    - tracking, 109, 111
- catgets( ), 28
- Caunt, Kevin, xxi
- cc, 55
- cc environment variable, 183
- Celestia, 195
    - configuring, 201, 210
    - LSB-compliant version of, 208, 210, 212, 212
    - testing, 202
- Certification Agreement, 18, 73, 76, **78**, 81, 86, 96, 225
- Certification Authority, 18, 73–74, 76, 78–80, 82–83, 87–89, 91–92, 95–98, 225–226
- Certification Register, 76, 78–79, 81, 86, 88, 90, 96, 98, 100, 225, 232
- Certification System Deficiency, 83–85, 97–98, 205, 225, 227
- char type, 208
- chroot environment, 156–160, 165–166, 168–171, 189
- command-line parameters, 35, 208
- Common Operating System Environment, see COSE
- Common UNIX Printing System, see CUPS
- compatibility, 8, 10
    - binary, 9, **13–24**
    - multiple-version, 24, 163
    - source, xv, 23
- compliance, 74, 92, 156, 226
- Concurrent Versions System, see CVS
- configuration files, 43, 95
- conformance requirements, 73–75, 77, 79, 91–93, 226
- Conformance Statement Questionnaires, 18, 73, 77, **79–80**, 84, 88, 90–91, 95, 98, 100, 226, 230
    - uploading, 81–82, 96
- copyright, 233
- COSE (Common Operating System Environment), 42
- cio, 19
- crlf, 63
- cron, 124
- CUPS (Common UNIX Printing System), 211
- curses, h, 39
- CVS (Concurrent Version System), 167

### D

- daemons, 159, 200
- Debian distribution, xxv, 122, 161, 197, 200
- DESTDIR environment variable, 211
- device driver, 38
- Digital Equipment Corporation, xvi
- directory hierarchy, 42, 131–132
- DISPLAY environment variable, 201
- distributions, 4, 9, 23, 41, 43, 53–54, 108, 231
    - 32-bit versus 64-bit, 207
    - certifying, 73–90, 193, 202
    - configuring, 199
    - testing, 194
