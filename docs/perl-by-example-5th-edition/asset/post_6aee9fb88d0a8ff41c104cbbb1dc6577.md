
## C.5 Appendix Summary

There is a lot more to Moose. This appendix has been an introduction to provide you with some Moose examples to help you get started. There is a plethora of information available on the Internet. Some starting points are listed in the following section.

## C.6 References

Following are some resources to continue your education on Moose.

- 1. *Moose::Manual* (a starter)
- 2. *Moose::Cookbook* (many examples)
- 3. Moose, “A Postmodern Object System for Perl,” <http://moose.interactive.com/en>.
- 4. Perl Maven, “Object Oriented Perl using Moose,” <http://permaven.com/object-oriented-perl-using-moose>.
- 5. The Perl Review, “Getting Started with Moose,” <http://www.theperlreview.com/articles/moose.html>.
- 6. The Sysadmin Notebook, “Building Modules and Testing,” <http://home.clara.net/drds/Perl/Modules.html>.

# Appendix D: Perlbrew, CPAN, and cpanm

Written by Alastair McGowan-Douglas

![](img/8556abcb353c0991f12099420ec28735_826_0.png)

Perl comes preinstalled on UNIX systems. Normally, you will find that the preinstalled version is older than the latest Perl release, and in some cases it will be subtly different. This Perl is designed by the system maintainers to work with the rest of the system. When you install packages, such as with the system package manager, the packages you install will have been tested against the version of Perl installed by the system.

Many of those packages are precompiled and tested versions of modules available on CPAN, the Comprehensive Perl Archive Network. This allows you to use those modules and that version of Perl to write your own scripts and applications on your system.

This is fine, until you either want to upgrade Perl or install modules that don't exist in your package manager. It is worthwhile to upgrade Perl so as to be up to date with the latest bug fixes and features. Installing modules from CPAN is a cornerstone of Perl programming; if you can't get things from CPAN, you'll find yourself reinventing wheels, writing nonportable code, and unable to use scripts others have written that rely on CPAN modules.

Upgrading and installing are two separate processes, and they are solved in two different ways, but they are related.

## D.1 CPAN and @INC

CPAN (traditionally *the* CPAN; but we usually treat it as a proper noun) is the place where all of the community-submitted code resides and where all modules not in core, can be found, fetched, and installed. In Modern Perl, the ability to find and install modules from CPAN is not just encouraged; it is imperative. Without it, you will write code that repeats mistakes others have made before and have already fixed. Your scripts will not be portable because you didn't use a module that wraps up Perl functions in portable ways. You will not be able to use other people's scripts that make heavy use of modules. In general, you will be using Perl as a blunt instrument instead of the Swiss Army Knife it can be, and you will find the community reluctant to help you if you have issues trying to solve a problem that's already been solved.

### D.1.1 Finding Modules

