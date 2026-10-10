# rpm

**Purpose:** Install/remove Red Hat Linux packages.

**Usage syntax:** `rpm [OPTIONS] [FILE]`

```
# rpm -iv nmap-4.85BETA9-1.i386.rpm
Preparing packages for installation...
nmap-4.85BETA9-1
...
```

![](bbox=[0.13, 0.25, 0.87, 0.27])

**rpm** is the traditional package manager for Red Hat Linux-based systems. It can be found on Red Hat Enterprise Linux and Fedora as well as a host of other Linux distributions built on the Red Hat/Fedora core.

Using **rpm** you can install or remove programs created specifically for Red Hat and Fedora-based systems. These packages typically have a `.rpm` file extension. The above example demonstrates using the **rpm** command to install an RPM package.

> **Note**
> 
> *Most Red Hat-based systems now utilize a program called **yum** to perform software installation tasks. Directly installing packages using **rpm** is rarely done given that **yum** will automatically download and install the requested package(s) and all required dependencies. See page 236 for more information.*

Common usage examples:

| | |
| :--- | :--- |
| `rpm -i [PACKAGE]` | Install the specified package |
| `rpm -U [PACKAGE]` | Upgrade the specified package |
| `rpm -e [PACKAGE]` | Remove the specified package |
| `rpm -qa` | List all installed packages |