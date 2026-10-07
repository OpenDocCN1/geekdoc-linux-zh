
## Automatic System-specific Configuration

After the `wine.conf` file has been successfully built, the `Configure` utility proceeds to make changes to the source tree via the `xkmf`. `xkmf` is a utility that creates makefiles for X Window and creates a `Makefile` from an `Imakefile` while taking into account the peculiarities of different X Window installations across UNIX-like platforms.

## How to Build Wine

To build Wine, simply type:

```bash
make
```

You're done with the hard part of configuring Wine. However, building Wine seems like the longest part. To build Wine from scratch takes approximately eight minutes on a 90 MHz Pentium. You will also need the `-lxext` libraries for the final link to work, so install it from your CD-ROM first.

## Using Wine

Using Wine can be as simple as typing `wine filename`. Wine can be configured and used with a number of different options—including a debugger for tracking down internal errors in Wine itself.

## Specifying Configuration Parameters

Wine's global configuration file is typically `/usr/local/etc/wine.conf`. The configuration parameters match mostly with the above questions and are organized in the format of MS-Windows `.ini` files. A sample file follows, with some comments on the usage of each section.

The following statements map MS-DOS drive letters to the matching subdirectory under Linux:

```ini
[drives]
A=/a
C=/c
```

These parameters tell Wine where to find Windows- and Wine-specific DLLs and directories:

```ini
[wine]
Windows=c:\\windows
System=c:\\windows\\system
Temp=c:\temp
Path=c:\windows;c:\windows\system
SystemResources=/users/wine/wine950122/sysres.dll
```

The following section applies to the mapping of MS-Windows fonts to X font (note that the * is used for wildcard matching of X fonts):

```ini
[fonts]
system=*-helvetica
mssansserif=*-helvetica
msserif=*-times
fixedsys=*-fixed
arial=*-helvetica
helv=*-helvetica
roman=*-times
default=*-*
```

The following section maps serial ports available under Wine with corresponding Linux serial port identifiers:

```ini
[serialports]
Com1=/dev/cua0
Com2=/dev/cua1
```

The following section maps printer ports available under Wine with the corresponding printer port under Linux:

```ini
[parallelports]
Lpt1=/dev/lp0
```

These parameters determine the amount of logging and the destination:

```ini
[spy]
File=CON
Exclude=WM_SIZE;WM_TIMER
```

## Using Command-Line Options

The Wine command line has the following format:

`wine wine_options program program_options`

For example:

```bash
bash# /usr/wine/wine -debugmsg +all /c/windows/winmine.exe
```

Table 59.1 shows command-line options available with Wine.

### TABLE 59.1. WINE COMMAND-LINE OPTIONS

| Option | Meaning |
| :--- | :--- |
| `-depth n` | Change the depth to use for multiple-depth screens. This configures Wine to use other than the default number of colors. (8 bitplanes is 256 colors and usually the only acceptable answer.) |
| `-desktop geom` | Run an MS-Windows application with a desktop of the size specified. For example, 850*620 would create a window of 850 by 620. Running with a desktop also eliminates the modal, or stuck-on-top, behavior of Wine applications. |
| `-display name` | Use an X display other than the default. This enables users to run an MS-Windows application on another X device over an attached network. |
| `-iconic` | Start application as an icon rather than full-screen. This is same functionality as run minimized from the Program Manager under native MS-Windows. |
| `-debug` | Enter debugger before starting application. |
| `-name name` | Set the application name. This is useful for telling the X Window manager a meaningful name for the application. The default name is wine. |
| `-privatemap` | Use a private color map. This is useful for applications that make extensive use of color. Running an application this way causes the colors of other X applications to look weird while the Wine session is the selected window. |
| `-synchronous` | Turn on synchronous display mode. This can severely slow down applications because it causes X Window to wait for the completion of each command before sending the next one. X applications can send commands to an X server that may or may not be on the same machine. Under some applications, synchronization is necessary so that graphics operations do not get optimized away by the X server. |
| `-backingstore` | This is an optimization that enables an X server to handle expose events without interrupting the client program. |
| `-spy file` | Turn on message spying to the specified file. This can also be done by output redirection. |
| `-debugmsg name` | Turn specific debugging information on or off. To get a current list of debug message types, enter the following command: `wine -debugmsg help help`. |

## The Wine Debugger

Wine has a built-in debugger that is useful for uncovering problems within the program. When an MS-Windows program exits due to a problem, the debugger starts in the xterm from which Wine was started. If you are not interested in troubleshooting Wine, simply type `quit` at the prompt and skip to the next section of this chapter.

The Wine debugger is similar to the GNU debugger `gdb`. Breakpoints can be set; examination and modification of registers as well as memory locations are possible. However, the following is a minimal debugger that includes only the commands listed in Table 59.2.

### Table 59.2. WINE DEBUGGER COMMANDS

| Command | Meaning |
| :--- | :--- |
| `break` | Set a breakpoint at a specified address or symbolic value. Wine will stop before executing instructions at this address. For example, `break * GDI_Ordinal_24` sets a breakpoint at the start of Windows Ellipse function known internally as `GDI.24`. |
| `bt` | Backtrace, or show the history of Wine calls leading to the current place. The addresses shown are the return addresses, not the calling addresses. |
| `cont` | Continue program execution until a breakpoint or error condition is reached. |
| `define` | Equates a symbol to a value. For example: `define myproc 0x00001c6.` |
| `disable` | Disable a specific breakpoint. Breakpoints defined by the `break` command are stored by breakpoint numbers. To disable a breakpoint, find the breakpoint number with the `info` command. To disable breakpoint number 1, simply type `disable 1`. |
| `enable` | Enables a breakpoint number, the opposite of `disable`. To enable the previously disabled breakpoint number 1, simply type `enable 1`. |
| `help` | Prints a help text of the available commands. |
| `info` | Provides information on the following:<br><br>`reg` registers information.<br><br>`stack` dumps the current stack.<br><br>`break` shows the current breakpoints and whether they are enabled.<br><br>`segments` shows information about memory segments in use. |
| `mode` | Switches between 16- and 32-bit modes. |
| `print` | Prints out values of expressions given. |
| `quit` | Exits debugger and ends any MS-Windows program in progress. |
| `set` | Enables depositing of values in registers and memory. |
| `symbolfile` | Loads a symbol file containing symbolic values. The file `wine.sym` is created as part of the Wine build. |
| `x` | Examines memory values in several different formats. The format of `x` is `x / format address`, where `format` can be one of the following:<br>- `x`: longword hexadecimal (32-bit integer)<br>- `d`: longword decimal<br>- `w`: word hexadecimal<br>- `b`: byte<br>- `c`: single character<br>- `s`: null-terminated ASCII string<br>- `I`: i386 instruction |

A number can be specified before the `format` to indicate a repeating group. For example, listing 10 instructions after a given address would be `x / 10 I 0x000001cd`.

In order to benefit from using the Wine debugger, an understanding of debugging i386 assembly is essential. If you are serious about debugging Wine, an assembly language output from GCC is essential.

## How Wine Works

Wine is composed of a MS-Windows program loader and a library of MS-Windows functions.

### How Wine Loads Programs

Wine's first duty is to load an MS-Windows executable image into memory. This also includes any DLL files and other resources that the application needs. MS-Windows uses a different executable image type than DOS which is called NE, or new executable. DLLs and font files also use this NE format, which makes Wine's job easier.
