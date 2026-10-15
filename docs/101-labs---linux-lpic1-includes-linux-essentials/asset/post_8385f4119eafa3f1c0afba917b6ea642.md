
# LAB 38

## Use RPM and YUM Package Management: `RPM`

**Lab Objective:**

Learn how to use the `RPM` package manager to install, uninstall, and obtain information on packages.

**Lab Purpose:**

`RPM` is a tool for installing `RPM`-based packages. It does not use repositories nor have automatic dependency resolution like `YUM` does, but it is useful for managing packages you may have downloaded outside of official repos.

> **IMPORTANT**: `RPM` is not pre-installed with Ubuntu and it may not install correctly. In that case, we recommend setting up another VM with a RedHat-based distro, such as CentOS.

**Lab Tool:**

A RedHat-based distro such as CentOS. Ubuntu is not recommended for this lab.

**Lab Topology:**

A single Linux machine, or virtual machine.

**Lab Walkthrough:**

### Task 1:

Open the Terminal and run: `rpm -qa`

This lengthy list is, of course, your list of installed packages. To get more information on a given package, try:

- `rpm -qs sudo`
- `rpm -q --dump sudo`

To install a package manually, you would run:

```bash
sudo rpm -i [file]
```

Where `[file]` can be either a downloaded `.rpm` or a URL.

Again, though, you would have to also install the dependencies manually first. To remove the package when you're done with it: `rpm -e [package]`

### Task 2:

Another useful tool is `rpm2cpio`. This tool converts a `.rpm` file into a `cpio` archive and spits it out on stdout. This makes it easy to access the files within, independent of `RPM`. For example:

```bash
rpm2cpio package.rpm | cpio -diium
```

### Notes:

Though `rpm` is great for information gathering, in practice it is generally better to manage your installed packages through a single central database. That may mean adding a third-party repo, or downloading a package and then manually adding it to `YUM`/`DNF`.

---

`DNF` is a newer tool which is replacing `YUM` in some distros. If you have one of these distros, you can safely replace all instances of `yum` with `dnf` in this lab.

### Task 2:

Let's say that you've downloaded the source code for some new and amazing application. Upon attempting to compile it, the code complains that `libvorbis.so` is missing. You can look to see if there's a package available containing it: `yum provides */libvorbis.so`

It turns out there are several, the most relevant of which being `libvorbis-devel` (you can run `yum info libvorbis-devel` to confirm that that is the correct package). If you were to install that package with `sudo yum -y install libvorbis-devel`, you would then be able to compile your application.

### Notes:

To experiment with a third major package manager, called `Zypper`, it is suggested to use a third distro, called `OpenSUSE`. This is outside the scope of this lab, but if you use `Zypper` after using `Apt` and `YUM` you will likely find that the commands and syntax are quite familiar.

---

# LAB 39

## Linux as a Virtualization Guest

**Lab Objective:**

Learn how to manage Linux desktops and servers in the context of virtualization.

**Lab Purpose:**

If you've followed the labs in order, you are probably running this lab in a VM. In addition to desktop virtualization, with the advent of "cloud computing" and IaaS, server virtualization has become a large part of everyday life for a professional Linux administrator.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux virtual machine running on VirtualBox

**Lab Walkthrough:**

### Task 1:

Open the VirtualBox Settings for the VM you are using for this lab. If possible, beef up the VM by doing the following (or if you don't have the system resources, then shrink resources assigned to the VM instead):

- Assign additional RAM and an additional processor to the VM
- Create another virtual disk image and assign it to the VM
- Assign an additional network adapter to the VM

Now reboot the VM and look to see if you can detect the additional resources. Does the memory show up in `free`? Can you see an extra processor with `lscpu`? Does `lsblk` show another disk? What about the network with `ip link show`?

The point of this exercise is to learn how easy it is to change the resources of a virtualized computer compared with a physical one. The same is true in the server world.

### Task 2:

In VirtualBox, make a clone of this VM. Boot it, access the Terminal, and run: `ip addr show`

Compare the results with the original VM. Are the IP address and MAC address the same, or were they automatically changed? (Depending on your settings, either could be the case.)

In a cloud scenario of multiple machines being cloned onto the same network, it is critical to make sure the network information is unique for each instance. This is also true of some security-related information, such as SSH host keys and the `D-Bus` machine ID.

### Task 3:

Finally, it is important to understand that guest VM's must have certain features beyond a generic Linux installation to make them usable as VMs. To illustrate this, run:

```bash
lsmod | grep vbox
```

You may see several VirtualBox-related kernel modules, such as `vboxguest`, `vboxsf`, or `vboxvideo`, among others. Additionally, specific kernel configuration is required: `grep GUEST /boot/config*`

### Notes:

`Cloud-init` is a package commonly used in cloud server environments to handle the unique per-server configuration on the first boot of an image deployment.

---

# LAB 40

## Work on the Command Line: Commands and Quoting

**Lab Objective:**

Learn basic Linux commands and shell syntax.

**Lab Purpose:**

The `Bash` command shell is pre-installed on millions of Linux computers around the world. Understanding how this shell works is a critical skill for working with Linux.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Open the Terminal application, then enter: `echo Hello World`

The `echo` command simply prints out all of the “words,” or arguments, that you give to it. This might not seem very useful, until…

### Task 2:

Now enter the following four commands, in order:

```bash
quote='cat /etc/issue'
backquote=`cat /etc/issue`
echo $quote
echo $backquote
```

Here, `quote` and `backquote` are called *variables*. In the first two lines, we set them to the values `"cat /etc/issue"` and `` `cat /etc/issue` ``, respectively. (We’ll get to the difference between quotes and backquotes in a minute.) In the last two lines, we reference the variables by putting `$` before them, and print out their contents.

### Task 3:

To understand single quotes, double quotes, and backquotes, enter the following:

```bash
hello="echo ""hello"""
echo "$hello"
echo '$hello'
echo `$hello`
```

Double quotes allow for variables to have their values referenced. Single quotes are always literal, while backquotes *execute* the command (including variable references) within those quotes.

### Task 4:

Now run the following commands:

- `pwd`
- `which pwd`
- `uname -a`

Can you figure out what these commands do? If not, there's another command—`man`—which could help you get some information.

Run `set -v`, then run the above commands again. You’ve just set the verbose flag in `Bash`, which repeats every command as you run it. To unset it, just run `unset -v`...

Just kidding! The completely unintuitive way to *unset* the `-v` flag is to `set +v`—run `set --help` to get more information on what `Bash` has available for customization; there's quite a bit.

`unset` actually has a different purpose, which is to unset variables. Observe:

- `foo=123`
- `echo $foo`
- `unset foo`
- `echo $foo`

**Notes:**

In some cases, you will want to reference variables with the `${variable}` syntax. This is equivalent to `$variable`, but the reasons for choosing one over the other are beyond the scope of this lab.

Backquotes also have an alternative syntax:

```bash
$(echo hello)
```



This syntax is generally preferred over `backquotes`. We only mention `backquotes` to distinguish them from single quotes and ensure the differences are clear.
