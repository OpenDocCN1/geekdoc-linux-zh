
![](img/d75cffbcb54aabfb0f9854162061d394_199_0.png)

Figure 12.2: Sample Implementation

## Example 12.17: Runtime Test Installation

```
# cp lsb-runtime-test-2.0-1.ia32.rpm  /opt/lsbsi-ia32/tmp
# /sbin/chroot /opt/lsbsi-ia32
# cd /tmp
# rpm -i lsb-runtime-test-2.0-1.ia32.rpm
# password -d vsx0
```

As shown in Section 12.2.1, log in as user `vsx0`, then run the LSB Runtime test suite (Example 12.18).

## Example 12.18: Running the Runtime Test Suite

```
vsx0$ telnet localhost
vsx0$ run_tests
```

### 12.6 PACKAGING THE SAMPLE IMPLEMENTATION

The LSB-si is released in several configurations for each of the following architectures:

1. **Base system**: A tarball containing only what is required by the LSB Written Specification. Can be entered via chroot. For complete conformance, requires the underlying Linux kernel to be LSB-conformant.
2. **Testable system**: Contains the base system plus additional files and programs needed to enable the LSB-si as a testing environment. This bundle can run the LSB Runtime test suite and LSB-conformant applications. Can be entered via chroot. Once running, it is possible to telnet into the environment. Complete conformance requires the underlying Linux kernel to be LSB-conformant.
3. **Bootable system**: The files from the base system plus a kernel and other support to make it possible to boot a standalone. Some additional configuration will be necessary---for example, an appropriate boot configuration for the target hardware and configuration of necessary kernel modules.
4. **Hosted system**: The files from the base system plus support to run User-Mode Linux, a kernel virtual machine that runs as a user-level application on the host system. User-Mode Linux may not be available for all LSB-supported architectures. The hosted bundle is also available as an installable, ready-to-run package.

![](img/d75cffbcb54aabfb0f9854162061d394_200_0.png)

> When the package is being extended beyond the base, there’s a tradeoff: The system becomes more usable, but includes various non-LSB commands and files, and therefore is a little less ‘pure’ in a testing sense.

### 12.7 DOWNLOADING THE SAMPLE IMPLEMENTATION

To download the LSB Sample Implementation go to the LSB Download Web site.⁶ Table 12.1 represents the information that can be accessed via the World Wide Web.

**lssbi-boot** LSB Sample Implementation bootable system containing a kernel and other support to make it possible to boot the LSB-si in a standalone mode. Requires installation of lssbi-core and post installation configuration.

**lssbi-core** LSB Sample Implementation base system containing only what is required by the LSB Written Specification. Can be entered via chroot.

**lssbi-graphics** LSB Sample Implementation graphics system containing the files necessary to support graphical applications within the LSB-si. Requires installation of lssbi-core.

**Table 12.1: Sample Implementation Download Page**

| Specification Version | Package | Version | Architecture |
| :--- | :--- | :--- | :--- |
| 2.0.0 | lssbi-boot | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | lssbi-core | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | lsb-graphics | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | lsb-test | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |
| 2.0.0 | lsb-uml | 2.0.2 | IA32, IA64, PPC32, PPC64, S390, S390X, x86_64 |

`lsbsi-test` LSB Sample Implementation testable system containing additional files and programs needed to enable the LSB-si as a testing environment. Requires installation of `lsbsi-core`.

`lsbsi-uml` LSB Sample Implementation hosted system containing support to run User-Mode Linux, a kernel virtual machine that runs as a user-level application on the host system. UML may not be available for all LSB-supported architectures. Requires installation of `lsbsi-core`.

`lsb` This package provides the base LSB package. Note that this package should only ever be installed on the LSB Sample Implementation. Installing this package on any other distribution may damage the system.

`lsb-uml-si` LSB Sample Implementation User-Mode Linux environment.

# CHAPTER THIRTEEN

## Using the LSB Development Environment

The LSB Development Environment is designed to help developers build applications which conform to the LSB Written Specification. They primarily do this by providing easy ways to:

- Compile against header files that contain definitions required by the LSB Written Specification
- Dynamically link against shared libraries that contain only interfaces required by the LSB Written Specification

### 13.1 UNDERSTANDING THE LSB DEVELOPMENT ENVIRONMENT

The LSB Development Environment is not intended to be an Integrated Development Environment (IDE) in itself, but rather an enhancement to existing IDEs, to allow them to build binaries that are LSB-compliant. Note that although the LSB Development Environment helps programmers build LSB-compliant applications, it is not the only way to do so.

1. http://www.linuxbase.org/build/
2. http://www.linuxbase.org/download/

A function allows older applications to continue to use the old version, while new applications can use the new version.

When a binary is created, it inspects the shared library it is linking against and records the versions of those interfaces it requires. At runtime, the binary will look for the interfaces with the recorded version number, and fail if they do not exist. Thus, it is necessary to link against shared libraries that contain the versions of the interfaces guaranteed to exist on an LSB-compliant runtime.

Where libraries supported by the LSB use symbol versioning, the specification lists specific versions of the interfaces. The LSB stub libraries only contain the versions of the interfaces allowed by the LSB Written Specification, and so if they are used, it is impossible to use a wrong version when building a binary.

Often there are interfaces contained in shared libraries that must not be used by an LSB-compliant binary. These interfaces are often private functions, or interfaces not supported by the LSB. Since the stub libraries only contain interfaces required by the specification, an error will occur during the linking stage if an application uses an unsupported interface.

### 13.3.2 LSB Header Files

The definitions contained within a header file associated with a library may change over time as the ABI of that library evolves. For example, a function in one version of the library may take one parameter, while in the next version it may take two parameters.

The LSB Written Specification defines an ABI for each supported library, and the header files used to compile against that library must match exactly. In order to avoid the problem of finding the exact version of the software that contains the correct definitions, header files matching the specification are supplied with the LSB Development Environment.

### 13.3.3 Using the Development Tools

There are currently two development tools, `lsb-build-chroot` and `lsb-build-cc`, that compile and link against compliant headers and libraries.

Using these tools is an easy way to build an LSB-compliant application. Both tools use the `lsb-build-base` package. This package contains the LSB header files and stub libraries.

#### 13.3.3.1 lsb-build-chroot

The `lsb-build-chroot` uses the **chroot** command to create a virtual LSB platform development environment on your machine. By default, it presents a minimal environment which, wherever possible, does not contain header files or libraries that, if compiled against, would lead to a binary that is not LSB-compliant. Within this environment, the `/usr/include` contains the LSB header files and the `/usr/lib` contains the LSB stub libraries.

To generate the virtual environment, the `lsb-build-chroot` uses bind mounts instead of copying the entire directory structure, so the disk space requirements are minimal. It also means that changes (such as compiling a binary) made within the environment are reflected immediately outside the environment, and vice versa.

You do not need root access to use `lsb-build-chroot` because it is implemented with an **ssh** daemon which is run on a high-port. The `ssh` daemon bind-mounts your home directory into the *chroot* environment, so you can log in to the restricted environment for compilation. You can also run a full editing and debugging environment outside of the `chroot` operating on the same files that you are compiling within the restricted environment.

In cases where applications need to compile or link against libraries that are not LSB-compliant, you can specifically import those libraries and header files into the *chroot* environment. Depending on the sophistication of the build process for your application, you might also have to import other tools into the environment so that they can run correctly.

![](img/d75cffbcb54aabfb0f9854162061d394_207_0.png)

The bind mounts might cause problems if you update system packages while `lsb-build-chroot` is running.
