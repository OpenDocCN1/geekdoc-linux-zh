+   Dia—This technical drawing editor from the GNOME Office suite enables you to create measured drawings, such as those used by architects and engineers. Its functionality is similar to that of Microsoft Visio.

+   Planner—You can use this project management application for project planning, scheduling, and tracking; this application is similar to, but not compatible with, Microsoft Project. It is found in the Office menu as the Project Planner item.

# A Brief History of OpenOffice.Org

The OpenOffice.org office suite has its roots in an application known as StarOffice. Originally developed by a German company, StarOffice was purchased by Sun Microsystems in the United States. One of the biggest complaints about the old StarOffice was that all the component applications were integrated under a StarOffice “desktop” that looked very much like a Microsoft Windows desktop, including a Start button and menus. This meant that in order to edit a simple document, unneeded applications had to be loaded, making the office suite slow to load, slow to run, and quite demanding on system resources.

After the purchase of StarOffice, Sun Microsystems released a large part of the StarOffice code under the GPL, and development began on what has become OpenOffice.org, which is freely available under the GPL. Sun continued development on StarOffice and released a commercial version as StarOffice 6.0. The significant differences between the free and commercial versions of the software are that StarOffice provides more fonts and more import/export file filters than OpenOffice.org (these filters cannot be provided in the GPL version because of licensing restrictions) and StarOffice provides its own relational database, Software AG’s Adabas D database.

# Installing and Configuring OpenOffice.org

Fedora provides an RPM package for OpenOffice.org. If you do not install the RPM package during your initial Fedora installation, you can install it later, using the Add/remove Applications tool or by using yum install openoffice.org from the command line.

# TIP

OpenOffice.org is constantly improving its productivity applications. You can check the OpenOffice.org website (http://www.openoffice.org/) for the latest version. The website provides a link to download the source or the pre-compiled version of the most current working installation files. A more current version might offer file format support that you need. Should you need a Windows compatible version, you will also find it at the website.

The initial Fedora installation of OpenOffice.org is done on a systemwide basis, but no individual users are configured. To install local files and use OpenOffice.org, a user can simply click any OpenOffice.org icon on her desktop, and her files are installed by the installation wizard. This initial installation takes a little time, and OpenOffice.org unfortunately does not display a dialog about what is going on in the background. During the delay, some users might assume that the application has not started, but that is not the case.