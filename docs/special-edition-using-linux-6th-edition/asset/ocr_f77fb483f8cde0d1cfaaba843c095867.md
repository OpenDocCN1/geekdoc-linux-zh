Generally, the only thing that differs in the helper packages is the list of files and the information fields. To define the information fields for a helper package, the spec file uses the `%package` directive followed by the fields. After that, sections use the package’s name to differentiate—for example,

```
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
```

# BUILDING A PACKAGE

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

# THE PREP STAGE

During the prep stage of the package build, the script in the %prep section of the spec file is run. This script will extract the source files from the TAR file and apply patches in preparation for the actual compilation of the software.

During this stage, a directory is created under /usr/src/distribution/BUILD. This is where the files are placed and where other stages will operate.

You can use any commands you need to prepare the source files in the BUILD directory. However, two special directives handle most of the actions that need to be performed. The %setup directive is used to extract the source files listed in the Source lines. The %patch directive is used to apply the patches listed in the Patch lines.