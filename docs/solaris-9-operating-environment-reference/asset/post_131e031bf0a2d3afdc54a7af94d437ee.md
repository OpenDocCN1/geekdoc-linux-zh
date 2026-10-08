
# solregis

## Options

- -c Exit without any dialog displayed if $HOME/.solregis/disable exists, DISABLE=1 is specified in /etc/default/solregis, or the user has already registered.
- -d Delay display of the initial screen until a window manager has asserted control of the X display.

## Exit Status

- 0 Successful completion.
- >0 An error occurred.

## Usage

The following resources can control the behavior and appearance of solregis.

| Name | Class | Value Type | Default |
| --- | --- | --- | --- |
| disable | Disable | Boolean | False |
| localeChoices | LocaleChoices | Int | 1 |
| action0 | Action | String | /usr/dt/bin/hotjava |
| initialURL0 | URL | String | file:///usr/dt/app-config/solregis/EReg.html |
| localeChoice | LocaleChoice | String | null |
| actionn | Action | String | null for 0 |
| initialURLn | URL | String | null for 0 |
| printContext | PrintContext | String | thisorigin |

True if executed in conditional mode, exit without displaying anything.

Specify the number of localeChoice, actionn, and initialURLn sets. The first set is 0, so if localeChoices is 1, localeChoice0, action0, and initialURL0 are the only active resources. If localeChoices is 1, display none of the localeChoices strings and use action0, and so forth. If localeChoices is greater than 1, make each localeChoices string an element in an exclusive locale choice list and apply the index of the selected item controls for the actionn and initialURLn resources.

Specify the string presented to the user for this choice.

# 1294

# solregis

## action/

Specify the file name of the command to be executed (normally expected to be a World Wide Web browser) when you choose Register Now, or specify the special string print. If you specify print, the initialURL string must be a file name on the local system naming a file that is to be printed after prompting for a print destination.

## initialURL/

Specify the argument to be passed to action/ for initial registration. This argument is normally the Uniform Resource Locator for the initial page to be displayed by the World Wide Web browser.

## printContext

Specify the XFN naming context to be displayed if you choose the special print action. For example, if you use the default printContextthisorgunit, display the printers in thisorgunit/service/printer.

## Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of solregis: HOME, LANG, LC_MESSAGES, and NLSPATH.

## Files

- /etc/default/solregis
Default values.
- /$HOME/.solregis/uprops
User registration information.
- /$HOME/.solregis/disable
Users disabled from registration.
- /usr/dt/app-defaults/C/Solregis
Default locale resources.
- /usr/dt/app-defaults/$LANG/Solregis
Default localized resources.
- /etc/dt/app-defaults/C/Solregis
Default installation resources.
- /usr/dt/app-defaults/$LANG/Solregis
Localized installation resources.

## Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWsregu |

- -c Check that the single input file is ordered as specified by the arguments and the collation sequence of the current locale. Set the exit code, and produce no output unless the file is out of sequence.

# 1296

# sort

# /usr/xpg4/bin/sort

- -c Same as /usr/bin/sort, except produce no output under any circumstances.
- -m Merge only. Assume the input files are already sorted.
- -u Sort uniquely by suppressing all but one in each set of lines having equal keys. If used with the -c option, check that there are no lines with duplicate keys, in addition to checking that the input file is sorted.
- -o output Specify the name of an output file to be used instead of the standard output. This file can be as one of the input files.
- -S kmem Specify the maximum amount of swap-based memory for sorting, in kilobytes (the default unit). You can also specify kmem directly as a number of bytes (b), kilobytes (k), megabytes (m), gigabytes (g), or terabytes (t), or as a percentage (%) of the available physical memory.

You can tune performance for a specific scenario with the -S option. However, you should note in particular that sort has greater knowledge of how to use a finite amount of memory for sorting than does the virtual memory system. Thus, a sort invoked to request an extremely large amount of memory with the -S option performs poorly. New in the Solaris 8 release.
- -T directory Specify the name of a directory to use for temporary files. (Obsolete with the Solaris 8 release.) Specify the amount of main memory used initially. Start using that number of kilobytes unless the administrative minimum or maximum is exceeded, in which case you use the corresponding extremus. Thus, -y 0 is guaranteed to start with minimum memory.-y no kmemargument starts with maximum memory. If you omit this option, begin using a system default memory and continue to use more space as needed.
- -z recsz (Obsolete.) Use to prevent termination when lines longer than the system-dependent buffer size are encountered. Because sort automatically allocates buffers large enough to hold the line

## Ordering Options

The default sort order depends on the value of LC_COLLATE. If LC_COLLATE is set to C, sorting is in ASCII. If LC_COLLATE is set to en_US, sorting is case insensitive when two strings are equal. Other locales have none. The following options override the default ordering rules. When ordering options appear independently of any key field, the requested rules are applied globally to all keys. When attached to a specific key, only that field is affected.

- -d Sort in dictionary order. Consider only letters, digits, and blanks (spaces) significant in comparisons.
- -f Fold lowercase letters into upper case.
- -i Ignore nonprintable characters.
- -M Compare as months. Fold the first three nonblank characters of the field to upper case, and compare. For example, in English the sorting order is JAN < FEB < ... DEC. Invalid fields lower than JAN. The -M option implies the -b option
-n Restrict the key to an initial numeric string consisting of optional blank characters, optional minus sign, and zero or more digits with an optional radix character and thousands separators, which is sorted by arithmetic value. An empty digit string is treated as 0. Leading zeros and signs do not affect ordering.
- -r Reverse the sense of comparisons.

## Field Separator Options

You can alter the treatment of field separators using the following options.

- -b Ignore leading blank characters when determining the starting and ending of a restricted sort key. If you specify the -b option before the first sort key, apply it to all sort keys. Otherwise, you can attach the -b option independently to each field-start, field-end, or +pos1 or -pos2 argument.
- -t Use char as the field separator. char is not considered to be part a field (although you can include it in a sort key). Each occurrence of char is significant (for example, char limits empty field). If you do not specify -t, use blank characters as default field separators; each maximal nonempty sequence of blank characters that follows a nonblank character is a field separator.

## Sort Key Options

You can specify sort keys using the following option.

- -k Define a restricted sort key.

The format of this definition:

- -k field-start [type], field-end [type]

where field-start and field-end define a key field restricted to a portion of the line. types is a modifier from the list of characters btrim. The modifier behaves like the b option applies only to the field-start or field-end to which it is attached. Characters within a field are counted from the first nonblank character in the field. (This rule applies separately to first-character and last-character). The other modifiers behave like the corresponding options but only to the key to which
