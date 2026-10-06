
# EXERCISE 2.1 (continued)

- 5. Type **rpm -q zsh** to verify that the package isn't currently installed. The system should respond with the message `package zsh is not installed`.

- 6. Type **rpm -qpi zsh-4.3.17-1.fc17.x86_64.rpm**. (You'll need to provide a complete path to the file if it's not in your current directory). The system should respond by displaying information about the package, such as the version number, the vendor, the hostname of the machine where it was built, and a package description.

- 7. Type **rpm -ivh zsh-4.3.17-1.fc17.x86_64.rpm**. The system should install the package and display a series of hashes (#).

- 8. Type **rpm -q zsh**. The system should respond with the complete package name.

- 9. Type **zsh**. This launches a shell, which functions much like the common bash and tcsh shells. You're likely to use your command prompt change, but you can issue most of the same commands you can use with zsh or tcsh.

- 10. Type **rpm -V zsh**. The system shouldn't produce any output—just a new command prompt. The verify (-v or --verify) command checks the package files against data stored in the database. Immediately after installation, packages should show no deviations. (A handful of packages will be modified during installation, but zsh isn't one of them)

- 11. Type **rpm -e zsh**. The system shouldn't produce any output—just a new command prompt. This command removes the package from the system. Note that you're removing the zsh package while running the zsh program. Linux continues to run the zsh program you're using, but you'll be unable to launch new instances of the program. Some programs might misbehave because of this; files will be missing after you remove the package.

- 12. Type **exit** to return to your normal shell.

- 13. Type **rpm -q zsh**. The system should respond with a `package zsh is not installed` error because you just uninstalled the package.

- 14. Type **yum install zsh**. The system should check your repositories, download zsh, and install it. It will ask for confirmation before beginning the download.

- 15. Type **rpm -q zsh**. The results should be similar to those in step 8, although the version may differ.

- 16. Type **rpm -e zsh**. This step removes zsh from the system but produces no output, as in step 11.

The final three steps will only work if your distribution uses Yum. If you're using a distribution that uses another tool, you may be able to locate and use its equivalent, such as zypper for SUSE.

# RPM and Yum Configuration Files

Ordinarily, you needn't need to explicitly configure RPM or Yum; distributions that use RPM configure it in reasonable ways by default. Sometimes, you may need to tweak a few details, particularly if you routinely build RPM packages and want to optimize your computer. You may also want to add a Yum repository for unusual software you need. To do so, you typically edit an RPM or Yum configuration file.

The main RPM configuration file is `/usr/lib/rpm/rpmrc`. This file sets a variety of options, nearly identical to the CPU optimizations used when compiling source packages. You shouldn't edit this file; instead, you create and edit `/etc/rpmrc` (to make global changes) or `~/.rpmrc` (to make changes on a per-user basis). The main reason to create such a file is to implement architecture optimizations—for instance, to optimize your code for your CPU model by passing appropriate compiler options when you build a source RPM into a binary RPM. This is done with the `optflags` lines:

```
optflags: athlon -O2 -march=i386
```

This line tells RPM to pass the -O2 -march=i386 options to the compiler when building for the Athlon platform. Although RPM can determine your system's architecture, the optflags line by itself is unlikely to set the correct flags. Most rpm files include a series of `buildarchtranslate` lines that allow rpmbuild (or older versions of RPM) to use one set of optimizations for a whole family of CPUs. For x86 systems, these lines translate look like this:

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```

These lines tell RPM to translate the athlon, i686, i586, i486, and i386 CPU codes to use the i386 optimizations. This effectively defeats the purpose of any CPU-specific optimizations for your architecture, but it guarantees that the RPMs you build will be maximally portable. To change matters, you must alter the line for your CPU type, as returned when you `uname -p`. For instance, on an Athlon-based system, you might enter the following line:

```
buildarchtranslate: athlon: athlon
```

Therefore, when you rebuild a source RPM, the result can be a performance boost, although it may reduce portability. In fact, you can use the optflags line if you want to bypass the default detection. Most rpm files include a series of `buildarchtranslate` lines that allow rpmbuild (or older versions of RPM) to use one set of optimizations for a whole family of CPUs. For x86 systems, these lines translate look like this:

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```

These lines tell RPM to translate the athlon, i686, i586, i486, and i386 CPU codes to use the i386 optimizations. This effectively defeats the purpose of any CPU-specific optimizations for your architecture, but it guarantees that the RPMs you build will be maximally portable. To change matters, you must alter the line for your CPU type, as returned when you `uname -p`. For instance, on an Athlon-based system, you might enter the following line:

```
buildarchtranslate: athlon: athlon
```

Therefore, when you rebuild a source RPM, the result can be a performance boost, although it may reduce portability. In fact, you can use the optflags line if you want to bypass the default detection. Most rpm files include a series of `buildarchtranslate` lines that allow rpmbuild (or older versions of RPM) to use one set of optimizations for a whole family of CPUs. For x86 systems, these lines translate look like this:

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```
[truncated repeated text logic]

# ## Debian Distributions and Conventions

As the name implies, Debian packages originated with the Debian distribution. Since that time, the format has been adopted by several other distributions, including Ubuntu, Linux Mint, and Xandros. Such distributions are derived from the original Debian, which means that packages from the original Debian are likely to work well on other Debian-based systems. Although Debian doesn't emphasize GUI configuration tools, its derivatives tend to be more GUI-centric, which makes these distributions more appealing to Linux novices. The original Debian is unusual in that it's maintained not by a company that is motivated by profit, but rather by volunteers who are motivated by the desire to build a product they want to use.
