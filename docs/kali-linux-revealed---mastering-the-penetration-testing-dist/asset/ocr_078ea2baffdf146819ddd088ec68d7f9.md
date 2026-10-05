+   - Packages can be added to ( removed from) a live ISO by modifying package-lists/*.chroot files.

+   - Custom packages can be included in the live image by placing the .deb files in a packages chroot directory. Their installation can be preseeded with prese/*.cfg files.

+   - You can add files to the filesystem by putting them at their expected location below the includes.chroot config directory.

+   - You can execute scripts during the live system's chroot setup process by installing them as hooks/Live/*.chroot files. You can also execute scripts at boot time of the generated live image: you must arrange for them to be installed in /usr/lib/Live/config/XXX-name, for example by relying on the includes.chroot config directory.

+   - The Debian Live Systems Manual¹² is an excellent reference for live-build configuration and testing.

Setting encrypted and unencrypted persistence on a USB key: it's fairly simple to create a standard Kali Live USB installation. Although the process may seem syntactically complex, it is relatively straight-forward to add both encrypted and unencrypted persistence to your portable installation to significantly extend its functionality.

In the next chapter, we will discuss how Kali scales to the enterprise. We will discuss configuration management and show you how to extend and customize Kali Linux in a way that is easy to deploy whether you have a pair of machines, or several thousand.

> ²http://debian-live.alioth.debian.org/live-manual/unstable/manual/html/live-manual.en.html