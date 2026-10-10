# # DISTFILES

The distfile contains a sequence of entries that specify the files to be copied, the destination hosts, and what operations to perform to do the updating. Each entry has one of the following formats.

```
<variable na> '=' <na list> [ label: ] <source list> `->' <destination list> <command list> [ label: ] <source list> `::' <ti_stamp file> <command list>
```

The first format is used for defining variables. The second format is used for distributing files to other hosts. The third format is used for making lists of files that have been changed since so given date. The source list specifies a list of files and/or directories on the local host which are to be used as the master copy for distribution. The destination list is the list of hosts to which these files are to be copied. Each file in the source list is added to a list of changes if the file is out of date on the host which is being updated (second format) or the file is newer than the ti stamp file (third format).

Labels are optional. They are used to identify a command for partial updates.

Newlines, tabs, and blanks are only used as separators and are otherwise ignored. Comnts begin with '#' and end with a newline.

Variables to be expanded begin with '$' followed by one character or a na enclosed in curly braces (see the examples at the end).

The source and destination lists have the following format: <na> or `(' <zero or more nas separated by white-space> ')' These simple lists can be modified by using one level of set addition, subtraction, or intersection like this: list '-' list or list '+' list or list '&' list If additional modifications are needed (e.g., "all servers and client machines except for the OSF/1 machines") then the list will have to be explicitly constructed in steps using "temporary" variables.

The shell ta-characters '[', ']', '{', '}', '*', and '?' are recognized and expanded (on the local host only) in the sa way as (1). They can be escaped with a backslash. The '~' character is also expanded in the sa way as csh but is expanded separately on the local and destination hosts. When the -owhole option is used with a file na that begins with '~', everything except the ho directory is appended to the destination na. File nas which do not begin with '/' or '~' use the destination user's ho directory as the root directory for the rest of the file na.

The command list consists of zero or more commands of the following format.

```
'install' <options> opt_dest_na ';' 'notify' <na list> ';' 'except' <na list> ';' 'except_pat' <pattern list> ';' 'special' <na list> string ';' 'cmspecial' <na list> string ' ;'
```

The install command is used to copy out of date files and/or directories. Each source file is copied to each host in the destination list. Directories are recursively copied in the sa way.