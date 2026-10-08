# Environment Options

Modifying the zipinfo default behavior with options in an environment variable is a bit complicated to explain because zipinfo tries to handle various defaults in an intuitive, yet UNIX-like, manner. (Try not to laugh.) zipinfo has three priority levels of options.

+   - Default options.
- Environment options, which can override or add to the defaults.
- Explicit options specified on the command line, which can override or add to either of the above.

The default variable is ZIPINFO_OPTS for VMS (where the symbol used to install zipinfo as a foreign command would otherwise be confused with the environment variable) and ZIPINFO for all other operating systems. With zip, ZIPINFO is also accepted (don't ask). If you define both ZIPINFO and ZIPINPUT, ZIPINFO takes precedence. You can use the unzip diagnostic option (-v with no file name) to check the values of all four possible unzip and zipinfo environment variables.

The default listing format corresponds roughly to the zipinfo -hst command (except when you specify individual files). If you prefer the long format listing (-1), you can change the default by using the ZIPINFO environment variable, as shown below.

```
ZIPINFO=-1 export ZIPINFO

UNIX Bourne shell.

setenv ZIPINFO -1

UNIX C shell.
ZIPINFO=-1

OS/2 or MS-DOS.
def ZIPINFO_OPTS "-1"
```

You can also specify negative options to override defaults. Precede the undesired option with one or more dashes. For example, if you don't like the totals, you can specify -t or --t options. The first dash is the regular switch character, but the second one is also interpreted as a minus sign. This dual use of dashes may seem a little awkward, but it's reasonably intuitive. After the first dash, any other dashes signify a negative option. This syntax is consistent with the behavior of the UNIX nice(1) command.

# Bugs

With unzip, zipinfo -M(more) option is overly simplistic in its handling of output. It fails to detect the wrapping of long lines and scroll lines at the top of the screen before they are read. zipinfo should detect and treat each occurrence of line wrap as an additional line print, which requires knowledge of both the screen width and height. In addition, zipinfo should detect the true screen geometry on all systems.

The multiple listing formats are unnecessarily complex and should be simplified. (That is not to say they will be.)

# Examples

The following example displays a basic, short-format listing of the complete contents of the 085DOC.ZIP archive, with both header and totals lines.