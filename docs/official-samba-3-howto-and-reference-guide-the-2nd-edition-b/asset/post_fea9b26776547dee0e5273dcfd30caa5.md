
## REPORTING BUGS

### 39.1 Introduction

Please report bugs using Samba’s Bugzilla[1] facilities and take the time to read this file before you submit a bug report. Also, check to see if it has changed between releases, as we may be changing the bug reporting mechanism at some point.

Please do as much as you can yourself to help track down the bug. Samba is maintained by a dedicated group of people who volunteer their time, skills, and efforts. We receive far more mail than we can possibly answer, so you have a much higher chance of a response and a fix if you send us a “developer-friendly” bug report that lets us fix it fast.

If you post the bug to the comp.protocols.smb newsgroup or the mailing list, do not assume that we will read it. If you suspect that your problem is not a bug but a configuration problem, it is better to send it to the Samba mailing list, as there are thousands of other users on that list who may be able to help you.

You may also like to look though the recent mailing list archives, which are conveniently accessible on the Samba Web pages at <http://samba.org/samba/>.

### 39.2 General Information

Before submitting a bug report, check your config for silly errors. Look in your log files for obvious messages that tell you’ve misconfigured something. Run testparm to check your config file for correct syntax.

Have you looked through Chapter 37, “The Samba Checklist”? This is extremely important. If you include part of a log file with your bug report, then be sure to annotate it with exactly what you were doing on the client at the time and exactly what the results were.

[1] https://bugzilla.samba.org/

### 39.3 Debug Levels

If the bug has anything to do with Samba behaving incorrectly as a server (like refusing to open a file), then the log files will probably be quite useful. Depending on the problem, a log level of between 3 and 10 showing the problem may be appropriate. A higher level gives more detail but may use too much disk space.

To set the debug level, use the `log level` in your `smb.conf`. You may also find it useful to set the log level higher for just one machine and keep separate logs for each machine. To do this, add the following lines to your main `smb.conf` file:

```
log level = 10
log file = /usr/local/samba/lib/log.%m
include = /usr/local/samba/lib/smb.conf.%m
```

and create a file `/usr/local/samba/lib/smb.conf.machine` where *machine* is the name of the client you wish to debug. In that file put any `smb.conf` commands you want: for example, `log level` may be useful. This also allows you to experiment with different security systems, protocol levels, and so on, on just one machine.

The `smb.conf` entry `log level` is synonymous with the parameter *debuglevel* that has been used in older versions of Samba and is being retained for backward compatibility of `smb.conf` files.

As the `log level` value is increased, you will record a significantly greater level of debugging information. For most debugging operations, you may not need a setting higher than 3. Nearly all bugs can be tracked at a setting of 10, but be prepared for a large volume of log data.

### 39.3.1 Debugging-Specific Operations

Samba-3.x permits debugging (logging) of specific functional components without unnecessarily cluttering the log files with detailed logs for all operations. An example configuration to achieve this is shown in:

```
log level = 0 tdb:3 passedb:5 auth:4 vfs:2
max log size = 0
log file = /var/log/samba/%U.%m.log
```

This will cause the level of detail to be expanded to the debug class (log level) passed to each functional area per the value shown above. The first value passed to the `log level` of 0 means turn off all unnecessary debugging except the debug classes set for the functional areas as specified. The table shown in Table 39.1 may be used to attain very precise analysis of each SMB operation Samba is conducting.

**Table 39.1 Debuggable Functions**

| Function Name | Function Name |
| :--- | :--- |
| all | passdb |
| tdb | sam |
| printdrivers | auth |
| lmanman | winbind |
| smb | vfs |
| rpc_parse | idmap |
| rpc_srv | quota |
| rpc_cli | acl |

### 39.4 Internal Errors

If you get the message “INTERNAL ERROR” in your log files, it means that Samba got an unexpected signal while running. It is probably a segmentation fault and almost certainly means a bug in Samba (unless you have faulty hardware or system software).

If the message came from smbd, it will probably be accompanied by a message that details the last SMB message received by smbd. This information is often useful in tracking down the problem, so please include it in your bug report.

You should also detail how to reproduce the problem, if possible. Please make this reasonably detailed.

You may also find that a core file appeared in a **corefiles** subdirectory of the directory where you keep your Samba log files. This file is the most useful tool for tracking down the bug. To use it, you do this:

```
$ gdb smbd core
```

adding appropriate paths to smbd and core so gdb can find them. If you do not have gdb, try dbx. Then within the debugger, use the command **where** to give a stack trace of where the problem occurred. Include this in your report.

If you know any assembly language, do a **disass** of the routine where the problem occurred (if it’s in a library routine, then disassemble the routine that called it) and try to work out exactly where the problem is by looking at the surrounding code. Even if you do not know assembly, including this information in the bug report can be useful.

### 39.5 Attaching to a Running Process

Unfortunately, some UNIXes (in particular some recent Linux kernels) refuse to dump a core file if the task has changed UID (which smbd does often). To debug with this sort of system, you could try to attach to the running process using `gdb smbd PID`, where you get `PID` from `smbstatus`. Then use `c` to continue and try to cause the core dump using the client. The debugger should catch the fault and tell you where it occurred.

Sometimes it is necessary to build Samba binary files that have debugging symbols so as to make it possible to capture enough information from a crashed operation to permit the Samba Team to fix the problem.

Compile with `-g` to ensure you have symbols in place. Add the following line to the `smb.conf` file global section:

```
panic action = "/bin/sleep 90000"
```

to catch any panics. If `smbd` seems to be frozen, look for any sleep processes. If it is not, and appears to be spinning, find the `PID` of the spinning process and type:

```
root# gdb /usr/local/samba/sbin/smbd
```

then “attach ‘`pid`’” (of the spinning process), then type “`bt`” to get a backtrace to see where the `smbd` is in the call path.

### 39.6 Patches

The best sort of bug report is one that includes a fix! If you send us patches, please use `diff -u` format if your version of `diff` supports it; otherwise, use `diff -c4`. Make sure you do the diff against a clean version of the source and let me know exactly what version you used.

## Part VI Reference Section

## HOW TO COMPILE SAMBA

You can obtain the Samba source file from the Samba Web site[1]. To obtain a development version, you can download Samba from Subversion or using **rsync**.

### 40.1 Access Samba Source Code via Subversion

#### 40.1.1 Introduction

Samba is developed in an open environment. Developers use a Subversion to “checkin” (also known as “commit”) new source code. Samba’s various Subversion branches can be accessed via anonymous Subversion using the instructions detailed in this chapter.

This chapter is a modified version of the instructions found at the Samba[2] Web site.

#### 40.1.2 Subversion Access to samba.org

The machine **samba.org** runs a publicly accessible Subversion repository for access to the source code of several packages, including Samba, rsync, distcc, ecache, and jitterbug. There are two main ways of accessing the Subversion server on this host.

##### 40.1.2.1 Access via SVNweb

You can access the source code via your favorite WWW browser. This allows you to access the contents of individual files in the repository and also to look at the revision history and commit logs of individual files. You can also ask for a diff listing between any two versions on the repository.

Use the URL `<http://svnweb.samba.org/>`.

[1] <http://samba.org/>
[2] <http://samba.org/samba/subversion.html>
