
## 1.1.1.1. Advantages of a Package

One of the most obvious benefits to having a package is that the package is one easily manageable chunk. If you move it from one place to another, there’s no risk of any part getting left behind. Although this is the most obvious advantage, it’s not the biggest one. The biggest advantage is that the package can contain the knowledge about what it takes to install itself on your computer. And if the package contains the steps required to install itself, the package can also contain the steps required to uninstall itself. What used to be a painful manual process is now a straightforward procedure. What used to be a mass of 20,000 files becomes a couple hundred packages.

## 1.1.2. Manage Your Packages or They Will Manage You

A couple hundred packages? Even though the use of packages has decreased the complexity of managing a system by an order of magnitude, it hasn’t yet gotten to the level of being a no-brainer. It’s still necessary to keep track of what packages are installed on your system. And if some packages require other packages in order to be installed or operate correctly, these should be tracked as well.

### 1.1.2.1. Packages Lead Active Lives

If you start looking at a computer system as a collection of packages, you’ll find that a distinct set of operations will take place on those packages time and time again:

- New packages are installed. Maybe it’s a spreadsheet you’ll use to keep track of expenses, or the latest shoot-'em-up game, but in either case it’s new and you want it.
- Old packages are replaced with newer versions. The company that wrote the word processor you use daily comes out with a new version. You’ll probably want to install the new version and remove the old one.
- Packages are removed entirely. Perhaps that overhyped strategy game just didn’t cut it. You have better things to do with that disk space, so get rid of the game!

With this much activity going on, it’s easy to lose track of things. What types of package information should be available to keep you informed?

### 1.1.2.2. Keeping Track of Packages

Just as certain operations are performed on packages, there are also certain types of information that will make it easier to make sense of the packages installed on your system:

- Certainly you’d like to be able to see what packages are installed. It’s easy to forget whether the fax program you tried a few months ago is still installed.

It would be nice to be able to get more detailed information on a specific package. This might consist of anything from the date the package was installed to a list of files it installed on your system.

Being able to access this information in a variety of ways can be helpful, too. Instead of simply finding out what files a package installed, it might be handy to be able to name a particular file and find out which package installed it.

If this amount of detail is possible, it should be possible to see if the way a package is presently installed varies from the way it was originally installed. It’s not at all unusual to make a mistake and delete one file—or 100. Being able to tell if one or more packages are missing files could greatly simplify the process of getting an ailing system back on its feet again.

Files containing configuration information can be a real headache. If it were possible to pay extra attention to these files and make sure any changes made to them weren’t lost, life would certainly be a lot easier.

## 1.2. Package Management: How to Do It

Well, all this sounds great: easy install, upgrade, and deletion of packages; getting package information presented several different ways; making sure packages are installed correctly; and even tracking changes to config files. But how do you do it?

As mentioned earlier, the obvious answer is to let the computer do it. Many groups have tried to create package management software. There are two basic approaches:

- Some package management systems concentrate on the specific steps required to manipulate a package.
- Other package management systems take a different approach, keeping track of the files on the system and manipulating packages by concentrating on the files involved.

Each approach has its good and bad points. In the first method, it’s easy to install new packages, somewhat difficult to remove old ones, and almost impossible to obtain any meaningful information about installed packages.

The second method makes it easy to obtain information about installed packages and fairly easy to install and remove packages. The main problem with using this method is that there may not be a well-defined way to execute any commands required during the installation or removal process.

In practice, no package management system uses one approach or the other; all are a mixture of the two. The exact mix and design goals will dictate how well a particular package management system meets the needs of the people using it. At the time Red Hat Software started work on its Linux distribution, there were a number of package management systems in use, each with a different approach to making package management easier.

## 1.2.1. The Ancestors of RPM

Because this is a book about the Red Hat Package Manager, a good way to see what RPM is all about is to look at the package management software that preceded RPM.

### 1.2.1.1. RPP

RPP was used in the first Red Hat Linux distributions. Many of RPP's features would be recognizable to anyone who has worked with RPM. Some of these innovative features are:

- Simple, one-command installation and uninstallation of packages.
- Scripts that can run before and after installation and uninstallation of packages.
- Package verification. The files of individual packages can be checked to see that they haven't been modified since they were installed.
- Powerful querying. The database of packages can be queried for information about installed packages, including file lists, descriptions, and more.

Although RPP possessed several of the features that were important enough to continue on as parts of RPM today, it had some weaknesses, too:

- It didn't use *pristine sources*. Every program is made up of programming language statements stored in files. This source code is later translated into a binary language that the computer can execute. RPP's packages were based on source code that had been modified specifically for RPP. Since the sources were no longer as the program's creator had written them, they were no longer *pristine*. This is a bad idea for a number of fairly technical reasons. Not using pristine sources made it difficult for package developers to keep things straight, particularly if they were building hundreds of different packages.
- It couldn't guarantee that executables were built from packaged sources. The process of building a package for RPP was such that there was no way to ensure that the executable programs were built from the source code contained in an RPP source package. Once again, this was a problem for package builders, especially those who had large numbers of packages to build.
- It had no support for multiple architectures. As people started using RPP, it became obvious that the package managers that were unable to simplify the process of building packages for more than one architecture, or type of computer, were going to be at a disadvantage. This was a problem, particularly for Red Hat Software, because it was starting to look at the possibility of creating Linux distributions for other architectures, such as the Digital Alpha.

Even with these problems, RPP was one of the things that made the first Red Hat Linux distributions unique. Its ability to simplify the process of installing software was a real boon to many of Red Hat's customers, particularly those with little experience in Linux.

### 1.2.1.2. PMS

While Red Hat Software was busy with RPP, another group of Linux devotees was hard at work with its package management system. Known as PMS, its development, lead by Rik Faith, attacked the problem of package management from a slightly different viewpoint.

Like RPP, PMS was used to package a Linux distribution. This distribution was known as the BOGUS distribution, and all the software in it was built from original unmodified sources. Any changes that were required were patched in during the process of building the software. This is the concept of pristine sources and is PMS's most important contribution to RPM. The importance of pristine sources cannot be overstated. It allows the packager to quickly release new versions of software and to immediately see what changes were made to the software.

The chief disadvantages of PMS were weak querying ability, no package verification, no multiple architecture support, and poor database design.

### 1.2.1.3. PM

Later, Rik Faith and Doug Hoffman, working under contract for Red Hat Software, produced PM. The design combined all the important features of RPP and PMS, including one-command installation and uninstallation, scripts run before and after installation and uninstallation, package verification, advanced querying, and pristine sources. However, it retained RPP's and PMS's chief disadvantages: weak database design and no support for multiple architectures.

PM was very close to a viable package management system, but it wasn't quite ready for prime time. It was never used in a commercially available product.

### 1.2.1.4. RPM Version 1

With two major forays into package management behind them, Marc Ewing and Erik Troan went to work on a third attempt. This one would be called the Red Hat Package Manager, or RPM.

Although it built on the experiences of PM, PMS, and RPP, RPM was quite different under the hood. RPM was written in the Perl programming language for fast development. Version 1 of RPM focused on addressing the flaws of its ancestors. In some cases, the flaws were eliminated, while in others the problems remained.

Some of the successes of RPM version 1 were:

- Automatic handling of configuration files. The contents of config files are often changed from what they were in the original package, making it hard for a package manager to know how a particular config file should be handled during installations, upgrades, and erasures. PM made an attempt at config file handling, but in RPM it was further improved. In many respects, this feature is the key to RPM's power and flexibility.
