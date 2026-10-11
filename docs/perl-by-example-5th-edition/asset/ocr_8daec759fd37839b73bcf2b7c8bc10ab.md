# Appendix

# D

# Perlbrew, CPAN,
and cpanm

Written by Alastair McGowan-Douglas

![](bbox=[0.5, 0.06, 0.9, 0.36])

Perl comes preinstalled on UNIX systems. Normally, you will find that the preinstalled version is older than the latest Perl release, and in some cases it will be subtly different. This Perl is designed by the system maintainers to work with the rest of the system. When you install packages, such as with the system package manager, the packages you install will have been tested against the version of Perl installed by the system.

Many of those packages are precompiled and tested versions of modules available on CPAN, the Comprehensive Perl Archive Network. This allows you to use those modules and that version of Perl to write your own scripts and applications on your system.

This is fine, until you either want to upgrade Perl or install modules that don't exist in your package manager. It is worthwhile to upgrade Perl so as to be up to date with the latest bug fixes and features. Installing modules from CPAN is a cornerstone of Perl programming; if you can't get things from CPAN, you'll find yourself reinventing wheels, writing nonportable code, and unable to use scripts others have written that rely on CPAN modules.

Upgrading and installing are two separate processes, and they are solved in two different ways, but they are related.

# D.1 CPAN and @INC

CPAN (traditionally *the* CPAN; but we usually treat it as a proper noun) is the place where all of the community-submitted code resides and where all modules not in core, can be found, fetched, and installed. In Modern Perl, the ability to find and install modules from CPAN is not just encouraged; it is imperative. Without it, you will write code that repeats mistakes others have made before and have already fixed. Your scripts will not be portable because you didn't use a module that wraps up Perl functions in portable ways. You will not be able to use other people's scripts that make heavy use of modules. In general, you