
## 3 Deploying ASP.NET 5 on Linux

In this chapter we will learn how to deploy ASP.NET 5 on Linux.

### 3.1 Getting Started

In this section we start to deploy ASP.NET 5 on Linux. In this book I use ASP.NET 5 preview, beta4. For illustration, I use Ubuntu 15.04 as Linux distro. Please follow installation steps on next section.

### 3.2 Deploying ASP.NET 5

This installation process is based on this documentation, [https://github.com/aspnet/Home/blob/dev/GettingStartedDeb.md](https://github.com/aspnet/Home/blob/dev/GettingStartedDeb.md). In this section, we install ASP.NET 5 on Linux manually (without docker). Firstly, you update your distro.

```bash
$ sudo apt-get update
```

In general, to install ASP.NET 5 on Ubuntu, you can do the following steps:

- Installing Mono
- Installing libuv
- Installing DNVM
- Installing git (optional)

#### 3.2.1 Installing Mono

Mono is .NET runtime for Linux. You need the latest version of Mono runtime. To install it, you can type these commands.

```bash
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E032
$ echo "deb http://download.mono-project.com/repo/debian wheezy main" > /etc/apt/sources.list.d/mono.list
$ sudo apt-get update
$ sudo apt-get install mono-complete
```

If finished, you can verify it by checking its version.

```bash
$ mono --version
```

```bash
agusk@ubuntu15:~$
agusk@ubuntu15:~$ mono --version
Mono JIT compiler version 4.0.1 (tarball Tue May 12 15:39:23 UTC 2015)
Copyright (C) 2002-2014 Novell, Inc, Xamarin Inc and Contributors. www.mono-project.com
    TLS:               __thread
    SIGSEGV:          altstack
    Notifications:    epoll
    Architecture:     amd64
    Disabled:         none
    Misc:             softdebug
    LLVM:             supported, not enabled.
    GC:               sgen
agusk@ubuntu15:~$
```

#### 3.2.2 Installing libuv

Libuv is a multi-platform asynchronous IO library that is used by the KestrelHttpServer that we will use to host our web applications.

Type these commands to install libuv library.

```bash
$ sudo apt-get install automake libtool curl
$ curl -sSL https://github.com/libuv/libuv/archive/v1.4.2.tar.gz | sudo tar -xz -C /usr/local/src/
$ cd /usr/local/src/libuv-1.4.2
$ sudo sh autogen.sh
$ sudo ./configure
$ sudo make
$ sudo make install
$ sudo rm -rf /usr/local/src/libuv-1.4.2 && cd ~/
$ sudo ldconfig
```

```bash
agusk@ubuntu15:~
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the `-LLIBDIR'
flag during linking and do at least one of the following:
- add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
during execution
- add LIBDIR to the 'LD_RUN_PATH' environment variable
during linking
- use the '-Wl,-rpath -Wl,LIBDIR' linker flag
- have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------
/bin/mkdir -p '/usr/local/include'
/usr/bin/install -c -m 644 include/uv.h include/uv-errno.h include/uv-threadpool.h include/uv-version.h include/uv-unix.h include/uv-linux.h '/usr/local/include/'
/bin/mkdir -p '/usr/local/lib/pkgconfig'
/usr/bin/install -c -m 644 libuv.pc '/usr/local/lib/pkgconfig'
make[1]: Leaving directory '/usr/local/src/libuv-1.4.2'
agusk@ubuntu15:/usr/local/src/libuv-1.4.2$ sudo rm -rf /usr/local/src/libuv-1.4.2 && cd ~/agusk@ubuntu15:~$ sudo ldconfig
agusk@ubuntu15:~$ 
```

#### 3.2.3 Installing DNVM

The last step is to install DNVM. Type this command.

```bash
$ curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh
```

If success, you can see a task which you should do. We must add dnvm on our profile.

```bash
agusk@ubuntu15:~
agusk@ubuntu15:~$ curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvm install.sh | DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh
Downloading dnvm as script to '/home/agusk/.dnx/dnvm/dnvm'
Appending source string to /home/agusk/.bashrc
Type 'source /home/agusk/.dnx/dnvm/dnvm.sh' to start using dnvm
agusk@ubuntu15:~$ 
```

Type this command.

```bash
$ nano /home/<account>/.bashrc
```

Please change `<account>` by your Linux login account.

Then, you get nano editor. You also edit this file using gedit or other text editor. Add this script on .bashrc file into your profile, for instance, `/home/<account>/.bashrc`.

Then, type this script.

```bash
source /home/<account>/.dnx/dnvm/dnvm.sh
```

Please change `<account>` by your Linux login account.

If done, save this file. After that, close your Terminal and then open again so Terminal will load profile script.

The next step is to upgrade. Type this command.

```bash
$ dnvm upgrade
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_29_0.png)

