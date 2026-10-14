![](bbox=[0.13, 0.12, 0.28, 0.22])

The same procedure is used for SUSE Linux Enterprise Desktop 10 service packs because they replace the original installation media.

In addition to the packages available for installation on the DVD, you can add external packages. You need to take only a few more steps to make these available. The following describes a directory structure to include software updates, but it can be used for external or custom packages as well.

+   1. To install the autoyast-utils package, log in as root and enter the following in a terminal window:
+   2. Run the create_update_source.sh command with the root of your installation repository as the argument:
+   3. Copy any RPM files you want to make available to the updates/suse/ architecture/ directory.
+   4. Change to that directory and run the updated_package_descr command:

```
yast -i autoyast2-utils
```

```
da10:~ # create_update_source.sh /export/sled10/
Creating /export/sled10//updates..
...
```

This will create the updates and yast directories as well as several subdirectories and files within your installation repository.

```
da10:/export/sled10/updates # cd suse/i386/
da10:/export/sled10/updates/suse/i386 #
create_package_descr -x setup/descr/EXTRA_PROV
using settings:
datadir: .
languages: english
output dir: ./setup/descr/
is not a directory: ignoring
extra_provides: setup/descr/EXTRA_PROV
done
processed 1 packages
now recoding to UTF-8: packages packages.DU
packages.en
da10:/export/sled10/updates/suse/i386 #
```