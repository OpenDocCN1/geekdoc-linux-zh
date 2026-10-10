```
# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation
# process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
$ 
```

First, notice that the file is full of helpful comments and warnings. The repository sources specified use the following structure:

```
deb (or deb-src) address distribution_name
package_type_list
```

The `deb` or `deb-src` value indicates the software package type. The `deb` value indicates it is a source of compiled programs, whereas the `deb-src` value indicates it is a source of source code.

The `address` entry is the software repository’s web address. The `distribution_name` entry is the name of this particular software repository’s `distribution` version. In the example, the `distribution` name is `focal`. This does not necessarily mean that the `distribution` you are running is Ubuntu’s Focal Fossa; it just means the Linux `distribution` is using the Ubuntu Focal Fossa software repositories. For example, in Linux Mint’s `sources.list` file, you will see a mix of Linux Mint and Ubuntu software repositories.

Finally, the `package_type_list` entry may be more than one word and indicates what type of packages the repository has in it. For example, you may see values such as `main`, `restricted`, `universe`, or `partner`.

When you need to add a software repository to your `sources` file, you can try to wing it yourself, but that more than likely will cause problems. Often, software repository sites or various package developer sites will have an exact line of text that you can copy from their website and paste into your `sources.list` file. It’s best to choose the safer route and just copy/paste.

The front-end interface, `apt`, provides intelligent command-line options for working with the Debian-based `dpkg` utility. Now it’s time to take a look at the Red Hat–based `distributions`’ `rpm` utility and its various front-end interfaces.