Some packages can be installed but should not be updated. These packages include kernel, kernel-PAE and others, as set by the default *installonlypkgs* value in yum. Because kernel packages are stored separately, we can keep multiple kernel packages installed on your system. By default, the *installonly_limit* value of 3 in /etc/yum.conf keeps the latest three *installonlypkgs* on your system, but will delete older packages of the same name as new kernel packages are added.

Here are some tips relating to setting up *yum.conf*:

+   * **Getting metadata** — The metadata that describes the contents of a yum repository is downloaded to your computer when you run the yum command. If you run the command again after the metadata expires (1.5 hours by default, as described earlier), you will have to wait again while yum checks to see if new metadata is available to download before yum proceeds. If available, yum downloads the new metadata.
+   
+   If yum is configured to access several repositories, it can take a long time to repeatedly check and update metadata. To get around this problem, you can extend the *metadata_expire* value or run yum with a *-C* on the command line (to use the existing metadata). The downside is that if the repository data has changed, you might not be getting the latest packages.

+   * **Excluding repositories** — Excluding repositories on the yum command line is another way to save time by preventing unneeded metadata from being downloaded. For example, if you know a package you want is in Fedora, disable the free *rpmfusion* repository by adding *--disablerepo=rpmfusion-free* or *--disablerepo=rpmfusion-* to the yum command line.

+   * **Plugins** — Fedora comes with the *plugins* feature enabled. This causes plugins in the */usr/lib/yum-plugins* directory to be enabled. When you start out, you may have no plugins or only the *refresh-updated* plugin. This plugin tells yum to notify the *yum-updated* daemon to refresh yum metadata. For information on other available plugins, refer to theYumPlugins Wiki (http://wiki.linux.duke.edu/YumPlugins).

For more information about the *yum.conf* file, type **man yum.conf** from a shell.

# Adding yum repositories (/etc/yum.repos.d/)

When you use the yum command to request to install a software package, it checks repositories listed in the /etc/yum.conf file and in files in the /etc/yum.repos.d directory. By default, you begin with repository listings from the following:

+   * **Fedora (fedora repo)** — This includes the same packages that are on the DVD that comes with this book. You can install any of those packages, or updates to them, from the repositories using *yum*. There are thousands of software packages in this repository.

+   * **Fedora Updates (fedora-updates repo)** — As updates become available from Fedora, you can automatically access those updates from mirror sites listed in *fedora-updates* repo.