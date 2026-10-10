
## 6.5 INSTALL DEVELOPMENT STATIONS

  The development stations will be the three machines (Virtual or not) used for development purpose. These three computers have to be setup with development dedicated tools corresponding to the type of GUI you want to develop with.

  The .NET Core 3 SDK is the base install on each station, the specialized tools required will be specified for each type of solution we will review.

  For the example projects presented in this book we have chosen to develop the code with Visual Studio 2019 on Windows, each project has been rebuilt on each OS after a raw copy of the projects (with the SDK).

### 6.5.1 The Windows station (main)

  The windows platform is the coding platform where you have to install the IDE (in our case Visual Studio 2019) and all the tools you need for writing software. The choice of Visual Studio 2019 is obvious in a professional context regarding the features and the high quality of the product (compared to Visual Code who is a more script development-oriented tool).

  First you have to install Visual Studio 2019.

  There are three different versions of the product:

- **Community**: Free version of the product, this version allows you all kind of .NET Core 3 development but does not integrate some features (see table with features).
- **Professional**: As the name indicate (This is the full product).
- **Enterprise**: Offer a better integration for large team and complex constraints environment, it also includes exclusives tools for software architect (architecture layer diagram) and tester (LiveTest).

  The following table below is a resume of the features and specificities of each edition of Visual Studio.

| | Visual Studio Community | Visual Studio Professional | Visual Studio Enterprise |
|---|:---:|:---:|:---:|
| Supported Features | | | |
| Supported Usage Scenarios | *** | **** | **** |
| **Development Platform Support** | | | |
| Integrated Development Environment | ** | ** | *** |
| Advanced Debugging and Diagnostics | * | ** | *** |
| **Testing Tools** | * | * | **** |
| **Cross-platform Development** | ** | ** | *** |
| **Collaboration Tools and Features** | *** | ** | **** |

(source Microsoft.com)

  Choose the version corresponding to the type of development you intend to do (or the type of license you own). In our case the community version is enough for fulfilling the educational needs of the present book.

  The install program will propose you to select the modules you want to install, you have to select at least the elements as described on the (figure 1) of course you can select a complete Install (for testing and reviewing purpose) but the required components you have to install (minimal) for the development needs of this book are:

- Visual Studio Core Editor
- NET desktop development
- ASP.NET and web development
- .NET Core cross-platform development

![Figure 1](img/3d310cc066dda6e2dfa67a650614076f_107_0.png)

  If you plan to use a native GUI library (like LibUI, GTK or QT) it should be wise (and sometimes mandatory) to install the C++ tools too (but we will signal in the samples chapter when and why install it).

- C++ Development environment
- C++ For Linux

  If you want to use a preview version of the .NET Core 3 or 3.1 (or later release still in preview phase) you have to configure Visual Studio 2019 to use it by selecting the proper option in the menu:

  Tools/Options/Environment/Preview features.

![Enable SDK preview in Visual Studio 2019](img/3d310cc066dda6e2dfa67a650614076f_108_0.png)

  For the main development station, you will also need to have a working Internet connection in order to access the NuGet central repository (on port 80) for restoring dependencies packages.

### 6.5.2 The Linux station

  (see .NET Core 3 install for Linux.)

  No additional install is required for ubuntu development station, many tools are already installed in the default setup of the ubuntu desktop system. Verify you have the ubuntu pre-requisites packages installed before the install of the .NET Core 3 SDK. Some samples will require specifics dependencies, but it will be signaled for each example requiring such install.

### 6.5.3 The macOS station

  (see .NET Core 3 Install for macOS).

  We recommend to install the excellent tool “Homebrew”, the missing package manager for macOS. It is often useful to easily install packages as part of a full stack macOS development (and it is mandatory in some cases we will study). You will find a detailed install instruction in the GTK project example section (who requires “brew” for the setup of the dependencies).

  For the development station, if you plane to use macOS system APIs or use native libraries it should be wise to install XCode as well or at least the “XCode command line tools”.

  XCode is the Apple IDE for macOS and ObjectiveC (the language in which macOS is written). It can help you to match the appropriate library (native API), for that OS.

  That’s suppose that you have minimum knowledge in ObjectiveC developments, that could be tricky if you do not know the macOS system (for specialist only).

![macOS station reference](img/3d310cc066dda6e2dfa67a650614076f_109_0.png)

https://brew.sh/

https://developer.apple.com/xcode/

## 6.6 CONFIGURATION FOR REMOTE DEBUGGING

  The remote debugging allows you to execute your code on a remote computer (with a different OS installed) it allows you to debug in real time without quitting you favorite IDE (Visual Studio on Windows) on the target platform.

  This technic is not really often used in the GUI desktop application development context because the platform specifics are shaded with the use of the cross-platform framework (in our case .NET Core 3).

  Nevertheless, it can be used during the development of a multi-platform .NET Standard library (for example a wrapper) used by the application and that is in this context that technic is reviewed.

### A) In Visual Studio:

  For enabling the remote debugging feature in Visual-Studio you have to install the “Remote debugging tools for Visual Studio 2019” at the following address. Download and install also a ssh client for Windows (Putty), It will be used for testing the connection with the remote machine and eventually copy the files with the scp utility (it depends how you want to work).

https://visualstudio.microsoft.com/downloads/#remote-tools-for-visual-studio-2019/

http://www.putty.org

![Visual Studio Remote Tools](img/3d310cc066dda6e2dfa67a650614076f_110_0.png)

### B) Install of the remote debugging tools for Visual Studio 2019 on Linux:

```bash
$ curl -sSL https://aka.ms/getvstdbgsh | /bin/sh /dev/stdin -v latest -l ~/vstdbg
```

  This command line instruction should install the required Linux debugger engine on the platform.

### C) Setup admin account for debugging on the Linux system (ubuntu):

  The creation of a specific user for the debugging is not mandatory but that provides the benefit of not interfering with other account’s permissions and groups (that way is much easier for managing users on the long run) but you can use the “root” account as well.

```bash
~$ Sudo adduser dbgVS
```

  You can also simply use the “root” account, if you do not have security constraints.

  You have to give this user the appropriate rights or/and add him in the appropriate group for having access (read/write) to the deployment folder (with also execute permission, in most of case the admin group is required).

### D) Enable SSH and open port on the firewall (setup communication between computers):

```bash
$ sudo apt-get install openssh-server unzip
$ sudo ufw allow ssh
```

  This command line installs the ssh server and open the required port on the firewall (port 22).

  Verify the user and the connection with a simple ssh test with the Linux machine (use putty and the new defined user) from your Windows station. Check also the folder permissions for the user.

### E) Deploy the application: Copy the file throw scp or use the publish tool in Visual Studio:

  To deploy the application, you have the choice to copy it with a “scp” command or to use a configuration file for the deployment of the application during the “publishing” phase. The file where you can specify the location of the source and the destination folder of the executable is “launch.json”.

### F) Attach the debugger (in Visual Studio) to the remote process on Linux:

  If the VS debugger has been installed on the Linux machine you should have access to the list of the process of the user you connected with. Select the process (in many cases the name of the program) and “Attach” it to the debugger in Visual Studio (make sure the checkbox “show process for all users” is actually checked).

### G) Do Debugging (in Visual Studio):

  You should be able now to debug the application on Linux from your Windows Visual Studio instance.
