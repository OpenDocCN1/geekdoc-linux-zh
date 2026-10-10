
## www.gnu.org

The home page for the GNU (a recursive acronym that stands for GNU’s Not Unix) project. Many of the utilities included with FreeBSD—such as the GCC compiler, the GAWK pattern-matching language, the Emacs editor, and the f77 FORTRAN compiler—are from the GNU project. This site contains information on almost all the GNU project’s software.

## www.gnome.org

The home page for the Gnome Desktop Environment project. Gnome news, tutorials, and so on can be found here.

## www.kde.org

The major competitor to Gnome. If you prefer KDE, this is your site.

## www.apache.org

This is the home page for the Apache Web server project—the most popular Web server in the world. It is free and is the Web server of choice for FreeBSD. This site also contains information about projects that can be used to extend Apache’s functionality, such as PHP, Perl, TCL, and more.

## www.mysql.com

MySQL is the open-source SQL database of choice for FreeBSD. This site contains documentation, tutorials, and so on for the MySQL database software.

## www.postgresql.org

The site for another open-source SQL database available for FreeBSD. PostgreSQL has more features than MySQL but is somewhat slower.

## www.php.net

The home page of the embedded scripting language of choice for building Web-based applications. PHP is an open-source competitor to Active Server Pages (ASP). PHP is primarily used for linking Web sites to databases. It integrates well with MySQL and PostgreSQL.

## www.perl.com

This site includes information and tutorials on the Perl programming language, which is included as a standard part of FreeBSD.

## www.python.org

The home page for the Python programming language, which is a popular alternative to Perl.

## www.sendmail.org

The home page of the Sendmail mail transfer agent, which is the default mail transfer agent included with FreeBSD.

## www.postfix.org

The home page for a popular alternative mail transfer agent for Sendmail. Postfix is a drop-in replacement for Sendmail. It is my favorite mail transfer agent. New users will find it much easier to configure than Sendmail.

## www.osnews.com

Although it is not FreeBSD specific, this news site often contains articles of general interest to FreeBSD users and sometimes runs FreeBSD specific articles.

## Usenet Newsgroups

The following non-FreeBSD-specific newsgroups are available on Usenet (contact your ISP to find out what news server you should be using to access Usenet).

### General Unix Newsgroups

These newsgroups cover topics that are not specific to FreeBSD but are of interest to Unix users in general. For example, they cover Unix administration practices, general Unix security issues, general Unix shell use, and so on.

- comp.security.unix
- comp.sources.unix
- comp.unix.admin
- comp.unix.advocacy
- comp.unix.misc
- comp.unix.programmer
- comp.unix.questions
- comp.unix.shell
- comp.unix.user-friendly

### X-Windows Newsgroups

- comp.emulators.ms-windows.wine
- comp.windows.x
- comp.windows.x.announce
- comp.windows.x.apps
- comp.windows.x.i386unix
- comp.windows.x.intrinsics
- comp.windows.x.motif
- comp.windows.x.pex

## Index

### Symbol and Numbers

- (asterisk), 164, 641
- @ (at) symbol in zone files, 758
- \ backslash, 149
- $db (database handle), 658
- $db->quote function, 663
- $ (dollar sign), 756
- filenames, 149
- $GENERATE directive, 757
- # (hash mark), 375
- $INCLUDE directive, 757
- $ORIGIN directive, 756
- % (percent wildcard), 641
- %! (begin PostScript file), 342
- # (pound sign), 78
- #! sequence, 254
- ; (semicolon), 640
- / (slash), 166
- $TTL directive, 757
- 4Front sound drivers Web site, 112
- 500 Server Error message (Apache), 605

### A

- A (Address) records (zone files), 760
- a2ps program, 342
- abort command, 355-357
- access, denying with ACL, 205
- access control
  - Apache
    - by address and password, 595
    - by hostname/IP address, 590-591
    - by password authentication, 592-593
    - groups, adding, 594
    - overview of, 590
    - users, adding, 593-594
  - disabling in xhost, 846
