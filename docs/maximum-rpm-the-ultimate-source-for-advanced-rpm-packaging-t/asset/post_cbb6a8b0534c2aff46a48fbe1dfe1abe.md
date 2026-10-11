
## 14.2.3. The autoreprov Tag: Disable Automatic Dependency Processing

Okay, so /lib/libc.so.5.3.12’s soname is libc.so.5. Let’s see if the libc package really does provide the libc.so.5 soname:

```
# rpm -q --provides libc
libm.so.5
libc.so.5
#
```

Yes, there it is, along with the soname of another library contained in the package. In this way, RPM can ensure that any package requiring libc.so.5 will have a compatible library available as long as the libc package, which provides libc.so.5, is installed.

In most cases, automatic dependencies are enough to fill the bill. However, there are circumstances when the package builder has to manually add dependency information to a package. Fortunately, RPM’s approach to manual dependencies is both simple and flexible.

There may be times when RPM’s automatic dependency processing is not desired. In these cases, the autoreprov tag may be used to disable it. This tag takes a yes/no or 0/1 value. For example, to disable automatic dependency processing, the following line may be used:

```
AutoReqProv: no
```

## 14.3. Manual Dependencies

You might have noticed that we’ve been using the words requires and provides to describe the dependency relationships between packages. As it turns out, these are the exact words used in spec files to manually add dependency information. Let’s look at the first tag: requires.

### 14.3.1. The requires Tag

We’ve been deliberately vague when discussing exactly what it is that a package requires. Although we’ve used the word capabilities, in fact, manual dependency requirements are always represented in terms of packages. For example, if package foo requires that package bar is installed, it’s only necessary to add the following line to foo’s spec file:

```
Requires: bar
```

Later, when the foo package is being installed, RPM will consider foo’s dependency requirements met if any version of package bar is already installed. As long as the requiring and the providing packages are installed using the same invocation of RPM, the dependency checking will succeed. For example, the command `rpm -ihv *.rpm` will properly check for dependencies, even if the requiring package ends up being installed before the providing package.

If more than one package is required, they can be added to the *requires* tag, one after another, separated by commas and/or spaces. So if package *foo* requires packages *bar* and *baz*, the following line will do the trick:

```
requires: bar, baz
```

As long as any version of *bar* and *baz* is installed, *foo*'s dependencies will be met.

#### 14.3.1.1. Adding Version Requirements

When a package has slightly more stringent needs, it’s possible to require certain versions of a package. All that’s necessary is to add the desired version number, preceded by one of the following comparison operators:

- `<`      Requires a package with a version less than the specified version.
- `<=`     Requires a package with a version less than or equal to the specified version.
- `=`      Requires a package with a version equal to the specified version.
- `>=`     Requires a package with a version greater than or equal to the specified version.
- `>`      Requires a package with a version greater than the specified version.

Continuing with our example, let’s suppose that the required version of package *bar* actually needs to be at least 2.7, and that the *baz* package must be version 2.1—no other version will do. Here’s what the *requires* tag line would look like:

```
requires: bar >= 2.7, baz = 2.1
```

We can get even more specific and require a particular release of a package:

```
requires: bar >= 2.7-4, baz = 2.1-1
```

#### 14.3.1.2. When Version Numbers Aren’t Enough

You might think that with all these features, RPM’s dependency processing can handle every conceivable situation. You’d be right, except for the problem of version numbers. RPM needs to be able to determine which version numbers are more recent than others in order to perform its version comparisons.

It’s pretty simple to determine that version 1.5 is older than version 1.6. But what about 2.01 and 2.1? Or 7.6a and 7.6? There’s no way for RPM to keep up with all the different version-numbering schemes in use. But there is a solution; there are two, in fact.

##### 14.3.1.2.1. Solution Number 1: Serial Numbers

When RPM can’t decipher a package’s version number, it’s time to pull out the serial tag. This tag is used to help RPM determine version number ordering. Here’s a sample serial tag line:

```
Serial: 42
```

This line indicates that the package has the serial number 42. What does the 42 mean? Only that this version of the package is older than the same package with the serial number 41, but younger than the same package with the serial number 43. If you think of serial numbers as being nothing more than very simple version numbers, you’ll be on the mark.

In order to direct RPM to look at the serial number instead of the version number when doing dependency checking, it’s necessary to append an $ to the end of the conditional operator in the requires tag line. So if a package requires package foo to have a serial number equal to 42, the following tag line would be used:

```
Requires: foo =S 42
```

If the foo package needs to have a serial number greater than or equal to 42, this line would work:

```
Requires: foo >=S 42
```

It might seem that using serial numbers is a lot of extra trouble, and you’re right. But there is an alternative.

##### 14.3.1.2.2. Solution Number 2: Just Say No!

If you have the option between changing the software’s version-numbering scheme or using serial numbers in RPM, consider changing the version-numbering scheme. Chances are, if RPM can’t figure it out, most of the people using your software can’t, either. But in case you aren’t the author of the software you’re packaging, and its version numbering scheme is giving RPM fits, the serial tag can help you out.

### 14.3.2. The conflicts Tag

The conflicts tag is the logical complement to the requires tag. It is used to specify which packages conflict with the current package. RPM will not permit conflicting packages to be installed unless overridden with the --nodeps option.

The conflicts tag has the same format as requires. It accepts a real or virtual package name and can optionally include version and release specifications or a serial number.

### 14.3.3. The provides Tag

Now that you've seen how it's possible to require a package using the requires tag, you're probably expecting that you'll need to use the provides tag in every single package. After all, RPM has to get those package names from somewhere, right?

While it is true that RPM needs to have the package names available, the provides tag is normally not required. It would actually be redundant because the RPM database already contains the name of every package installed. There's no need to duplicate that information.

But wait! We said earlier that manual dependency requirements are always represented in terms of packages. If RPM doesn't require the package builder to use the provides tag to provide the package name, then what is the provides tag used for?

#### 14.3.3.1. Virtual Packages

Enter the virtual package. A virtual package is nothing more than a name specified with the provides tag. Virtual packages are handy when a package requires a certain capability, and that capability can be provided by any one of several packages. Here's an example: In order to work properly, sendmail needs a local delivery agent to handle mail delivery. There are a number of different local delivery agents available: sendmail1 will work just fine with any of them.

In this case, it doesn't make sense to force the use of a particular local delivery agent as long as one's installed, sendmail1's requirements will have been satisfied. So sendmail1's package builder adds the following line to sendmail1's spec file:

```
requires: 1da
```

There is no package with that name available, so sendmail1's requirements must be met with a virtual package. The creators of the various local delivery agents indicate that their packages satisfy the requirements of the 1da virtual package by adding the following line to their packages' spec files:

```
provides: 1da
```

![](img/5ceb645f91e0f928013c644127692ba8_233_0.png)

Now, when sendmail is installed, as long as there is a package installed that provides the 1da virtual package, there will be no problem.
