+   • If you need to highly customize your searches and your search results, investigate the -L, -s, and -q flags in pkg-search(8).

# ## Examining Found Packages

Perhaps you’re not sure whether a package is what you really want. You might look up details on the package from a third-party site, like FreshPorts (https://www.freshports.org/), but that would require leaving your terminal, and I can’t countenance that. Use the -R flag to examine the repository catalog’s metadata for the package. This metadata is a subset of the full package manifest built into each package.

```
# pkg search -R apache24
name: "apache24"
origin: "www/apache24"
version: "2.4.25_1"
comment: "Version 2.4.x of Apache web server"
maintainer: "apache@FreeBSD.org"
www: "http://httpd.apache.org/"
--snip--
```

The package manifest includes fields for the package name, the port the package is built from, the software version, the package repository, dependencies, and more. It’s rarely enough used and subject to change, so we won’t discuss it in detail, but scrolling through this information provides more details about the software inside the package.

One important detail here is the www field, which gives the website the original software comes from. This is the Apache web server, not a fork or some other project using that name.

The default format for this raw manifest is YAML, or “YAML Ain’t Markup Language.” It’s yet another syntax for formatting configuration files, but it’s fairly human-readable. Use the --raw-format flag to choose an alternate format. Other supported formats include json and json-compact.

```
# pkg search -R --raw-format json-compact apache24
```

If you want to automatically parse package information, this is how you grab the raw data.