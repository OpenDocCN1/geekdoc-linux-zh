# Examining ps Options

The official syntax for ps is fairly simple:

```
ps [options]
```

This simplicity of form hides considerable complexity because ps supports three different types of options, as well as many options within each type. The three types of options are as follows:

**Unix98 options** These single-character options may be grouped together and are preceded by a single dash (-).

**BSD options** These single-character options may be grouped together and must *not* be preceded by a dash.

**GNU long options** These multicharacter options are not grouped together. They're preceded by two dashes (--).

Options that may be grouped together may be clustered without spaces between them. For instance, rather than typing ps -a -f, you can type ps -af. The reason for so much complexity is that the ps utility has historically varied a lot from one Unix OS to another. The version of ps that ships with major Linux distributions attempts to implement most features from all these different ps versions, so it supports many different personalities. In fact, you can change some of its default behaviors by setting the PS_PERSONALITY environment variable to posix, old, linux, bsd, sun, or digit1, or various others. (Chapter 2 describes how to set environment variables.) The rest of this section describes the default ps behavior on most Linux systems. Table 3.1 summarizes some of the more useful ps features.

# TABLE 3.1 Common ps Options

| Unix98 Option(s) | BSD Option(s) | GNU Long Option(s) | Description |
| :--- | :--- | :--- | :--- |
| | | --help | This option displays a summary of some of the more common ps options. |
| -A, -e | x | | By default, ps displays only processes that were run from its own terminal (xterm, text-mode login, or remote login). The -A and -e options cause it to display all the processes on the system, and x displays all processes owned by the user who gives the command. The x option also increases the amount of information that's displayed about each process. |