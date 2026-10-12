
some formulas as well as showing you how to build a basic Data Pilot later on in this chapter.

- **Impress**—This presentation program is similar to Microsoft PowerPoint and enables you to create slide show presentations that include graphs, diagrams, and other graphics. Impress also works well with PowerPoint files. When it is opened, Impress starts with a wizard that steps you through the creation of a new presentation, lets you use an existing template (although none is provided), or allows you to open an existing presentation.

- **Math**—This math formula editor enables you to write mathematical formulas with a number of math fonts and symbols for inclusion in a word processing document. Such symbols are highly specialized and not easily included in the basic functionality of a word processor. It is of interest primarily to math and science writers, but Math can be useful to anyone who needs to include a complex formula in their text.

- **Base**—This database was introduced with the OpenOffice.org 2.0 suite, which is provided with Fedora. It provides a fully functional database application. When you open Base, you are asked to set up the database for use. The easy-to-use setup assistants take you through most of the hard work.

- **Draw**—This graphics application allows you to create images for inclusion in the documents produced with OpenOffice.org. It saves files only in OpenOffice.org format, but it can import most common image formats. It is not meant as a replacement for more general graphics applications, but it has enough features to meet most needs.

- **Dia**—This technical drawing editor from the GNOME Office suite enables you to create measured drawings, such as those used by architects and engineers. Its functionality is similar to that of Microsoft Visio.

- **Planner**—You can use this project management application for project planning, scheduling, and tracking; this application is similar to, but not compatible with, Microsoft Project. It is found in the Office menu as the Project Planner item.

## A Brief History of OpenOffice.org

The OpenOffice.org office suite is based on a commercial suite called StarOffice. Originally developed by a German company, StarOffice was purchased by Sun Microsystems in the United States. One of the biggest complaints about the old StarOffice was that all the component applications were integrated under a StarOffice “desktop” that looked very much like a Microsoft Windows desktop, including a Start button and menus. This meant that in order to edit a simple document, unrelated applications had to be loaded, making the office suite slow to load, slow to run, and quite demanding on system resources.

After the purchase of StarOffice, Sun Microsystems released a large part of the StarOffice code under the GPL, and development began on what has become OpenOffice.org, which is freely available under the GPL. Sun continued development on StarOffice and released a commercial version as StarOffice 6.0. The significant differences between the free and commercial versions of the software are that StarOffice provides more fonts and even more import/export file filters than OpenOffice.org (these filters cannot be provided on the GPL version because of licensing restrictions) and StarOffice provides its own relational database, Software AG's Adabas D database. The StarOffice counterpart to OpenOffice.org 2.0 is StarOffice 8.

## Installing and Configuring OpenOffice.org

Fedora provides an RPM package for OpenOffice.org. If you do not install the RPM package during your initial Fedora installation, you can install it later, using the Add/remove Applications tool or by using `yum install openoffice.org` from the command line.

> **TIP**
>
> OpenOffice.org is constantly improving its productivity applications. You can check the OpenOffice.org website (http://www.openoffice.org/) for the latest version. The website provides a link to download the source or a pre-compiled version of the most current working installation files. A more current version might offer file format support that you need. Should you need a Windows compatible version, you will also find it at the website. Sometimes the version that Fedora provides can be a little unstable. If you find that this happens, you are best advised to go to the OpenOffice.org website and download the Linux version. OpenOffice.org is packaged in RPM format, so refer to Chapter 7, "Managing Software," for instructions on how to use the rpm command.

The installation of OpenOffice.org is done on a systemwide basis, meaning that all users have access to it. However, each user has to go into OpenOffice.org to configure it for their individual needs. This initial configuration happens transparently the first time you load any of the OpenOffice.org components, and might mean the application takes a little longer to load as a result. Be patient, and your desired application will appear.

Shown in Figure 9.1 are icons on the left of the top desktop panel that represent the different components of OpenOffice.org as well as other applications. From left to right, beginning with the Applications and Actions menus, the icons represent the Firefox web browser, Evolution email, OpenOffice.org Writer, OpenOffice.org Impress, and OpenOffice.org Calc. The icons displayed on your desktop might vary from those shown here. If you click the Applications icon, the main menu opens, and all the OpenOffice.org applications can be accessed from the Office menu.

As is the case with many Linux applications, you may be somewhat overwhelmed by the sheer number of configuration options available to you in OpenOffice.org. Thankfully a lot of thought has gone into organizing these options, which are available by clicking the Tools menu and selection Options. It does not matter which program you use to get to this dialog box, it appears the same if summoned from Writer, Impress, or Calc. It acts as a central configuration management tool for all OpenOffice.org applications. You can use it to set global options for all OpenOffice.org applications, or specific options for each individual component. For instance, in Figure 9.2, you can change the user details and information, and this is reflected across all OpenOffice.org applications.

## 246 CHAPTER 9 Productivity Applications

![](img/2045828cf45e5632bf056f9ca99d6755_281_0.png)

**FIGURE 9.1** The OpenOffice.org suite provided by Fedora is simple to configure and use.

![](img/2045828cf45e5632bf056f9ca99d6755_281_1.png)

**FIGURE 9.2** You can set user details for all OpenOffice.org applications from this dialog.

> **TIP**
>
> Two websites provide additional information on the functionality of OpenOffice.org:
>
> http://linguacomponent.openoffice.org/download_dictionary.html—This site provides instructions and files for installing spelling and hyphenation dictionaries, which are not included with OpenOffice.org.
>
> http://sourceforge.net/projects/oextras/—This site provides templates, macros, and clip art, which are not provided with OpenOffice.org.

OpenOffice.org is a constant work in progress, but the current release is on par with the Sun-version of StarOffice 8.0. You can browse to the OpenOffice.org website to get documentation and answers to frequently asked questions and to offer feedback.

## Working with OpenOffice.org Writer

Out of all the applications that make up OpenOffice.org, the one that you are most likely to use on a regular basis is Writer, the OpenOffice.org word processor. With a visual style very similar to Microsoft’s Word, Writer has a number of strengths over its commercial and vastly more expensive rival. In this section you will learn how to get started with Writer and make use of some of its powerful formatting and layout tools.

### Getting Started

You can access Writer either through its shortcut on the panel or by going to the Applications, Office menu and selecting Word Processor. After a few seconds Writer opens up with a blank document and a blinking cursor awaiting your command. It can be tempting to just dive in and start typing your document, but it can be worthwhile to do some initial configuration before you get stuck in.

First of all, make sure that the options are set to your requirements. Click the Tools menu and select Options to bring up the Options dialog box as seen in Figure 9.2. The initial screen allows you to personalize OpenOffice.org with your name, address, and contact details, but there are options to configure features that you might also want to alter. First of all, check that your default paths are correct by clicking the Paths option. You might want to alter the My Documents path, as shown in Figure 9.3, to something a little more specific than just your home directory.

![](img/2045828cf45e5632bf056f9ca99d6755_282_0.png)

**FIGURE 9.3** Click the Edit button to choose your default documents directory.

You might also want to change OpenOffice.org so that it saves in Microsoft Word format by default, should you so require. This can be done under the Load/Save General options shown in Figure 9.4, and it is a good idea if you value your work to change the Autorecovery settings so that it saves every couple of minutes.

Also shown in Figure 9.4 are a set of options that are specific to Writer. From top to bottom, they are

- **General**—Specify options that affect the general use of Writer
- **View**—Specify what you want Writer to display
- **Formatting Aids**—Specify whether you want to see non-printing characters
- **Grid**—Create a grid that you can use to snap frames and images in place
