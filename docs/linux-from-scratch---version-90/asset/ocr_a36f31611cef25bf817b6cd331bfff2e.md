# 5.29. Perl-5.30.0

The Perl package contains the Practical Extraction and Report Language.
Approximate build time: 1.6 SBU
Required disk space: 275 MB

# 5.29.1. Installation of Perl

Prepare Perl for compilation:

```
sh Configure -des -Dprefix=/tools -Dlibs=-lm -Uloclibpth -Ulocincpth
```

The meaning of the Configure options:

-des
This is a combination of three options: -d uses defaults for all items; -e ensures completion of all tasks; -s silences non-essential output.
-Uloclibpth amd -Ulocincpth
These entries undefined variables that cause the configuration to search for locally installed components that may exist on the host system.

Build the package:

```
make
```

Although Perl comes with a test suite, it would be better to wait until it is installed in the next chapter.
Only a few of the utilities and libraries need to be installed at this time:

```
cp -v perl cpan/podlators/scripts/pod2man /tools/bin
mdir -pv /tools/lib/perl5/5.30.0
cp -Rv lib/* /tools/lib/perl5/5.30.0
```

Details on this package are located in Section 64.40.2, "Contents of Perl."