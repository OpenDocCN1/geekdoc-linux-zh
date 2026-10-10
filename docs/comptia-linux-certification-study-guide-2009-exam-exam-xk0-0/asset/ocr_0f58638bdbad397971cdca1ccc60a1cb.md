deb http://security.debian.org/ lenny/updates main contrib

deb-src http://security.debian.org/ lenny/updates main contrib

deb http://volatile.debian.org/debian-volatile lenny/volatile main contrib

deb-src http://volatile.debian.org/debian-volatile lenny/volatile main contrib

There is an internal database kept by APT to track the packages that are currently installed, those that are not installed, and those that are available to be installed. You can use the `apt-get` command to query this database, install and remove packages, and to check for dependencies in packages. As this list changes when new packages are added and new dependencies come into force, the list needs to be updated. This is achieved using the following command:

```
apt-get update
```

# Installing Packages

Packages can be installed using the `install` option, with the general syntax of

```
apt-get install package_name(s)
```

An example of the first part of the output is shown below when the abword package is installed:

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  abword-common abword-help abfonts abiword-plugin-grammar abiword-plugin-mathview
  aspell-en-doc-base latex-xft-fonts libaiksaurs-1.2-0c2a
  libaiksaurs-1.2-data libaiksaursgkt-1.2-0c2a libfreeze thaw-perl
  libfribidi0 libgdom2-0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a liblink-grammar4
  liblousmouth-l-0 libmldbm-perl libots0 libt-l-5 libuuid-perl libwv-l-2-3
  link-grammar-dictionaries-en
Suggested packages:
  abword-plugin-goffice
The following NEW packages will be installed:
  abword abword-common abword-help abiword-plugin-grammar
  abiword-plugin-mathview aspell-en-doc-base latex-xft-fonts
  libaiksaurs-1.2-0c2a libaiksaurs-1.2-data libaiksaursgkt-1.2-0c2a
  libfreeze thaw-perl libfribidi0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a
```