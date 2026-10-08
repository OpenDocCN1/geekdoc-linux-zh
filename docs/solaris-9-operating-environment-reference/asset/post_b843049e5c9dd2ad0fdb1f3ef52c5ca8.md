
# 858

# mesg

/dev/kmem Kernel virtual memory image device. This device special file is used as the corefile when the live operating system is examined.

/dev/ksyms Kernel symbol table device. This device special file is used as the objectfile when the live operating system is examined.

/proc/pid/* Process information files that are read during examination and control of user processes.

/usr/lib/adb/usr/platform/platform-name/lib/adb Default directories for macro files that are read with the $ and $$ commands. platform-name is the name of the platform, derived either from information in a corefile or crash dump, or from the current machine as by uname -i (see uname(1)).

/usr/lib/mdb/usr/platform/platform-name/lib/mdb Default directories for debugger modules that are loaded with the ::load commands. platform-name is the name of the platform, derived either from information in a corefile or crash dump, or from the current machine as by uname -i (see uname(1)).

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmdb (32 bit) SUNmdbx (64 bit) |
| Interface stability | Evolving |

# See Also

adb(1), cmdtool(1), gcore(1), proc(1), pgrep(1), ps(1), stty(1), truss(1), uname(1), coreadm(1M), dumppadm(1M), savecore(1M), exec(2), fork(2), _lwp_self(2), pipe(2), vfork(2), elf(3ELF), signal(3), signal(3THREAD), libkvm(3LIB), libthread(3LIB), libthread_db(3LIB), signal(3THREAD), thr_self(3THR), threads(3THR), core(4), proc(4), attributes(5), largefile(5), ksyms(7D), mem(7D)

Linker and Libraries Guide

Solaris Modular Debugger Guide

# mesg — Permit or Deny Messages

# Synopsis

```
/usr/bin/mesg [-n | -y | n | y]
```

# mesg

# Description

The mesg command controls whether other users can send messages to a terminal device using write(1), talk(1), or other commands. The terminal device affected is determined by a search for the first terminal in the sequence of devices associated with standard input, standard output, and standard error. With no arguments, mesg reports the current state without changing it. Processes with appropriate privileges may be able to send messages to the terminal independently of the current state.

# Options

+   -n | n
Deny permission to other users to send message to the terminal. See write(1).
- -y | y
Grant permission to other users to send messages to the terminal.

# Examples

The following example uses the mesg command with no arguments to display the current state, and first turns off, then turns on, the ability to receive messages from another terminal.

```
castle mesg
is y
castle mesg -n
castle mesg
is n
castle mesg -y
castle mesg
is y
castle@
```

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of mesg: LC_TYPE, LC_MESSAGES, and NLSPATH.

# Exit Status

+   0 Messages are receivable.
1 Messages are not receivable.
2 Error.

# Files

+   /dev/tty* Terminal devices.
/dev/pts* Terminal devices.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUMwcu |

# 860

# mixerctl

# See Also

talk(1), write(1), attributes(5), environ(5)

# mixerctl — Audio Mixer Control Command-Line Application

# Synopsis

/usr/sbin/mixerctl [-a | -d dev] [-iv] [-e | -o]

# Description

Some audio devices support the audio mixer functionality. Some mixer(7i) for a complete description of the audio mixer. Use the mixerctl command, new in the Solaris 8 Operating Environment, to control the mode of the audio mixer and to get information about the audio mixer and the audio device. Some audio(7i) for details.

# Options

If you specify no options, option -i is assumed.

+   -a Apply the command to all audio devices.

+   -d dev The argument specifies an alternative audio device control for the command to use.

+   -e Enable the audio mixer function if the audio device supports it. If supported, you can enable the audio mixer at any time. If the audio mixer is already enabled, the command silently ignores the option.

+   -i Print the audio device type information for the device and indicate whether the audio device uses the audio mixer. If the device uses the audio mixer, this option displays the audio mixer's mode.

+   -o Turn off the audio mixer function if the audio device supports it. You can turn off the audio mixer, if supported, only if one process has the device opened with the O_RDWR flag or if two processes have the device opened, with the O_RDONLY flag and the other with the O_WRONLY flag. The command silently ignores the disable option if the audio mixer function is already disabled.

+   -v Verbose mode. Print the audio_info_t structure for the device, along with the type information. This option implies the -i option.

# Examples

The following example turns off the audio mixer function.

```
mopoke% mixerctl -o
audio mixer for /dev/audioctl is disabled
```

```
mopoke%
```

The following example enables the audio mixer function.

mopoke% mixerctl -e
Audio mixer for /dev/audictl is enabled

mopoke%

The following example prints information for the audio device.

```
mopoke% mixerctl -i
Device /dev/audictl:
Name = SUNW, audiots
Version = a
Config = onboardi
```

Audio mixer for /dev/audictl is enabled

mopoke%

The following example prints the audio_info_t structure for the device along with the device type information. This option implies the -i option.

```
mopoke% mixerctl -v
Device /dev/audictl:
Name = SUNW, audiots
Version = a
Config = onboardi
```

Audio mixer for /dev/audictl is enabled
Sample Rate

```
Play 48000
Record 48000
Channels 2
Play 2
Record 2
Precision 16
Play 16
Record 16
```

```
Encoding 3 (linear)
Record 3 (linear)
Gain 191
Record 127
Balance 32
Play 32
Record 32
```

```
Port 0x00000003 (SPKR|HDPHONE)
Record 0x00000001 (MIC)
Avail Ports 0x00000007 (SPKR|LINE)
Play 0x00000043 (MIC|LINE|CODEC LOOPBACK)
Record 0x00000005 (SPKR|LINE)
Play 0x00000043 (MIC|LINE|CODEC LOOPBACK)
```

Samples 0
Play 0
Record 0
Active
Play 0
Record 0
Error
Play 0
Record 0
Play 0
Record 0
Count
Play 0
Record 0
Waiting
Play 0
Record 0
Open
Play 0
Record 0
HW Features 0000001
MIXER
0000001
Enabled 0000001
MIXER
0000001
SW Features 0000001
MIXER
0000001
SW Features 0000001
DUPLEX
INPUT 0000001
OUTPUT
0000001
LOOPBACK
0000001
MIXER 0000001
Environment Variables AUDIEDEV If you do not specify the -d and -a options, AUDIEDEV is consulted. If set, AUDIEDEV contains the full path name of the device. If AUDIEDEV is not set, /dev/audioctl is used.

Files /dev/audioctl

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUMwcu |

The following example creates the subdirectory ltr/jan.
castle% mkdir -p ltr/jan
castle% ls -l

rm(1), sh(1), umask(1), intro(2), mkdir(2), attributes(5), environ(5), largefile(5)

# 865

# mkmsgs

mkmsgs — Create Message Files for Use by gettxt

# Synopsis

/usr/bin/mkmsgs [-o] [-i locale] input-strings msgfile

# Description

Use the mkmsgs command to create a file of text strings that can be accessed by gettxt(1), srch(1), exstr(1), and gettxt(3C)). mkmsgs takes as input a file of text strings for a particular locale (see locale(3C)) and creates a file in a format that can be retrieved. By using the -i option, you can install the file under /usr/lib/local/LC_MAGES directory (locale corresponds to the language in which the strings are written). input-strings is the name of the file that contains the original strings. msgfile is the name of the output file where mkmsgs writes the strings. Messages are transformed and copied sequentially from input-strings to msgfile. To generate an empty message in msgfile, leave an empty line at the correct place by editing the input-strings file. Add new strings only at the end of the file; then, create a new msgfile and install it in the correct place. If you do not follow this procedure, the retrieval function retrieves the wrong string and software compatibility will be broken.

# Options

+   -o Overwrite msgfile if it exists.

+   -i locale Install msgfile in the /usr/lib/local/locale/LC_MAGES directory. Create directories under /usr/lib/local if they do not exist. Only someone who is a supervisor or a member of group bin can create or overwrite files in this directory.

# Examples

The following example shows an input message file C.str.

```
File %s:\t cannot be opened\ns: Bad directory\n
```

```
write error\n
```

The following command uses the input strings from C.str to create text strings in the appropriate format for the file UX in the current directory.
