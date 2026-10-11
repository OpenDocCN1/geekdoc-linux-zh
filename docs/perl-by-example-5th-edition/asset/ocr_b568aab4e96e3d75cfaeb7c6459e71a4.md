# 13.2  The Standard Perl Library

![](bbox=[0.03, 0.1, 0.66, 0.25])

Figure 13.4    Accessing package variables.

# 13.2  The Standard Perl Library

The Perl distribution comes with a number of standard Perl library functions and packages. The Perl 4 library routines are procedural programs and their names end in a .pl extension. The Perl 5 modules end with a .pm extension. In Perl 5, the .pm files are called **modules**. The .pm files are modules written in two programming styles: procedural and object-oriented. The module filenames start with a capital letter. The .pm filenames starting with a lowercase letter are a special type of module, called a **pragma**. A **pragma** is a module that tells the compiler that certain conditions must be checked in a Perl program before it can run. Files that have no extension at all are subdirectories. They contain common modules that are divided into several .pm files; for example, the Math subdirectory contains *BigFloat.pm*, *BigInt.pm*, *Complex.pm*, and *Trig.pm*.

The following is a sample listing from the standard Perl 5.18 library:2

| ActivePerl | Bit | Compress | Data | Errno.pm |
| --- | --- | --- | --- | --- |
| ActivePerl.pm | Bundle | Config | Date | Eval |
| ActiveState | CGI | Config.pm | Devel | Exception |
| Algorithm | CGI.pm | Config.pod | Digest | Exporter |
| AnyDBM_File.pm | CORE | Config_gn.pl | Digest.pm | Exporter.pm |
| App | CORE.pod | Config_heavy.pl | DrvHandle.pm | ExtUtils |
| Archive | CPAN | Cwd.pm | Dist | Fatal.pm |
| Attribute | CPAN.pm | DB.pm | Dumpvalue.pm | Fcntl.pm |
| AutoLoader.pm | CPANPLUS | DBD | DynaLoader.pm | File |
| AutoSplit.pm | CPANPLUS_pm | DBI | Email | FileCache.pm |
| B | Carp | DBI.pm | Encode | FileHandle.pm |
| B.pm | Carp.pm | DBM_Filter | Encode.pm | Filter |
| BSD | Class | DBM_Filter.pm | English.pm | FindBin.pm |
| Benchmark.pm | Clone.pm | DB_File.pm | Env.pm | GD |

2.  The pathname to the standard Perl library is determined at the time Perl is installed. This can be assigned either a default value or a pathname designated by the person installing Perl.