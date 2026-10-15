
# INSTALLATION

> Managing your packages and updating your system is a key part of the command line

## 032 Debian: update repositories

Debian-based (Ubuntu-based) distros use `apt-get` as the command line package manager. One of the quirks of `apt-get` as a manager is that before updating or installing center, it does not check if there is a newer version of the repositories before any installation in Debian.

## 033 Debian dependencies

Compiling offers between software and they'll have a guide on how to go about it. The problem you might face is that it will stop until you find and install the right dependency. By installing `apt-auto` and then using it with configuration:

```bash
sudo apt-get update
sudo apt-auto run --configure
```

## 034 Red Hat: uninstall software

`yum` can choose to uninstall any package that you have on your system, whether it installed directly from `yum` or not. As long as you know the package name you can uninstall:

```bash
sudo apt-get update
sudo apt-auto run --configure
```

## 035 Debian: install software 

Unlike a graphical package manager or center, to search for the list of packages you want to install you need to know the package name before installing. Once you do, though,

## 036 Debian: force install

Sometimes when installing it will refuse to install if specific requirements are not met needing to be installed for the software properly. You can force the package to install even without the dependencies.

## 037 Red Hat: remove package

The `yum` function `install` on Red Hat and Fedora-Linux distros requires that you have a package downloaded and ready. You can download with `yum` and then install it with:

```bash
sudo apt-get install
sudo apt-get download
sudo rpm -vhf --force
```

## 038 Debian: update software

You can upgrade the software in Debian by the first term performing the repository update command in Tip 32, follow by the upgrade command.

```bash
sudo apt-get upgrade
```

## 039 Red Hat: manual installation

`RPM` is the package manager on Red Hat and can be installed locally packages. You can either do something like in Tip 45 and download the package from the repos or download it from the internet and with:

```bash
sudo apt-get upgrade
sudo rpm -i
```

## 040 Debian: uninstall software 

As a package manager, `apt-get` is the simple way to install, upgrade and remove software as well. Installing is sometimes simple by replacing in with a newer version, but sometimes you need to use `apt-get` to remove the old version.

## 041 Debian: force install

Sometimes when installing it will refuse to install if specific requirements are not met needing to be installed for the software properly. You can force the package to install even without the dependencies.

## 042 Red Hat: remove package

The `yum` function `install` on Red Hat and Fedora-Linux distros requires that you have a package downloaded and ready. You can download with `yum` and then install it with:

```bash
sudo apt-get install
sudo apt-get download
sudo rpm -vhf --force
```

## 043 Debian: update software
