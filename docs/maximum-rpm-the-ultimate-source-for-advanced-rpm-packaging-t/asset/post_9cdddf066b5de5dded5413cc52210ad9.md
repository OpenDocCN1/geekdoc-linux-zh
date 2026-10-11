
volume.c: In function `mix_set_volume':
volume.c:67: warning: implicit declaration of function `ioctl'
90 blocks
82 blocks

This is the entire output from a package build of **cddplayer**. Note that warning messages (actually, anything sent to stdout) are still printed.

### 12.1.17. --rcfile <rcfile>: Set Alternate rpmrc File to <rcfile>

The `--rcfile` option is used to specify a file containing default settings for RPM. Normally, this option is not needed. By default, RPM uses `/etc/rpmrc` and a file named `.rpmrc` located in your login directory.

This option would be used if there were a need to switch between several sets of RPM defaults. Software developers and package builders will normally be the only people using the `--rcfile` option. For more information on *rpmrc* files, see Appendix B.

## 12.2. Other Build-Related Commands

Two other commands also perform build-related functions. However, they do not use the `rpm -b` command syntax we’ve been studying so far. Instead of specifying the name of the spec file, as with `rpm -bi`, it’s necessary to specify the name of the source package file.

Why the difference in syntax? The reason has to do with the differing functions of these commands. Unlike `rpm -b`, where the name of the game is to get software packaged into binary and source package files, these commands use an already-existing source package file as input. Let’s take a look at them in the following sections.

### 12.2.1. `rpm --recompile: What Does It Do?`

The `--recompile` option directs RPM to perform the following steps:

- 1. Install the specified source package file.
- 2. Unpack the original sources.
- 3. Build the software.
- 4. Install the software.
- 5. Remove the software’s build directory structure.

While you might think this sounds a great deal like an install of the source package file, followed by an `rpm -bi`, this is not entirely the case. Using `--recompile`, the only file required is the source package file. After the software is built and installed, the only thing left, other than the newly installed software, is the original source package file.

The `--recompile` option is normally used when a previously installed package needs to be recompiled. `--recompile` comes in handy when software needs to be compiled against a new version of the kernel.

Here's what RPM displays during a `--recompile`:

```
# rpm --recompile cdplayer-1.0-1.src.rpm
Installing cdplayer-1.0-1.src.rpm
  Package: cdplayer
Executing: %prep
 ...
 + exit 0
Executing: %build
 ...
 + exit 0
Executing: %install
 ...
 + exit 0
Executing: special doc
 ...
 + exit 0
Executing: sweep
 ...
 + exit 0
#
```

The very first line shows RPM installing the source package. After that are ordinary executions of the %prep, %build, and %install sections of the spec file. Finally, the cleanup of the software's build directory takes place, just as if the `--clean` option had been specified.

Since `rpm -i` and `rpm -U` are not being used to install the software, the RPM database is not updated during a `--recompile`. This means that doing a `--recompile` on an already-installed package may result in problems down the road, when RPM is used to upgrade or verify the package.

### 12.2.2. rpm `--rebuild`: What Does It Do?

Package builders, particularly those who create packages for multiple architectures, often need to build their packages starting from the original sources. The `--rebuild` option does this, starting from a source package file. Here is the list of steps it performs:

- 1. Install the specified source package file.
- 2. Unpack the original sources.
- 3. Build the software.
- 4. Install the software.
- 5. Create a binary package file.
- 6. Remove the software's build directory tree.

Like the --recompile option, --rebuild cleans up after itself. The only difference between the two commands is that --rebuild also creates a binary package file. The only remnants of a --rebuild are the original source package, the newly installed software, and a new binary package file.

Package builders find this command especially handy because it allows them to create new binary packages using one command, with no additional cleanups required. There are two times when --rebuild is normally used:

- When the build environment (for example, compilers, libraries) has changed.
- When binary packages for a different architecture are to be built.

Here's an example of the --rebuild option in action:

```
# rpm --rebuild cdplayer-1.0-1.src.rpm
Installing cdplayer-1.0-1.src.rpm
* Package: cdplayer
Executing: %prep
...
+ exit 0
Executing: %build
...
+ exit 0
Executing: %install
...
+ exit 0
Executing: special doc
...
+ exit 0
Binary Packaging: cdplayer-1.0-1
...
Executing: %clean
...
+ exit 0
Executing: sweep
...
+ exit 0
#
```

The very first line shows RPM installing the source package. The lines after that are ordinary executions of the %prep, %build, and %install sections of the spec file. Next, a binary package file is created. Finally, the spec file's %clean section (if one exists) is executed. The cleanup of the software's build directory takes place, just as if the --clean option had been specified.

### 12.3. Summary

That completes our overview of the commands used to build packages with RPM. In Chapter 13, “Inside the Spec File,” we’ll look at the various macros that are available and how they can make life easier for the package builder.

## 13

# Inside the Spec File

In this chapter, we’re going to cover the spec file in detail. There are a number of different types of entries that comprise a spec file, and every one will be documented here. The different types of entries are

- Comments—Human-readable notes ignored by RPM.
- Tags—Data definitions.
- Scripts—A set of commands to be executed at specific times.
- Macros—A method of executing multiple commands easily.
- The %files list—A list of files to be included in the package.
- Directives—Used in the %files list to direct RPM to handle certain files in a specific way.
- Conditionals—Permit operating system— or architecture-specific preprocessing of the spec file.

Let’s start by looking at comments.

### 13.1. Comments: Notes Ignored by RPM

Comments are a way to make RPM ignore a line in the spec file. The contents of a comment line are entirely up to the person writing the spec file.

To create a comment, enter an pound sign (#) at the start of the line. Any text following the comment character will be ignored by RPM. Here’s an example of a comment:

```
# This is the spec file for playmidi 2.3...
```

Comments can be placed in any section of the spec file.

### 13.2. Tags: Data Definitions

Looking at a spec file, the first thing you’ll see are a number of lines, all following the same basic format:

```
<something>: <something-else>
```

*<something>* is known as a *tag* because it is used by RPM to name or tag some data. The tag is separated from its associated data by a colon. The data is represented by *<something-else>*. Tags are grouped together at the top of the spec file, in a section known as the *preamble*. Here’s an example of a tag and its data:

Vendor: White Socks Software, Inc.

In this example, the tag is *Vendor*. Tags are not case sensitive—they may be all uppercase, all lowercase, or anything in between. The *Vendor* tag is used to define the name of the organization producing the package. The data in this example is White Socks Software, Inc.. Therefore, RPM will store White Socks Software, Inc. as the vendor of the package.

Note also that spacing between the tag, the colon, and the data is unimportant. Given this, and the case insensitivity of the tag, each of the following lines is equivalent to the previous example:

VendOr : White Socks Software, Inc. 

vendor:White Socks Software, Inc. 

VENDOR : White Socks Software, Inc.

The bottom line is that you can make tag lines as neat or as ugly as you like—RPM won't mind either way. Note, however, that the tag's data might need to be formatted in a particular fashion. If there are any such restrictions, we'll mention them. The following sections group together tags of similar functions for easier reference, starting with the tags used to create the package name.

#### 13.2.1. Package Naming Tags

The following tags are used by RPM to produce the package's final name. Since the name is always in this format:

```
<name>-<version>-<release>
```

it's only natural that the three tags are known as name, version, and release.

##### 13.2.1.1. The name Tag

The name tag is used to define the name of the software being packaged. In most (if not all) cases, the name used for a package should be identical in spelling and case to the software being packaged. The name cannot contain any whitespace: If it does, RPM will only use the first part of the name (up to the first space). Therefore, if the name of the software being packaged is cdplayer, the name tag should be something like this:

```
Name: cdplayer
```

##### 13.2.1.2. The version Tag

The version tag defines the version of the software being packaged. The version specified should be as close as possible to the format of the original software's version. In most cases, there should be no problem specifying the version just as the software's original developer did. However, there is a restriction: There can be no dashes in the version. If you forget, RPM will remind you:

```
# rpm -ba cdplayer-1.0.spec
Package: cdplayer
Illegal '-' char in version: 1.0-a
```