When writing code, it is valuable to search first on [http://metacpan.org/](http://metacpan.org/) to see whether your problem has been solved before. If it has, you can download and use that module. If not, consider solving your problem in a generic way, such that you could upload your module to CPAN for future developers to do what you just tried.

### D.1.2 Using Modules

When you *use Module;*, Perl looks in various places for *Module.pm*, and loads the first one it finds. If it doesn't find it at all, you will get a compile-time error:

```
use Module;
Can't locate Module.pm in @INC (you may need to install the Module module)
```

(This particular error message was introduced in 5.18; prior to this version, it did not give the hint about installing the module.)

The use directive defines a requirement; semantically, it says that the script in question cannot run without the stated module. Hence, Perl refuses to go further without the module. The message states that the file could not be found in @INC, which you will recognize as the name of a Perl array @INC is, indeed, an array; the array that contains all the search paths for modules.

You can inspect the contents of @INC by either using it as a normal array and printing them, or asking *perl -V* to list them:

```
$ perl -E'say for @INC;'²
/etc/perl
/usr/local/lib/perl/5.18.2
/usr/local/share/perl/5.18.2
...
<snippet>

$ perl -V
Summary of my perl5 (revision 5 version 18 subversion 2) configuration:
```

1. At the time of writing, the traditional CPAN search site ([http://search.cpan.org](http://search.cpan.org)) is fluctuating between available and unavailable. That site is being phased out for not being community-run—the code is not available and the community cannot access the server that hosts it. The new site, metacpan, is available on github at [https://github.com/CPAN-API](https://github.com/CPAN-API).
2. -E is a new option introduced with 5.10 that is equivalent to `-c/use feature \'5.10\''`. -E turns on all the features introduced with 5.10. Here, we use it, in order to use say.

## CPAN and @INC

```
Platform:
osname=linux, osvers=3.2.0-58-generic, archname=x86_64-linux-gnu-thread-multi
...
<snip>
...
Compiled at Mar 27 2014 16:30:28
@INC:
   /etc/perl
   /usr/local/lib/perl/5.18.2
   /usr/local/share/perl/5.18.2
   /usr/lib/perl5
   /usr/share/perl5
   /usr/lib/perl/5.18
   /usr/share/perl/5.18
   /usr/local/lib/site_perl
...
```

These are all the directories Perl will look in by default. Listed is the default output for the Perl provided with Linux Mint 17, which comes with 5.18; your output may differ.

These directories are the places Perl looks when your script requests a module. Apart from `/`, however, all of these directories are system directories. Only root can write to these. Some of these directories don't even exist! This is just a default set that Perl is built with. The ones that do exist are:

```
/usr/lib/perl5
/usr/share/perl/5.18
/usr/lib/perl/5.18
/usr/share/perl/5.18
```

(Of course the current directory exists) Files in the `lib` directories are architecture-dependent, and therefore are going files that interface between Perl and existing C libraries, or else are written in C for efficiency purposes. Those in `share` are everything else—pure Perl modules, essentially.

Keep in mind, that all of these files are provided by `apt`, Debian's package manager. None of them were installed manually by the user. What if you want to use a module from CPAN, but `apt` hasn't installed it?

## I Already Have It!

In some cases you will already have the module you want. This is most often the case when you are writing the module, so it's not actually on CPAN yet; or it is, but you've `updated` it and want to use the updated version.

Less often, you will have been provided a module from somewhere other than CPAN. This can happen if you are using code from a third-party vendor. This is very uncommon. Most modules written by third parties go on CPAN anyway, because they interface into proprietary software or services, meaning the company suffers nothing from making the modules themselves free on CPAN.

In all cases, you can tell Perl where to look for modules using the -I option to Perl, which prepends the @INC array with the requested directory. (Ordinarily you will have a distribution with a script and a lib directory containing the script’s modules). The -I option is shown here:

```bash
$ perl -I lib example.pl
```

This is the technique cpanm will use when testing modules prior to installation. With -I, the temporary directory with the module in it can be added to @INC, and the test scripts run in this context. This ensures the module being tested is the one in the temporary directory, and not an older version installed in system Perl.

For more permanent locations for your modules, you can use the PERLLIB environment variable. Simply set it to a set of colon-separated paths, much like PATH itself, and these will be added to @INC as well.

```bash
$ PERLLIB="$HOME/perl5:$$PERLLIB$$" perl example.pl
```

### D.1.3 Package Manager

For modules you want to get from CPAN, the first thing to check is your package manager, if your system has one. As noted, Debian has apt, RedHat and derivatives have yum, and FreeBSD has ports. If you have access, the easiest way to get a module for the system Perl is to install it via the package manager.

Modules from the package manager have the advantage of having been tested by the vendor; i.e., the people who put the operating system together in the first place. You will often hear the term “vendor Perl” used to refer to the system Perl that your vendor supplies. Additionally, on many systems, the packaged versions are precompiled. This means the procedure for getting a Perl module with C dependencies is a simple matter of unpacking it. Later, we will see how otherwise complex this can be.

This method is not without its drawbacks, however, including the following:

- You need root access. If you are working in a corporate environment, you are unlikely to have this access. Sometimes there are procedures in place to request that those who do have access install it for you, but these processes take time and aren’t necessarily going to be granted.
- It installs to system Perl. If you are using Perlbrew (discussed later), you will not be able to use a prepackaged version, because Perlbrew creates custom Perl installations independent of vendor Perl.
- The version in the package manager might not be the version containing the features you want. You will have to get the latest version from CPAN if the packaged version is older.
- It might not be there! There are tens of thousands of distributions on CPAN, and it is infeasible for a vendor to package, test, and distribute every one of them.

With the recent resurgence of Perl’s popularity (the “Modern Perl” movement)
