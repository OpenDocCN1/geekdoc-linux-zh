```
/etc/apt/trusted.pgp.kali-archive-keyring.gpg
-------
pub 4096R/7D0D0BF6 2012-03-05 [expires: 2018-02-02]
Key fingerprint = 44C6 513A B2E4 B3D3 0875 F7D8 ED44 4F0 7D8D 08F6
uid Kali Linux Repository <devel@kali.org>
sub 4096R/FC00D0CB 2012-03-05 [expires: 2018-02-02]
```

When a third-party package source is added to the sources.list file, APT needs to be trust the GPG authentication key (otherwise it will keep complaining that it can't ensure the authenticity of the packages from that repository). The first step is of to get the public key. More than not, the key will be provided as a small text file, which we will call key.asc in the following examples.

To add the key to the trusted keyring, the administrator can run apt-key add < key.asc. Another way is to use the synaptic graphical interface: Its authentication in the Settings -> Repositories menu provides the ability to import a key from the .asc file.

For people who prefer a dedicated application and more details on the trusted keys, it is possible to use gui-apt -key (in the package of the same name), a small graphical interface that manages the trusted keyring.

Once the appropriate keys are in the keyring, APT will check the signatures before any risky operation, that front-ends will display a warning if asked to install a package whose authenticity can't be ascertained.

# 8.4. Package Reference: Diving Deeper into the Debian Package System

Now it is time to dive really deep into Debian and Kali's package system. At this point, we are going to move beyond tools and syntax and focus more on the nuts and bolts of the packaging system. This behind-the-scenes view will help you understand how APT works at its foundation and give you insight into how to streamline and customize the Kali system. You may not necessarily master all the material in this system, but the walk-through and reference material will serve you as you grow in your mastery of the Kali Linux system.

So far, you have interacted with APT package data through the various tools designed to interface with it. Next, we will dig deeper and take a look inside the packages and at internal meta-information (or information about other information) used by the package management tools.

This combination of a file archive and of meta-information is directly visible in the structure of a .deb file, which is simply an archive, concatenating these files:

```
$ ar t /var/cache/apt/archives/apt_1.4-betal_amd64.deb
debian-binary
control.tar.gz
data.tar.xz
```

The Debian- binary file contains a single version number describing the format of the archive: