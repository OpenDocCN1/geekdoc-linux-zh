# FLATPAK

# Get hold of up-to-date
software with Flatpaks

Aaron Peters went all in Ubuntu. deb package formats years ago, and has never looked back. That said, there's always time for a second opinion...

# Mode of operation

linux has made great strides in the area of software compatibility. Or more accurately, software is available however across the various distributions and their native package formats. This still requires the hard work of packers. They need to take an application and tweak it to fit the releases of different distributions, and even different ones. However, a universal package format has emerged, bringing the promise of 'once, run anywhere' (on Linux, anyway).

Flatpak (flatpak.org) is amazing and it's got a lot to learn. In this article we reviewed Flatpak in LF2024, explore how to use it and take a look at some important developments.

Flatpak is a package format, and tool to install and manage those packages. Many Linux package formats use the concept of dependencies, which a developer can define that package A depends on package B. When a user tries to install package A, the system will recognise it and install package B with it. This is how you install any application and end up with all the packages downloaded and installed.

In contrast, Flatpak provides both the application and everything it needs to run in a distro-environment. This approach has its pros and cons.

![](bbox=[0.555, 0.325, 0.905, 0.395])

A Flatpak file contains all the information necessary to find an application, determine its dependencies, and install it.

+   - Using the bleeding-edge version of an application, while keeping the standard version as well.
- LibreOffice, shown in the screenshot (on page 7) runs versions 5 and 6 at the same time.
- You have security concerns, and feel better with running a program in a sandbox. Example: Calibre.
- To use a more recent, stable, and/or more fully featured version of an application than your distribution provides.

As we saw in LF2024, there are other formats that provide similar advantages. This Ubuntu's Snap (snap..io) and Flatpak. They all perform multiple functions, Flatpak has a steeper learning curve compared to Snap.

+   - Snap is a Canonical project, and it's available to other distributions. Ubuntu if you use other distro, or just prefer a software system that isn't locked by yours. however, Flatpak is better than Snap.

+   - The approach of Flatpak is to avoid installing dependencies and running a single file. This is straightforward, but not necessarily easy, especially for new users. First off you need to download the Flatpak file to be installed, then you can run any incompatible version of the same library. The project offers an extra tool to do that, but you need to download and configure that yourself.

Despite all of this, Flatpak and Snap can use any (or all) of the formats on your machine at the the

![](bbox=[0.065, 0.445, 0.185, 0.55])

Aaron Peters wishes he was a programmer, but is happy settling for writing what he to do in the form of software documentation.

Flatpaks are identified by a source URL. The site you might use when naming code packages. The top-level domain comes first, then the domain name, and so on.

# QUICK TIP

| Pros | Cons |
|---|---|
| Distribution origin | Uses extra data with duplicate files |
| Ease of installation | It root or non-root users |
| No conflicts with system library | Server applications

We get basically that Flatpak is a format. Find a program, install and run run without worrying about what else is on your system may be an incompatible version of the same library. Furthermore, installing applications as Flatpaks allows you to match and match programs where you can't worry with your package system, such as:

110