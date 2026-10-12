# ## Getting updates with up2date

Whether you have registered your computer with Red Hat Network or not, you can use the `up2date` command (or right-click the notification icon and click **Launch up2date**) to find and install updates. As with `rhn_register`, you need root access to your computer to run `up2date`. This is because `up2date` needs permission to change configuration files and install packages.

The `up2date` configuration file (`/etc/sysconfig/rhn/up2date`) determines the behavior of `up2date`. Here are a few of the key settings in the `up2date` configuration file to help you understand what `up2date` will do when you launch it:

+   * Debugging is disabled by default. Change `debug=0` to `debug=1` to turn on debugging if you are having trouble with `up2date`.
+   * Downloaded packages are stored in the `/var/spool/up2date` directory. After they are installed, the packages are deleted (by default).
+   * The `up2date` log file is `/var/log/up2date`. You can open the file in any text editor to see descriptions of everything `up2date` did.
+   * Any packages that begin with the word `kernel` are skipped. Add other package names you want skipped to the `pkgSkipList=kernel*` entry. You can use shell wildcard characters, such as the asterisk shown in the example, to match all kernel packages.

The `up2date` configuration file contains other settings that you can use to further refine your `up2date` session. For example, you can identify an HTTP proxy server, change the number of failed network-connection attempts that must occur before an exit, or indicate that you want to retrieve source packages along with the binary packages.

The `up2date` sources file (`/etc/sysconfig/rhn/sources`) is another configuration file you might consider making enhancements to. In particular, if you want to get updates of packages already installed on your system from yum or apt repositories, you can add the locations of those repositories to this file. The following two lines contain examples of entries you could add to the sources file for yum and apt repositories, respectively:

```
yum fedora-core-i386-stable http://download.fedora.us/fedora/fedora/3/i386
apt freshrmas-9-i386 http://www.freshrmas.net/fedora/linux/3/i386_updates freshrmas
```

The `yum` example shows the service as `yum` and the channel name is `fedora-core-i386-stable`, followed by the location of the `yum` repository. In the `apt` example, the repository is divided into three parts: the host name, path, and final directory. Notice that in this example, both `updates` and `freshrmas` directories are available repositories. Once you have added a line similar to the ones just shown, they appear as channels in the **Channel** window when you run `up2date`.

To use the official locations for packages from Red Hat Inc., you can simply use the default `up2date` settings. Here's an example of an `up2date` session: