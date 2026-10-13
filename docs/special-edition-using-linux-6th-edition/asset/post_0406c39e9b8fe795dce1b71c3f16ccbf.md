
Unfortunately, rpm uses a percent sign to indicate both section identifiers and directives in the %Prep and %Files sections, which can be confusing. Some packagers capitalize the first letter of section identifiers and leave directive names in all lowercase to distinguish the two in their spec files, but this is not universal.

Most sections in the spec file contain shell scripts that perform the actions required for that stage of the build process. If you are not familiar with shell scripting, you might want to refer to the “Shell Programming” section in Chapter 14, “Customizing Your Shell Environment.”

## SECTIONS USED DURING THE BUILD PROCESS

The following sections are used during the build process:

- **%Prep** — This section contains a shell script to extract the source files and apply the patches. It is used during the prep stage.
- **%Build** — This contains a shell script to build (compile) the software. It is used during the build stage.
- **%Install** — This contains a shell script to install the software. This is used during the Install stage. (You can probably see a pattern emerging here!)
- **%Files** — This section contains a listing of the files and directories in the package.
- **%Clean** — This optional section contains a shell script to clean up after a package build.
- **%Changelog** — This contains changelog information about the SPEC file itself.

## SECTIONS FOR PACKAGE SCRIPTS

The following scripts are not used at build time; they are inserted into the package and used by the package manager on the end user’s system when the package is installed, removed, or verified.

- **%Pre/%Post** — Scripts to run on the end user’s system before and after installing the package files
- **%Preun/%Postun** — Scripts to run on the end user’s system before and after removing the package files
- **%Triggerin/%Triggerun** — Scripts to run when a specific package is installed and uninstalled. For example, these could be used by a mail client to add sendmail support whenever sendmail is installed.
- **%Triggerpostun** — Script to run after a specific package is uninstalled (versus before the package is uninstalled in the case of %Triggerun).
- **%Verify** — Contains a script run on the end user’s system to verify the package files. If empty, the default verification mechanism of RPM is used.

## HELPER PACKAGES

It is common to have helper packages defined in a spec file. For example, if a package mypackage also has a mypackage-devel package, both will be described in the same spec file.

Generally, the only thing that differs in the helper packages is the list of files and the information fields. To define the information fields for a helper package, the spec file uses the `%package` directive followed by the fields. After that, sections use the package’s name to differentiate—for example,

```spec
%package devel
Summary: Development files for applications which will manipulate RPM packages.
Group: Development/Libraries
%ifos linux
Requires: python >= 1.5.1
%endif
%description devel
This package contains the RPM C library and header files. These development files
will simplify the process of writing programs which manipulate RPM packages and
databases and are intended to make it easier to create graphical package managers
or any other tools that need an intimate knowledge of RPM packages in order to
function.
```

## BUILDING A PACKAGE

Use the -b option with rpm to build packages. You can use other options with this command to perform only certain stages of the build process. This is useful for debugging the build process for a package. Table 17.2 lists the build options and the stages that they refer to.

**Table 17.2  RPM Build Options**

| Option | Stage, or Action |
|---|---|
| `p` | Prep |
| `c` | Build (compile) |
| `i` | Install |
| `b` | Packaging (create a binary package) |
| `a` | All (build binary and source packages) |
| `l` | Check file list |
| `--short-circuit` | Only execute this stage (not preceding ones) |

## THE PREP STAGE

During the prep stage of the package build, the script in the %prep section of the spec file is run. This script will extract the source files from the TAR file and apply patches in preparation for the actual compilation of the software.

During this stage, a directory is created under /usr/src/distribution/BUILD. This is where the files are placed and where other stages will operate.

You can use any commands you need to prepare the source files in the BUILD directory. However, two special directives handle most of the actions that need to be performed. The %setup directive is used to extract the source files listed in the Source lines. The %patch directive is used to apply the patches listed in the Patch lines.

## THE BUILD STAGE

