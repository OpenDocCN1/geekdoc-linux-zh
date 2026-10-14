# NOTE

You can see a more extensive list of apt-get parameters by running apt-get without any parameters. The cryptic line at the bottom, "This APT has Super Cow Powers," is made even more cryptic if you run the command apt-get moo.

# Finding Software

With so many packages available, it can be hard to find the exact thing you need using command-line APT. The general search tool is called apt-cache and is used like this:

```
apt-cache search kde
```

Depending on which repositories you have enabled, that will return about a thousand packages. Many of those results will not even have KDE in the package name, but will be matched because the description contains the word KDE.

You can filter through this information in several ways. First, you can instruct apt-cache to search only in the package names, not in their descriptions. This is done with the -n parameter, like this:

```
apt-cache -n search kde
```

Now the search has gone down from 1,006 packages to 377 packages.

Another way to limit search results is to use some basic regular expressions, such as ^, meaning "start," and $, meaning "end." For example, you might want to search for programs that are part of the main KDE suite and not libraries (usually named something like libkde), additional bits (such as xmms-kde), and things that are actually nothing to do with KDE yet still match our search (like tkdesk). This can be done by searching for packages that have a name starting with kde, as follows:

```
apt-cache -n search '^kde.'
```

Perhaps the easiest way to find packages is to combine apt-cache with grep, to search within search results. For example, if you want to find all games-related packages for KDE, you could run this search:

```
apt-cache search games | grep kde
```

When you've found the package you want to install, just run them through apt-get install as per usual. If you first want a little more information about that package, you can use apt-cache showpkg, like this:

```
apt-cache showpkg mysql-server-5.0
```

This shows information on "reverse depends" (which packages require, recommend, or suggest mysql-server-5.0), "dependencies" (which packages are required, recommended, or suggested to install mysql-server-5.0) and "provides" (which functions this package gives