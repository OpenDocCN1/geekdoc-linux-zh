
## AUTHORS

- Juan Antonio Martinez

## SEE ALSO

`pam_pkcs11(8)`, `polkit-1(8)`, PAM-PKCS11 User Manual

## PKMON

### NAME

`pkmon` - PackageKit console client

### SYNOPSIS

**pkmon** [search] [debuginstall] [remove]

### DESCRIPTION

This manual page documents briefly the **pkmon** command.

**pkmon** is the command line client for PackageKit.

### RETURN VALUES

- **0**
  Success
- **1**
  Failed with miscellaneous internal error.

### SEE ALSO

`pkcon(1)`.

The programs are documented fully on [the Gnome Web site](https://www.gnome.org/).

### AUTHOR

This manual page was written by Richard Hughes <richard@hughsie.com>.

## PKTTYAGENT

### NAME

`pkttyagent` - Textual authentication helper

### SYNOPSIS

`pkttyagent` [--version] [--help]

`pkttyagent` [--process *pid* | --system-bus-name *busname*] [--notify-fd *fd*] [--fallback]

### DESCRIPTION

**pkttyagent** is used to start a textual authentication agent for the subject specified by either **—process** or **—system-bus-name**. If neither of these options are given, the parent process is used.

To get notified when the authentication agent has been registered either listen to the Changed D-Bus signal or use **—notify-fd** to pass the number of a file descriptor that has been passed to the program. This file descriptor will then be closed when the authentication agent has been successfully registered.

If **—fallback** is used, the textual authentication agent will not replace an existing authentication agent.

### RETURN VALUE

If the authentication agent could not be registered, **pkttyagent** exits with an exit code of 127. Diagnostic messages are printed on standard error.

If one or more of the options passed are malformed, **pkttyagent** exits with an exit code of 126. If stdin is a tty, then this manual page is also shown.

If the authentication agent was successfully registered, **pkttyagent** will keep running, interacting with the user as needed. When its services are no longer needed, the process can be killed.

### NOTES

Since process identifiers can be recycled, the caller should always use *pid*,*pid-start-time* when using the **—process** option. The value of *pid-start-time* can be determined by consulting e.g. the `/proc` file system depending on the operating system. If only *pid* is passed to the **—process** option, then **pkttyagent** will look up the start time itself but note that this may be racy.

### AUTHOR

Written by David Zeuthen <davidz@redhat.com> with a lot of help from many others.

### BUGS

Please send bug reports to either the distribution or the polkit-devel mailing list, see the link on how to subscribe.

### SEE ALSO

`polkit(8)`, `polkit(8)`, `pkexec(1)`, `pkcheck(1)`, `pkaction(1)`

## PL2PM

### NAME

`pl2pm` - Rough tool to translate Perl4 .pl files to Perl5 .pm modules.

### SYNOPSIS

`pl2pm` *files*

### DESCRIPTION

`pl2pm` is a tool to aid in the conversion of Perl4-style .pl library files to Perl5-style library modules. Usually, your old .pl file will still work fine and you should only use this tool if you plan to update your library to use some of the newer Perl 5 features, such as AutoLoading.

### LIMITATIONS

It’s just a first step, but it’s usually a good first step.

### AUTHOR

Larry Wall <larrymwall@gmail.com>

## PLDD

### NAME

`pldd` - display dynamic shared objects linked into a process

### SYNOPSIS

`pldd` *pid*

`pldd` *option*

### DESCRIPTION

The **pldd** command displays a list of the dynamic shared objects that are linked into the process with the specified process ID. The list includes the libraries that have been dynamically loaded using `dlopen(3)`.

### OPTIONS

- `-, --help`
  Display program help message.
- `--usage`
  Display a short usage message.
- `-V, --version`
  Display the program version.

### VERSIONS

**pldd** is available since glibc 2.15.

### CONFORMING TO

The **pldd** command is not specified by POSIX.1. Some other systems have a similar command.

### EXIT STATUS

On success, **pldd** exits with the status 0. If the specified process does not exist, the user does not have permission to access its dynamic shared object list, or no command-line arguments are supplied, **pldd** exits with a status of 1. If given an invalid option, it exits with the status 64.

### EXAMPLE

```bash
$ echo $$ # Display PID of shell 1143
$ pldd $$ # Display DSOs linked into the shell
1143:
/usr/bin/bash
linux-vdso.so.1
/lib64/libtinfo.so.5
/lib64/libdl.so.2
/lib64/libc.so.6
/lib64/ld-linux-x86-64.so.2
/lib64/libnss_files.so.2
```

### NOTES

The command

```bash
ls -l /proc/PID
```

also shows output that includes the dynamic shared objects that are linked into a process.

### SEE ALSO

`cat(1)`, `ls(1)`, `dlopen(3)`, `proc(8)`

### COLOPHON

This page is part of release 4.00 of the Linux *man-pages* project. A description of the project, information about reporting bugs, and the latest version of this page, can be found at [https://www.kernel.org/doc/man-pages/](https://www.kernel.org/doc/man-pages/).

## PMAP

### NAME

`pmap` - report memory map of a process

### SYNOPSIS

`pmap` [options] *pid* […]

### DESCRIPTION

The `pmap` command reports the memory map of a process or processes.

### OPTIONS

- `-x, --extended`
  Show the extended format.
- `-d, --device`
  Show the device format.
- `-q, --quiet`
  Do not display any header or footer lines.
- `-A, --range` *low,high*
  Limit results to the given range between *low* and *high* address range. Notice that the low and high arguments are single string separated with comma.
- `-X`
  Show even more details than the *-x* option. WARNING: format changes according to */proc/PID/smaps*
- `-XX`
  Show everything the kernel provides
- `-p, --show-path`
  Show full path to files in the mapping column
- `-c, --read-rc`
  Read the default configuration
- `-C, --read-rc-from` *file*
  Read the configuration from *file*
- `-n, --create-rc`
  Create new default configuration
- `-N, --create-rc-to` *file*
  Create new configuration to *file*
- `-h, --help`
  Display help text and exit.
- `-V, --version`
  Display version information and exit.

### EXIT STATUS

- `0`
  Success.
- `1`
  Failure.
- `42`
  Did not find all processes asked for.

### SEE ALSO

`proc(5)`, `top(1)`

### STANDARDS

No standards apply, but pmap looks an awful lot like a SunOS command.

### REPORTING BUGS

Please send bug reports to [bug-pmap@bugs.debian.org](mailto:bug-pmap@bugs.debian.org)

## POD2HTML

### NAME

`pod2html` - convert .pod files to .html files

### SYNOPSIS

```bash
pod2html --help --version --html_root=<name> --html_path=<URL> --infile=<name> --outfile=<name> --
podpath=<name>:...:<name> --podroot=<name> --cachedir=<name> --flush --recurse --
norecurse --quiet --noquiet --verbose --noverbose --index --noindex --
backlink --nobacklink --header --noheader --poderrors --nopoderrors --css=
<URL> --title=<name>
```

### DESCRIPTION

Converts files from `pod` format (see `perlpod`) to `HTML` format.

### ARGUMENTS

`pod2html` takes the following arguments:

- **help**
  - `--help`
  Displays the usage message.
- **html_dir**
  - `--html_dir=<name>`
  Sets the directory to which all cross references in the resulting HTML file will be relative. Not passing this causes all links to be absolute since this is the value that tells `Pod::Html` the root of the documentation tree.
  Do not use this and `--html_root` in the same call to `pod2html`; they are mutually exclusive.
- **html_root**
  - `--html_root=<URL>`
  Sets the base URL for the HTML files. When cross-references are made, the HTML root is prepended to the URL.
  Do not use this if relative links are desired; use `--html_dir` instead.
  Do not pass both this and `--html_dir` to `pod2html`; they are mutually exclusive.
- **infile**
  - `--infile=<name>`
  Specify the pod file to convert. Input is taken from STDIN if no infile is specified.
- **outfile**
  - `--outfile=<name>`
  Specify the HTML file to create. Output goes to STDOUT if no outfile is specified.
- **podroot**
  - `--podroot=<name>`
  Specify the base directory for finding library pods.
- **podpath**
  - `--podpath=<name>:...:<name>`
  Specify which subdirectories of the podroot contain pod files whose HTML converted forms can be linked-to in cross-references.
- **cachedir**
  - `--cachedir=<name>`
  Specify which directory is used for storing cache. Default directory is the current working directory.
- **flush**
  - `--flush`