The build stage is where rpm actually compiles the software for your system, using the script in the %Build section. Often this script includes running programs such as configure to set up the software build environment, and make to actually compile the software.

No special directives are available for this section of the spec file. However, rpm sets several shell variables that have values that might be useful for this script.

The following shell variables are available for your use throughout the scripts in the spec file:

- **RPM_SOURCE_DIR** — Location of RPM sources directory. This is `/usr/src/distribution/` sources by default, but can be overridden by configuration values in `/etc/rpmrc` or `~/.rpmrc`.
- **RPM_BUILD_DIR** — Location of RPM BUILD directory. This is `/usr/src/distribution/BUILD` by default. This can also be overridden.
- **RPM_DOC_DIR** — Location at which the document directory for this package is placed. The default value is `/usr/doc`.
- **RPM_OPT_FLAGS** — String of compiler options for producing optimized code for the target architecture (i386). This is often used with make during the compilation of the software.
- **RPM_OS** — String indicating the OS (not just Linux!) used during the build process.
- **RPM_ARCH** — String indicating the architecture during the build process.
- **RPM_ROOT_DIR** — Root directory used during all steps of the build process.
- **RPM_BUILD_ROOT** — Root directory used for the install and packaging stages of the build process.
- **RPM_PACKAGE_NAME** — The name of the package.
- **RPM_PACKAGE_VERSION** — The version of the software in the package.
- **RPM_PACKAGE_RELEASE** — The release of the package.

## THE INSTALL STAGE

During the install stage, the commands are run to actually install the software onto your system. At the end of this stage, the software will be installed on your system, compiled, formatted, and ready to run, exactly as it needs to be on an end user’s system. The shell script to perform this is found in the %Install section of the spec file.

The files put in a package during the packaging stage (described in the next section) are taken from their regular positions in the working filesystem. Their placement, ownership, and permissions are recorded in the package so that they will have those same attributes on the user’s system when the package is installed. Thus, it is critical that the install stage sets up the files completely and properly.

## THE PACKAGING STAGE

During this stage, the package files (binary and source RPMs) are actually created. The files that were placed into your filesystem during the install stage are collected and placed into the binary package file, along with information from the spec file. Then all the materials used to produce the package are collected and bundled together into a source RPM package, which can be used (with a similar set of tools and libraries) to reproduce the package at a later date.

The `%files` section of the spec file lists the files and directories on your filesystem that will be put into the package. This will correspond with the files that were placed on your filesystem during the install stage of the build process.

The `%files` section supports the following directives and options:

- `%doc` — Marks documentation files. These go in a directory under `/usr/doc` on the end user’s system. Don’t use this for man pages or other documents that have to reside in specific locations on the end user’s system. Note that the paths listed with this directive are relative to the BUILD directory, not the regular filesystem. For example, in Listing 17.1, the NEWS file listed with the `%doc` directive refers to `/usr/src/distribution/BUILD/ed-0.2/NEWS`, which will be placed on the user’s system as `/usr/doc/ed-0.2/NEWS` when this package is installed.
- `%config` — Marks configuration files. These files get special handling during remove and upgrade operations on the user’s machine.
- `%dir` — Indicates a directory. This causes rpm to package all the files in the indicated directory and all its subdirectories.
- `-f filename` — The `-f` option used with the `%files` section indicates to read the file list from a separate file. For example, the following line:

  `%files -f edlist`

  reads the file list from the file `/usr/src/distribution/BUILD/ed-0.2/edlist`, instead of from the spec file.

> **Caution:** Be careful with listing directories in the file list. If an item in the file list is a directory, rpm interprets it as a `%dir` item and reads all the files in it. This can end up placing a huge number of files (and not the right ones) in the package, if the directory is not correct.

At the end of this stage, a binary package file is in the RPMS/i386 directory and a source package file in SRPMS.

## PACKAGING MISCELLANY

This section has a few miscellaneous tips to help you debug the package building process. Also, some of the conventions used by major distributions for their packages are described. You might want to use similar techniques when you build packages.
