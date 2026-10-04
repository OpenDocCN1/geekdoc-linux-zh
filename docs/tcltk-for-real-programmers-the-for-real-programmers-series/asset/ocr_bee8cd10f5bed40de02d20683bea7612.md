# 13.2 Expect

# 13.2 Expect

| Language | C |
| Primary Site | http://expect.nist.gov/
| Contact | libes@nist.gov, Don Libes |
| Tcl Revision Supported | Tcl: 7.3-8.0p2 Tk: 3.6-8.0p2 |
| Supported Platforms | Unix |

Unofficially Supported Platforms Windows NT: http://bmrc.berkeley.edu/people/chaffee/expectnt.html

Other Book References Exploring Expect, Tcl/Tk Tools

Expect adds commands to Tcl that make it easy to write scripts to interact with programs that use a character-based interface. This includes programs such as telnet and FTP that use a prompt/command type interface or even keyboard-driven spreadsheet packages as sc.

Expect can be used for tasks ranging from changing passwords on remote systems to converting an interactive hardware diagnostics package into an automated test system. When you link the expect extension with the Tk libraries, you get an interpreter (expecttk) that is ideal for adding a GUI to dialog-based programs.

There are three indispensable new commands in expect:

```
Syntax: spawn options commandName commandArgs
```

+   * spawn Starts a new process and connects the process's stdout to the expect interpreter.
* options The spawn command supports several options, including
  * -noecho The spawn will echo the command line and arguments unless this option is set.
  * -openfileID The -open option lets you to process the input from a file handle (returned by