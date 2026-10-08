# Chapter 19: Adding, Removing, and Updating Software

in binary format, as firmware and binary fonts. The main portion of the repository is designed to provide everything most people will need for a functional Linux desktop or server system that is fully supportable by Canonical, Ltd.

+   **Restricted:** The restricted repository contains source and binary packages for commonly used software that is not available under a free license. Packages in the restricted repository are not guaranteed to be supported by Canonical, but are provided because they are necessary to use Linux on certain hardware. For this reason, some items from the *restricted* repository are included in Ubuntu installer cds in subdirectories of *dists/dist_name/restricted* and *restricted/. Restricted items typically include drivers for specific network interface cards (NICs) and video cards.

+   **Universe:** The universe repository contains binary and source packages for the rest of the free and open source software that is commonly associated with Linux systems, that is available under a variety of different licenses and is not guaranteed to be supported by Canonical, Ltd. There's simply too much software in the universe (pardon the expression) for Canonical to guarantee support for all of the software it contains.

+   **Multiverse:** The multiverse repository contains binary and source packages for software that is not released under a license that meets the Ubuntu guidelines for free and open source software (www.ubuntu.com/licensing). This software is not supported by Canonical, Ltd., and it is your responsibility to verify that you satisfy the requirements imposed by software from the multiverse.

# Note

The official descriptions of the official Ubuntu repositories are located at www.ubuntu.com/ubuntu/components — I've tried to distill them down to their essentials, but if you're a licensing fan, there's plenty of good reading there. ■

Two additional repository components also exist, known as the backports and partner repositories:

+   **Backports:** The backports repository component contains outdated or bleeding-edge versions of Linux software, including software that may already have an official version in one of the other repository components. Software in this repository is not supported by Canonical but is provided because newer versions of existing software packages offer some critical feature that users may require.

+   **Partner:** The partner repository component contains software that is produced by various partners of Canonical. Software in this repository component is not supported by Canonical but is provided as a convenience to Ubuntu users who need access to software.

# Tip

If you are curious about the packages that are installed or available in the Ubuntu repositories for different releases, see the web page at http://packages.ubuntu.com. This page enables you to select the distribution that you are interested in and view a list of all the packages, organized into various logical categories. It also provides a search capability so that you can search for specific packages.

673