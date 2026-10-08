# CHAPTER 11 | Managing OpenOffice.org Alerts and Updates

The developers behind OpenOffice.org update their software on a regular basis. When available, OpenOffice.org may be highlighted in an alert associated with one of the OpenOffice.org applications.

Some alerts may be addressed by an update to the OpenOffice.org suite. Others may be addressed in policy. For example, if a virus is transmitted through some image format, the bulletin may suggest that (and your users) avoid loading files with type of image—at least until the next version of the OpenOffice.org suite is made available.

When possible, it's easier to implement an update from the repositories associated with a distribution. But such updates aren't always available. For example, OpenOffice 3.x wasn't made available in the repositories for the Red Hat Desktop until a couple of years after OpenOffice.org version 3.0 was first released. But the OpenOffice 2.x series was still sufficiently capable for most users.

Users need OpenOffice.org 3.x on Red Hat systems could download associated packages directly from http://download.openoffice.org/. Updates are available in both Red Hat Package Manager (RPM) and Debian package formats for both Red Hat and Ubuntu-systems.

# Web Browsers

Web browsers are one area where choice may make life more difficult for security professionals. Half a dozen different browsers are available from regular Ubuntu repositories, easily accessible to users with direct online access. So it may be in your interest to limit what users can download and install. One method based on custom repositories is described in this chapter.

This section describes two browsers commonly used on Linux: Mozilla Firefox and Conqueror. Mozilla Firefox is the same source browser found on both Microsoft and Apple operating systems.

The Mozilla Foundation is the open source organization behind the Firefox browser and other open source tools like the Thunderbird e-mail manager and the SeaMonkey internet suite. Mozilla maintains a list of security announcements at http://www.mozilla.org/security/announce/. Such announcements are classified by product at http://www.mozilla.org/security/known-vulnerabilities.

In contrast, Conqueror is part of the KDE desktop environment. As security, issues are maintained by the developers at the KDE Foundation. Fortunately for KDE, there have been few security issues directly related to that desktop environment. As you can see at http://www.kde.org/info/security!, there have been a few dozen advisories released in the past decade of KDE software, including Conqueror as a Web browser.

# Adobe Applications

Given the popularity of Adobe formats such as the Portable Document Format (PDF) and Flash player, it's important for Linux administrators to monitor the status of such applications. Adobe security advisories can be found online at http://www.adobe.com/support/security/