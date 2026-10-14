# Objective 1—Access and Use man Pages

The most important command for online help is man (an abbreviation of manual or man page). All manual pages are available in English and many have been translated into other languages. Because these translations are often incomplete or not maintained, we recommend using the English versions.

To display the man page of the man command, open the GNOME terminal and enter

```
geeko@da10:~ > man man
```

If the English man pages are not shown automatically with the man command, you can display the English version of the man page by using the variable LANG=en_EN. For example, to display the English version of the man page for the man command, you would enter the following:

```
geeko@da10:~ > LANG=en_EN man man
```

Using the parameter LANG=en_EN switches to the English language for the requested man pages only.

The following is the first page of the manual pages for the man command:

```
man(1)  Manual pager utils  man(1)

NAME
  man an interface to the on-line reference manuals

SYNOPSIS
  man [-c|-w|-tZTdevice] [-adhu7V] [-Msystem[,...]] [-Llocale] [-pstring]
  [-Mpath] [-Ppager] [-rprompt] [-Slist] [-eextension] [[section]page...]

  man -l [-7] [-tZTdevice] [-pstring] [-Ppager] [-rprompt] file...
  man -k [apropos options] regexp
  man -f [whatis options] page ...

DESCRIPTION
  man is the system's manual pager. Each page
  argument given to man is normally the name of
  a program, utility or function. The manual
  page associated with each of these arguments
  is then found and displayed. A section, if
  provided, will direct man to look only in that
  section of the manual. The default action
  is to search in all of the available sections,
  following a pre-defined order and to show
  only the first page found, even if page exists
  in several sections.
```

The header of each manual page contains the command name at the left and right sides and the section number to which the manual page belongs. The center of the header describes the class of programs this program belongs to. The last line usually contains the date of the last changes.