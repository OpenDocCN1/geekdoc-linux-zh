
Webmin 1.250 on rhel611.austin.com (Red Hat Enterprise Linux 66AS)

![](img/23b949da14ff7bab8762f0f0361af394_299_0.png)

Figure B-6 Example of a Webmin user interface window

# More Information

More information about Webmin, including project details, documentation, and access to the latest version available for download can be found at the Webmin site:

http://www.webmin.com

# Other important tools

## Tivoli management tools

Tivoli has a full set of management tools available for helping you handle the complexity of managing clients in an enterprise environment. Linux clients are supported by most of Tivoli's management tools, including tools that help monitor, manage, and deploy Linux client systems. Refer to the Tivoli Web site for more information about the enterprise management tools offered and their features:

http://www.ibm.com/software/tivoli

## Open Country OCM Suite

Open Country provides an enterprise level management tooling platform. It addresses many traditional large enterprise system management requirements. Some of those include: provisioning, system management, monitoring, updates, and asset tracking. For more information, see:

http://www.opencountry.com

## OpenNMS

OpenNMS is an open source distributed enterprise network and system management platform. The OpenNMS framework is SNMP-based and handles discovering network nodes and services, polling for their availability, and recording the system information for immediate use or creating thresholds. OpenNMS also gathers and reports network and service events. For more information about the project, to view a demo, or to download the itself, refer to the OpenNMS Web site:

http://www.opensms.org

## SBLIM

SBLIM is an acronym for Standards-Based Linux Instrumentation for Manageability. This open source project provides standard Web-Based Enterprise Management (WBEM) components. The goal of this project is to provide a complete Open Source implementation of a WBEM-based management solution for Linux. WBEM-based management is a growing method of managing clients using an object-based approach defined by the Distributed Management Task Force (DMTF).

The SBLIM components or packages help to provide a unified management strategy among Linux clients with distribution specific configuration files and management tools. It also provides an abstraction to simplification of common management tasks. The result is a common management method for handling system management tasks across different Linux clients.

You can read more about SBLIM project, the available packages, and the underlying technology at the SBLIM Web site:

http://sblim.sourceforge.net

## WBEM-SMT

Within the previously mentioned SBLIM project, a component of particular interest is WBEM-SMT. WBEM-SMT stands for WBEM Systems Management Tasks. The goal of the WBEM-SMT component is to improve the management features and ease of use of the Linux operating system. WBEM-SMT provides a set of task-oriented user interfaces that exploit the SBLIM WBEM-based instrumentation and automate many aspects of configuration.

One of the tasks that WBEM-SMT has provided is an interface for configuring DNS. An example of the DNS task can be seen in Figure B-7.

![](img/23b949da14ff7bab8762f0f0361af394_301_0.png)

Figure B-7 Example of a WBEM-SMT user interface window

More information about the WBEM-SMT package can be found at the SBLIM Web site at:

http://sblim.sourceforge.net/wbemsmt.html

# C

## Automating desktop migration using Versora Progression Desktop

This appendix describes the benefits of using an automated migration tool, such as Versora's Progression Desktop. It then expands upon the three ways to run Progression Desktop; manually with the GUI, manually with the command line, and automatically with a systems management tool. Finally, we describe Progression Desktop's extensible architecture.

## Benefits of an automated migration

A manual desktop migration is a time-consuming task. When dealing with a standard office or advanced office user, there are a myriad of technical considerations associated with the migration of data and application and system settings. A sample migration of e-mail, Web browser settings, and data is shown in Chapter 8, "Client migration scenario". Since a manual migration is estimated to require several hours of time per desktop, it could feasibly take an organization weeks or even months to complete. A Windows to Linux migration requires a technician to be proficient on both platforms with an understanding of the differences in file structures, applications, application settings, and system settings.

By using an automated tool in a large migration, a test machine or lab can be used to quickly lay the migration strategy. Any issues with the migration can be fixed in the test lab and rolled into the process. This allows for the least amount of downtime when it is time for the actual migration to begin. Use of automated tools provides predictable results that can be repeated simultaneously on desktops throughout the organization. Also, automated tools do not require the technician to have the same level of technical expertise required for a manual migration, because much of that knowledge is built into the program. When used in conjunction with systems management tools, certain automated tools allow one technician to migrate up to one hundred desktops in the same time period that a single migration requires.

## What is Progression Desktop

Progression Desktop by Versora is an example of a set of applications and tools that can automatically migrate system settings, application settings, and data from Windows to Linux. The Web site is:

http://www.versora.com

System settings include such as desktop wallpaper, keyboard and mouse settings, screen saver settings, system sounds, network shares, dial-up connections, and fonts. System settings can be applied to both GNOME and KDE desktop environments. Application settings include e-mail related settings as messages, address books, and calendar events; Web browser-related settings as favorites, cookies, and the browser home page; word processing-related settings as custom dictionaries, default templates, and AutoCorrect; instant messaging settings such as accounts and buddy list preferences. In each of these application categories, settings can be migrated from any source application to any of the destination applications. Some example mappings can be found in Table C-1.

Documents can be chosen by folder or by file, or even by file type. The documents can be copied as they are or sent through a conversion process based on file type to ensure compatibility on the target desktop. Progression Desktop also allows files to be excluded based on location or file type; for instance, a corporation might want to migrate the users' directories, but exclude all MP3 files or others that violate corporate policies.

## Table C-1 Some applications supported by Progression Desktop

| Category | Source applications | Destination applications |
| --- | --- | --- |
| E-mail | Microsoft Outlook Microsoft Outlook Express Mozilla Mail Thunderbird | Novell Evolution KMail Mozilla Mail Thunderbird |
| Web browser | Microsoft Internet Explorer Mozilla Mozilla Firefox | Konqueror Mozilla Firefox |
| Word processor | Microsoft Word OpenOffice.org Writer | OpenOffice.org Writer |
| Instant messaging | AOL Instant Messenger GAIM | GAIM Kopete |

## How to migrate with Progression Desktop

There are three ways to migrate clients with Progression Desktop:

- Using the provided GUI
- Using the command line with templates
- Using a systems management tool to automatically invoke the command line with templates

Each of these methods follows the same basic steps, as shown in the diagram Figure C-1. First, the Windows-based executable of Progression Desktop is run on the source desktop. This process retrieves information from each of the selected source applications and stores these settings into a neutral source. This neutral source, called a Platform Neutral Package (NP), must be made available to the destination machine. This step is accompanied by copying the file to a network share, or directly to the destination machine. Finally, the Linux-based executable of Progression Desktop is run on the destination machine. This process gathers information from the PNP and applies the settings to the appropriate location for each of the target applications.
