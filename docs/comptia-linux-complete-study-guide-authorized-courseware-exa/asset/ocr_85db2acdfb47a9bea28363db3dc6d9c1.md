# RPM and Yum Configuration Files

Ordinarily, you needn't explicitly configure RPM or Yum; distributions that use RPM configure it in reasonable ways by default. Sometimes, though, you may want to tweak a few details, particularly if you routinely build source RPM packages and want to optimize the output for your system. You may also want to add a Yum repository for some unusual software you run. To do so, you typically edit an RPM or Yum configuration file.

The main RPM configuration file is `/usr/lib/rpm/rpmrc`. This file sets a variety of options, mostly related to the CPU optimizations used when compiling source packages. You shouldn't edit this file, though; instead, you should create and edit `/etc/rpmrc` (to make global changes) or `~/.rpmrc` (to make changes on a per-user basis). The main reason to create such a file is to implement architecture optimizations—for instance, to optimize your code for one CPU model by passing appropriate compiler options when you build a source RPM into a binary RPM. This is done with the **`optflags`** line:

```
optflags: athlon -O2 -g -march=i686
```

This line tells RPM to pass the -O2 -g -march=i686 options to the compiler whenever building for the athlon platform. Although RPM can determine your system's architecture, the optflags line by itself isn't likely to be enough to set the correct flags. Most default rpmrc files include a series of buildarchtranslate lines that cause rpmbuild (or rpm for older versions of RPM) to use one set of optimizations for a whole family of CPUs. For x86 systems, these lines typically look like this:

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```

These lines tell RPM to translate the athlon, i686, i586, i486, and i386 CPU codes to use the i386 optimizations. This effectively defeats the purpose of any CPU-specific optimizations you create on the **`optflags`** line for your architecture, but it guarantees that the RPMs you build will be maximally portable. To change matters, you must alter the line for your CPU type, as returned when you type **`uname -p`**. For instance, on an Athlon-based system, you might enter the following line:

```
buildarchtranslate: athlon: athlon
```

Thereafter, when you rebuild a source RPM, the system will use the appropriate Athlon optimizations. The result can be a slight performance boost on your own system, but reduced portability—depending on the precise optimizations you choose, such packages may not run on non-Athlon CPUs. (Indeed, you may not even be able to install them on non-Athlon CPUs!)