- Samba, 785
  - guest account, 788
  - share-level, 788
  - user-level, 786-787
- Access Control Lists (ACLs), 753
  - configuring, 200-201
  - deleting entries, 205
  - denying access with, 205
  - getting information about current settings, 201
  - maximum permissions mask, setting, 202
  - overview of, 200
  - removing entries, 206
  - users or groups, adding, 203-205
- access privileges and databases, 657-658. See also permissions
- access to FTP
  - anonymous, allowing, 617-618
  - controlling, 616-617
- access-control statements, 754
- accessing database content with Perl and CGI, 662
- ACLs. See Access Control Lists (ACLs)
- Add a New User form, 49-51
- AddHandler directive (Apache), 601-602
- adding
  - groups to /etc/group file, 211
  - hard disks, 401
  - shells to system
    - /etc/shells file, 235-236
    - installing from packages, 234
    - installing from ports, 234-235
    - overview of, 234
    - tcsh compared to bash, 233-234
  - users
    - adduser script, 206-208
    - /etc/passwd and /etc/master.passwd files, 209-210
    - /etc/pwd.db and /etc/spwd.db files, 210
    - post-installation, 49-51
- AddModule directive (Apache), 598
- Address (A) records (zone files), 760
- Address Resolution Protocol (ARP)
  - checking cache contents with arp command, 500
  - Ethernet level and, 497-499
  - routing between networks using, 499
- AddType directive (Apache), 602
- adduser command, 853
- adduser script, changes in, 206
- administering
  - databases, scripts for
    - Perl, 658-662
    - Python, 660-661
  - systems, 189
- air gaps, 717-718
- alias for queries, creating, 645
- aliases, creating
  - bash, 247
  - tcsh, 245
- aliasing printer names, 356

- AllowMouseOpenFail option of ServerFlags section of Xf86Config file, 829
- AllowOverride directive (Apache), 586-588
- ALTER TABLE command (SQL), 656
- amd (NFS auto-mount daemon), 774-775
- amnesiac (default hostname), 77
- anonymous FTP
  - access, allowing, 617-618
  - files controlling, 614-615
  - overview of, 613
- Anonymous FTP Configuration screen, 617
- Apache
  - MaxClients directive, 721
  - mod_ssl, 699
  - security
    - CGI scripts, 701-702
    - overview of, 698-699
- Apache Project, 577
- Apache Software Foundation and PHP, 669
- Apache Web server
  - access control
    - by address and password, 595
    - groups, adding, 594
    - by hostname/IP address, 590-591
    - overview of, 590
    - by password authentication, 592-593
    - users, adding, 593-594
  - AddHandler directive, 601
  - AddModule directive, 598
  - AddType directive, 602
  - advantages of, 582
  - AllowOverride directive, 586-588
  - CGI
    - enabling, 604-605
    - writing programs, 606-608
  - configuring
    - htaccess file, 586-588
    - httpd.conf file, 585-586
    - overview of, 584-585
    - file layout, 583-584
    - forking model, 588
    - installed support files for, 582
    - LoadModule directive, 598
  - modules
    - building with apxs, 599
    - built-in, 598
    - dynamic, 598
    - mod_perl, 600
    - mod_php, 600
    - mod_python, 600
    - overview of, 597
    - third-party, 599
  - opening, 582
  - overview of, 577-578
  - server-side includes, 600-601, 603
  - starting and stopping HTTP daemon, 588-590
  - virtual hosting, 595-597
- Apache-SSL, 699-701
- apachectl configtest command, 589-590
- apachectl graceful command, 590
- apachectl restart command, 589
- apachectl tool, 589-590
- AppleTalk, 765, 780
- applications
  - availability of, 99
  - dock (WindowMaker)
    - installing, 93-94
    - starting, 94
  - e-mail
    - Mutt, 125
    - overview of, 123