Now you already installed dnvm. It will be used to manage ASP.NET 5 runtime on Linux. You can verify dnvm by typing this command.

```bash
$ dnvm help
```

So you see a list of dnvm parameter.

```bash
agusk@ubuntu15:~$ dnvm upgrade
Determining latest version
Latest version is 1.0.0-beta4
Downloading dnx-mono.1.0.0-beta4 from https://www.nuget.org/api/v2
Download: https://www.nuget.org/api/v2/package/dnx-mono/1.0.0-beta4
############################################## 100.0%
Installing to /home/agusk/.dnx/runtimes/dnx-mono.1.0.0-beta4
Adding /home/agusk/.dnx/runtimes/dnx-mono.1.0.0-beta4/bin to process PATH
Setting alias 'default' to 'dnx-mono.1.0.0-beta4'
agusk@ubuntu15:~$ dnvm help

    ██████████████████████████

.NET Version Manager - Version 1.0.0-beta6-10381
By Microsoft Open Technologies, Inc.

DNVM can be used to download versions of the .NET Execution Environment and mana
ge which version you are using.
You can control the URL of the stable and unstable channel by setting the DNx_FE
ED and DNx_UNSTABLE_FEED variables.

Current feed settings:
```

You can also see a list of your DNx runtime by typing this command.

```bash
$ dnvm list
```

```bash
dnvm alias <alias>
    display value of the specified alias

dnvm alias <alias> <sever>|<alias>|<package>
    <alias>              the name of the alias to set
    <sever>|<alias>|<package>    the DNx version to set the alias to. Alternativel
    y use the version of the specified alias

dnvm unalias <alias>
    remove the specified alias

dnvm [help|-h|-help|--help]
    displays this help text.

dnvm update-self
    updates dnvm itself.
agusk@ubuntu15:~$ dnvm list

Active Version          Runtime Arch Location           Alias
--------- ----------    --------  ---  --------    -----   ----
        *   1.0.0-beta4    mono      ~/.dnx/runtimes    default

agusk@ubuntu15:~$
```

#### 3.2.4 Installing git

This task is optional but I recommend to install it because we want to run the sample app from https://github.com/aspnet/Home.

Type this command to install git.

```bash
$ sudo apt-get install git
```

```bash
agusk@ubuntu15:~

agusk@ubuntu15:~$ sudo apt-get install git
[sudo] password for agusk:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  git-man liberror-perl
Suggested packages:
  git-daemon-run git-daemon-sysvinit git-doc git-el git-email git-gui gitk
  gitweb git-arch git-cvs git-mediawiki git-svn
The following NEW packages will be installed:
  git git-man liberror-perl
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 3,517 kB of archives.
After this operation, 22,7 MB of additional disk space will be used.
Do you want to continue? [Y/n]
```

## 3.3 Testing

To test our ASP.NET 5, we use code samples from https://github.com/aspnet/Home. We clone this code samples and then restore all required libraries using dnu command.

Type these commands.

```bash
$ git clone https://github.com/aspnet/Home
$ cd Home
$ dnu restore
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_32_0.png)

Now you are ready to run code samples.

### 3.3.1 ASP.NET Console

To run ASP.NET Console, we can use dnx. Firstly, navigate to ConsoleApp project.

Type these commands.

```bash
$ cd samples/latest/ConsoleApp/
$ dnx . run .
```

If success, you can see a message “Hello World” on Terminal.
