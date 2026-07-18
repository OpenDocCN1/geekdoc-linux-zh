![](Images/8f50737a-b9b3-4a8b-8f26-3786bfb60468.png)

![](Images/8f50737a-b9b3-4a8b-8f26-3786bfb60468.png)

# What this book covers

[Chapter 1](#b814b90c-1b8c-4ce8-bb04-1fc5a1ecad47.xhtml), *Installation, Reference and Help*, introduces the administrators to what .NET Core is, what its capabilities are, how it’s been implemented in Linux, and proceeds to introduce PowerShell. The chapter contains information on the history of PowerShell, how it is implemented on Unix-like systems, and how it differs from the currently-available shells.

[Chapter 2](#3f96cc43-1cb0-4c3c-8c3d-bded816886fe.xhtml), *Introducing the Core and its Capabilities*, takes the reader through how to install PowerShell, get around the documentation, search for information, discover cmdlets, and attach modules and providers to extend the capabilities of PowerShell.

[Chapter 3](#64bf6673-e6a4-45af-bbf5-79c92f40f8df.xhtml), *Preparing for Administration using PowerShell*, prerequisites to efficient administration is a comfortable workspace. In this chapter, we customize our Terminal, learn how PowerShell behaves, and learn to think in PowerShell along with the various ways to use the cmdlets.

[Chapter 4](#0b85b7b3-7cbf-4e9d-a5c1-cb7b00fb7d54.xhtml), *First Steps in Administration using PowerShell*, knows how PowerShell behaves, we start with basic utilities in PowerShell in this chapter, such as fetching the date and counting the returned objects. We work with processes and learn how to schedule them with the implementation of crontab in PowerShell.

[Chapter 5](#beccee73-7f30-4673-b1c9-919cf65971b6.xhtml), *Passing data through pipelines*, introduces the readers to use pipelines to leverage object-oriented model of PowerShell.

[Chapter 6](#83a80abd-5927-4e83-b31a-9a46e4725787.xhtml), *Using Variables and Objects*,takes the reader through defining and using variables effectively in scripts. Also, the chapter takes a deep dive into the objects returned by PowerShell cmdlets.

[Chapter 7](#bc6c5353-e3b1-4bcd-95e7-68d8b79f7ae5.xhtml), *Flow Control using Branches and Loops*,takes the reader through building a logic that uses branching and looping, as the basic logical building blocks of scripts and functions.

[Chapter 8](#20d73393-b166-4857-bf13-d153475e34cd.xhtml),* Working with Strings*, takes the readers through using them to the benefit of administrators.

[Chapter 9](#123e435d-0211-41ba-ba34-bb07d99bdb06.xhtml), *Performing Calculations*, would help the reader perform mathematical calculations within PowerShell.

[Chapter 10](#a86f9b5f-4098-4136-a57a-ef0c923ed0de.xhtml), *Using Arrays and Hash Tables*, gives the user a good understanding of how arrays and hash tables work in PowerShell and how to use them.

[Chapter 11](#00667dfe-b91d-40ac-88b4-146256e6deef.xhtml), *Handling Files and Directories*, would take the reader through all that they need to know on file handling using PowerShell.

[Chapter 12](#d7e18544-bf52-4156-8f8e-fb676042f74a.xhtml), *Building Scripts and Functions*, takes the user through creating scripts as a means of code reuse. Apart from writing a series of instructions to run scripts without interactions, the chapter takes the interactive scripts approach to enable better flexibility. Functions are a better way of leveraging PowerShell's potential in code reuse. This chapter also introduces the concept of functions as a step further from merely writing scripts.

[Chapter 13](#facd6558-bdb2-4cde-baae-a51c0c24fbe3.xhtml), *Advanced Concepts of Functions*, shows the next step in the process of building functions, and packs the advanced capabilities that help build production-ready functions that have all functionalities of a cmdlet, such as parameter sets and complete help.

[Chapter 14](#8c3c5fbb-9a67-44c0-bebb-e3dd4f1796f7.xhtml), *Getting Under the Hood: Debugging and Error Handling*, takes the readers through the various options available, that help scripters and administrators create reliable scripts. This chapter also introduces the reader to the different types of errors, reading errors in PowerShell, and handling them gracefully.

[Chapter 15](#f90cd558-5b45-4dfa-b604-6962e325c4cd.xhtml), *Working with the Environment*, introduces the reader to how PowerShell handles the environment. The reader would learn to use the environment variables, know how a command was invoked, and other important aspects that would make using PowerShell easier.

[Chapter 16](#9ab58466-c69b-427b-9f6a-11264677eccd.xhtml), *Security in PowerShell*, introduces the reader to the security features available in PowerShell, and how to turn them on and off.

[Chapter 17](#e67171c1-a22d-47d8-bfcd-effcd89f154a.xhtml), *Enterprise Administration using PowerShell*,enables the reader to tap into the power of PowerShell and start managing computers in an enterprise using PowerShell.

[Chapter 18](#455c7d93-81c3-416b-98bc-039ed38c1a3a.xhtml), *Best Practices Round-up*, the best practices are re-iterated so as to ensure that the reader remembers them, along with explanations to why they’re considered best practices.

[Chapter 19](#a164ee68-8be4-4c1b-9e98-db9d875106e1.xhtml), *PowerShell and Cloud Operations*, moves away from on-premises environments to see how we can administer Azure and AWS cloud platforms using the available options.

[Chapter 20](#447dd099-2243-49f9-a9c1-b3fbcdc94f77.xhtml), *Using PowerShell for SQL Database Management*, designes to teach you the fundamentals of using PowerShell to manage your SQL Servers, as well as perform development activities on them. It includes the installation and configuration procedures and also covers some  basic database administration tasks using SMO libraries in PowerShell.

# Table of Contents

# Preface

PowerShell 6.0 Linux Administration Cookbook will take you through a complete tour of understanding .NET Core, PowerShell in general, PowerShell on Linux for management and automation. This book will also cover advanced concepts on how to use PowerShell and manage Docker containers, Cloud, VMware and SQL databases.

# Installation, Reference and Help

In this chapter we're going to cover the following recipes:

1.  Installing PowerShell
2.  Fetching help information in PowerShell
3.  Fetching help information for a specific cmdlet
4.  Updating help
5.  Searching help for keywords
6.  Looking for help information specific to a parameter
7.  Exploring the `about_` topics
8.  Discovering cmdlets
9.  Finding modules
10.  Installing modules from the repository
11.  Listing the various providers in PowerShell

# Introduction

It all begins with the installation of PowerShell on your system. Installation of PowerShell is simple and straightforward. Since PowerShell is open source, its source code is available on the arguably largest platform for open source projects, GitHub. At the moment, Windows, Debian (and Ubuntu), RedHat Linux (and CentOS), Fedora and macOS are officially supported by **the PowerShell project**. Arch Linux and Kali Linux are supported by the community. Community support is also available for the AppImage edition of PowerShell that can be used on most of the modern-day Linux distributions.

An AppImage is a way of packaging applications to run on Linux distributions. Every application has its dependencies. On Linux, the package managers manage the installation of the dependencies while installing the packages. An AppImage package, on the other hand, packs all the necessary dependencies within itself. An AppImage can run in **portable** mode, or be installed on the system, based on user preference.

PowerShell is, as of writing of this chapter, experimentally available for Windows on ARM and Raspbian Stretch.

# Installing PowerShell

Basically, in Linux, it should be fairly simple to get the source code and build the application from the source code using make. This approach should work for PowerShell as well. However, as noted above, official support and community support are available only for a few distributions. We would focus on installing PowerShell on Ubuntu and CentOS since they are two of the most popular Linux distributions.

PowerShell is available in two releases: stable and preview. The stable releases are suitable for production environment since they're more reliable. The preview releases are for test environments where the administrators are allowed to feel a little adventurous, and are willing to report bugs they come across along with providing feedback on the capabilities.

# Getting Ready

Getting ready to install PowerShell on your computer is simple. You simply need a working Linux computer, which you have administrator privileges on. Depending on what mode you pick to install PowerShell, you may or may not need a package manager. Chances are, your Linux distribution already has a package manager available.

# How to do it...

As discussed, we will look at the procedure to install PowerShell on Ubuntu (and its derivatives) as well as CentOS (and its derivatives).

# Installation on Ubuntu

There really are many ways to install PowerShell on your computer. Since we're installing PowerShell on Ubuntu, we shall look at two ways to do it. The first is by adding Microsoft's key and registering the repository and then using the Advanced Package Tool (APT) to install PowerShell, and the other, directly using the .deb package from GitHub.

# Installing from the repository

The last version of Ubuntu that PowerShell has an official package for is Ubuntu 17.04\. If you have Ubuntu 17.04, use the steps below to install PowerShell. Otherwise, it is suggested that you use the direct download method.

1.  The first step is to import the GPG keys for the public repository:

```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

2.  Now that the key has been added, register the repository---this repository is maintained by Microsoft.

```
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.04/prod.list
```

3.  Update the package list using the following command.

```
sudo apt update
```

4.  Next, install PowerShell.

```
sudo apt install -y powershell
```

# Installing via direct download

Follow the steps below to install PowerShell on Ubuntu:

1.  Go to [https://github.com/powershell/powershell](https://github.com/powershell/powershell).
2.  Scroll down to the table that contains the list of Linux distributions officially supported by the PowerShell team.
3.  Click on the relevant link: `.deb` under Downloads (stable)—we will stick to the stable release.
4.  Read the installation instructions if you need additional information.
5.  Run the .deb file with `gdebi` or `eddy` or one such package installer to complete the installation.

If you aren't running one of the distributions supported officially by the Team or by the community, use the AppImage. Follow steps 1 and 2 from above, and:

1.  Click on Many Linux distributions | AppImage to download the Ap-pImage file. An AppImage file is a an application, packaged with all the dependencies required to run the application.
2.  Save the AppImage file at a convenient location.
3.  Once the download completes, navigate to the download location and run the AppImage.
4.  If you get a prompt asking if you would like PowerShell installed, choose the response appropriate to your environment.

# Installation on CentOS

Installation of PowerShell on CentOS 7 (or RedHat 7) also has two methods: the repository and direct download. The process is similar to that of installation on Ubuntu Linux.

# Installing from the repository

To begin installation:

1.  First, register the Microsoft repository.

```
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo
```

2.  Next, install PowerShell using `yum`.

```
sudo yum install -y powershell
```

# Installing via direct download

Follow the steps below to install PowerShell on CentOS:

1.  Go to [https://github.com/powershell/powershell](https://github.com/powershell/powershell).
2.  Scroll down to the table that contains the list of Linux distributions officially supported by the PowerShell team.
3.  Click on the relevant link: `.rpm` under Downloads (stable)—we will stick to the stable release.
4.  Read the installation instructions if you need additional information.
5.  Install the RPM package using the following command (assuming your download is at `~/Downloads` and your PWD is `~/Downloads`.

```
sudo yum install <the-downloaded-file.rpm>
```

# Using the AppImage package

Using the AppImage is much simpler.

1.  Go to [https://github.com/powershell/powershell](https://github.com/powershell/powershell).
2.  Scroll down to the Get PowerShell section, and find the AppImage link under community-supported distributions.
3.  Download the AppImage and place it at a convenient location.
4.  Run `chmod a+x PowerShell-<version>-<architecture>.AppImage` to make the AppImage executable.
5.  Call the AppImage to run PowerShell. You may be asked if you'd like the AppImage installed on your computer. Select Yes if you would like that.

# How it works...

The package manager installs the package with all its dependencies and makes the relevant commands available for use.

In case of the AppImage package, the dependencies are all bundled into the package (including .NET Core), and the package can either run in portable mode on your computer, or can be installed and called. Launch PowerShell by running `pwsh` to take a look.

# See also

1.  Recipe 2.5: Comparing Windows PowerShell and PowerShell

# Fetching Help Information in PowerShell

Commands in PowerShell are called cmdlets (pronounced: command-lets). Cmdlets come pre-packaged with all the necessary help information, just like the help available for any of the Linux commands. The difference is that there's a separate cmdlet available to get you the necessary help; help is not a switch in PowerShell.

Before we begin, let's launch the Terminal (launch any of the terminal emulators available on your computer). Let's now type `pwsh` to call PowerShell. Proceed with the steps below once you get the PS prompt.

To get help information in PowerShell:

Enter `Get-Help` at the prompt to get an overview of the help system in PowerShell. You would see an output like this:

![](Images/f608603b-ab54-460d-996d-23861db19141.png)

PowerShell cmdlets are built with help information written in them. Running `Get-Help` without any arguments would simply show you basic information on help available in PowerShell, which is not quite remarkable. Let us look at another recipe to leverage `Get-Help` a little better.

# Fetching Help Information for a Specific Cmdlet

While Get-Help shows information about help itself, it can also take in other cmdlets as arguments and show help for them. Let's pick `Get-Command` as an example and get help on the cmdlet.

# How to do it...

1.  At the prompt, type in the following:

```
Get-Help Get-Command
```

2.  You'd get an output like this:

![](Images/0f4996e6-5ed6-4bfe-a7da-c37a3cfc3d03.png)

3.  You can even get complete help on a cmdlet, including information about each of the parameter that you can use with the cmdlet; information such as whether the parameter is positional, mandatory and so on. We shall see in detail about each of these as we move into administration using PowerShell. To get full help on the cmdlet, enter:

```
PS> Get-Help Get-Command -Full
```

4.  To see examples of how to use the cmdlet, enter:

```
PS> Get-Help Get-Command -Examples
```

5.  To read help information online, enter:

```
PS> Get-Help Get-Command -Online
```

Notice that parameters are grouped in the output under SYNTAX. We can see two such groups in this case. These groups are called **Parameter Sets**. Parameter sets tell us which parameters can be grouped together. Two parameters not appearing within the same parameter set cannot be used together.

# How it works...

When you run the cmdlet, `Get-Help` with another cmdlet as the argument, `Get-Help` fetches help information for the cmdlet that was passed as the argument; `Get-Command` in this case. We shall see in the later chapters how arguments are handled. For now, we're simply calling the help for an arbitrary cmdlet.

If you notice the output, you'd see the name of the cmdlet, the syntax to use with the cmdlet, the alias available for the cmdlet and more online help if required. Full and Examples are switches which tell PowerShell the level of help you need. These are mutually exclusive; you cannot run `-Full` and `-Examples` at the same time.

# See also

1.  Recipe 2.6: Listing out the aliases and using them in place of cmdlets
2.  Recipe 1.4: Updating help
3.  Recipe 1.3: Fetching help information for a specific cmdlet (Information about Parameter Sets)

# Updating Help

Help information in PowerShell is dynamic. In most situations, PowerShell goes online to fetch the latest help. However, it is also possible to store the help files offline. This can be done using the cmdlet, `Update-Help`.

# How to do it...

To download the help files for the locally-installed PowerShell modules:

1.  Type `exit` to exit PowerShell. This is so that you can relaunch PowerShell with elevated privileges.
2.  Enter `sudo pwsh` to launch PowerShell as a super-user.
3.  At the `PS` prompt, run `Update-Help`.
4.  Wait for the update progress bar to appear. The bar will fill as the help files download to your computer.

![](Images/0475c76f-4e54-4f67-a125-cc9b7bd7f082.png)

# How it works...

PowerShell goes online to fetch help information every time you run the Get-Help cmdlet—the help files are not stored offline. This is primarily to ensure that only the latest help is referred. Besides, viewing help online also does not occupy space on the local computer.

In some cases, however, it is necessary that help information be stored for offline access. In such situations, it would make sense to download and store the help files.

One of the reasons this action requires elevated privileges is that the help information is stored within the shell. Therefore, non-administrators may not be able to update help without administrator intervention.

# Searching Help for Keywords

Linux administrators are very comfortable using `grep` to search for specific text patterns in any textual output. PowerShell, as we know, returns only **object**—PowerShell treats text as an object as well.

While converting an object into text diminishes the power of PowerShell, it still is necessary in some scenarios. In this case, we shall look for the keyword, “common” in the help output.

# How to do it...

Let us begin the process of searching by first getting the help information for a cmdlet:

1.  Launch PowerShell by entering `pwsh` at the terminal.
2.  At the prompt, type in:

```
PS> Get-Help Get-Command
```

This should give you helpful information on the specified cmdlet.

3.  Convert the output into text using the Out-String cmdlet along with the -Stream switch to return one string at a time rather than the whole of the help information as a single string. This way, we'd be able to run string matching more efficiently and get shorter search results.

```
PS> Get-Help Get-Command | Out-String -Stream
```

4.  There won't be a noticeable difference at the moment. Add the Select-String cmdlet to perform the grep-like operation.

```
PS> Get-Help Get-Command | Out-String -Stream | Select-String 'common'
```

5.  This gives you an output with the exact line that has the string, ‘common' in it.

![](Images/f417912f-ba4f-4748-a45f-ce68acc26dfc.png)

# How it works...

At the first step, we simply get the help information for the Get-Command cmdlet. This output is an object—performing a text lookup operation is best done when the output is text. Out-String converts this output into a plain string; the only issue is that the whole block of text is one single string. A text lookup this way may not be really helpful. We use the -String switch to break the large string into smaller pieces (paragraphs in this case). Next, we use the Select-String along with the keyword to select the string that contains our keyword.

# Looking for help information specific to a parameter

As we saw in the previous sections, PowerShell's help output could be a little overwhelming. We run `Get-Help` with the `-Full` switch when we need information on the parameters in the cmdlet whose help information we want to access. However, this lists out all the parameters. What if we wanted information on only a single parameter?

# Discovering Cmdlets

So far, we saw how to get help on cmdlets. We used the Get-Command cmdlet as the example argument. We would now use Get-Command to discover cmdlets in PowerShell. Get-Help and Get-Command thus become the most important cmdlets when you need any help information in PowerShell.

PowerShell is like plain English—PowerShell follows the Verb-Noun format in cmdlet naming, which makes the cmdlets sound like plain English commands. PowerShell even uses what's known as **approved verbs**, that ensures that verbs follow a convention when naming cmdlets. The nouns, on the other hand, can be arbitrary.

Most programmers would suggest learning to “think in the language”. This, combined with muscle memory (which helps you remember the keys on the keyboard), makes programming as well as scripting faster. PowerShell's structure being like English helps a lot in this regard; it's easy to think in PowerShell. For instance, if you would like to know the current date, all you have to say is, `Get-Date`, and PowerShell will print the date and time on the screen for you.

# How to do it...

Let us look at how to get information only about the `Noun` parameter of `Get-Help`.

1.  Invoke PowerShell by running `pwsh` on the terminal window.
2.  At the prompt, enter `Get-Help Get-Command` to look for basic help information on the cmdlet.
3.  Note down the parameter which you want more information about. Let's pick the parameter `Noun` as an example.
4.  Enter the following command at the prompt:

```
PS> Get-Help Get-Command -Parameter Noun
```

The output contains information specific to the `Noun` parameter:

![](Images/35e5d79d-da5e-48da-a3a1-2a533159bf7b.png)

# How it works...

This is a classic example of object filtering. Since the output of most PowerShell cmdlets are objects, it is easy to select the necessary object and discard the rest from the output.

When we run `Get-Help` with the cmdlet we need help about and the specific parameter of the cmdlet we are looking for, we get a filtered help specific to the cmdlet in question. In our case, we picked the Noun parameter of `Get-Command`.

# Exploring the About_ Topics

Documentation is one of the key strengths of PowerShell. While not all modules have complete documentation, all of the first-party modules do, along with the well-done third-party ones. By default, PowerShell itself has exhaustive documentation built within it.

In this recipe, we would look for `about_` topics, pick one of the topics from the output and read more about the subject we picked.

# How to do it...

Let us begin with listing out all the `about_*` helpfiles.

1.  Invoke PowerShell using the command, `pwsh`.
2.  Enter `Get-Help about_*` to list out all the `about_*` helpfiles.

```
Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
about_Aliases                     HelpFile
about_Arithmetic_Operators        HelpFile
about_Arrays                      HelpFile
about_Assignment_Operators        HelpFile
about_Automatic_Variables         HelpFile
.
.
.
about_Wildcards                   HelpFile
```

3.  Pick out the topic you'd like to read about—we pick `about_Modules`.
4.  Enter `Get-Help about_Modules` to read up on PowerShell modules.

```
ABOUT MODULES

Short Description
Explains how to install, import, and use PowerShell modules.

Long Description
A module is a package that contains PowerShell commands, such as cmdlets,
providers, functions, workflows, variables, and aliases.

People who write commands can use modules to organize their commands and
share them with others. People who receive modules can add the commands in
the modules to their PowerShell sessions and use them just like the
built-in commands.
.
.
.
How to Find the Commands in a Module

Use the Get-Command cmdlet to find all available commands. You can use the
parameters of the Get-Command cmdlet to filter commands such as by module,
name, and noun.
.
.
.
The following modules (or snap-ins) are installed with PowerShell. *
CimCmdlets * Microsoft.PowerShell.Archive * Microsoft.PowerShell.Core *
Microsoft.PowerShell.Diagnostics * Microsoft.PowerShell.Host *
Microsoft.PowerShell.Management...
```

# How it works...

`Get-Help` gives you information about cmdlets if the cmdlet is passed as an argument. In cases where you know only a part of the name of the cmdlet, you can use a combination of characters and wildcards to list out cmdlets that match the search string (`about_*` in our case).

Now, we pick the topic we would like to read about and enter that specific `about_` topic. Now, `Get-Help` shows the complete documentation about the topic.

# How to do it...

Get-Command can help determine the best cmdlet for a task. To find cmdlets, follow the steps below:

1.  At the Terminal, type `pwsh` to invoke PowerShell.
2.  Enter Get-Command to get a list of all cmdlets available in PowerShell. The number of cmdlets returned would change based on when you last updated PowerShell and the modules you've loaded.

```
PS> Get-Command
```

This may not be particularly useful—what would you do with a list of commands if you were looking for something to list out the currently-running processes?

3.  A process is a noun. We want a list of cmdlets that work on *processes*. At the prompt, type:

```
PS> Get-Command -Noun Process
```

Note that in PowerShell, the noun is in the singular form. Therefore, it's Process and not Processes.

4.  If you would like to further narrow down the list of cmdlets returned, add the verb as well.

```
PS> Get-Command -Verb Get -Noun Process
```

5.  If you're feeling lazy, or unsure of the exact conventions, you could even use the wildcard.

```
PS> Get-Command -Noun Proc*
```

6.  If you'd rather not write so much, and you're almost sure you know the partial cmdlet, you can straight away use wildcard search.
7.  If you know the name of the module which contains the cmdlet, you can even use the Module parameter when invoking `Get-Command`.

```
PS> Get-Command -Noun Process -Module Microsoft.PowerShell.Management
```

# How it works...

PowerShell has the capability to identify the verb and the noun in cmdlets, based on the first occurrence of hyphen. Anything that appears before the first hyphen is the verb, and anything that appears after, is the noun. When cmdlets are loaded from modules, PowerShell identifies the verbs and the nouns in them. The search promptly returns the cmdlets based on the search specifications. Filters based on the name of the verb, noun or even the module restrict the search accordingly.

# Finding Modules

Loosely coupling the components is one of the keys to success of a framework. PowerShell follows this principle as well. All cmdlets are packaged within modules. The modules can be first-party-provided, created by you, or even third-party-created.

Installation of modules, which could've been a hassle in the past, has been streamlined today. PowerShell now comes pre-packaged with a package manager called, `PowerShellGet`, that connects to the PowerShell gallery ([https://www.powershellgallery.com](https://www.powershellgallery.com)). The PowerShell gallery is an online repository that contains modules, scripts and other utilities that administrators can download and install in order to extend PowerShell's capabilities.

While it is possible to download PowerShell modules from third-party sites, our focus in this book would be the PowerShell repository.

# How to do it...

To find modules in the PowerShell repository, follow these steps:

1.  Launch PowerShell by running `pwsh` on the Terminal.
2.  Look for the command pertaining to modules.

![](Images/98edfcda-d148-4d35-a041-807f5ddd86f9.png)

Notice the list of commands available to work with modules. Some of them are of the cmdlet type, while others are functions.

3.  Filter the output further, using the verb.

```
PS> Get-Command -Noun Module -Verb Find
```

You get `Find-Module` as the output.

4.  Enter the following to list out all the modules.

```
PS> Find-Module
```

The list begins to appear. The search results are way too many. Press `Ctrl + C` to abort the execution.

5.  Search for a module to help you work with Docker containers.

![](Images/788be588-8afd-4bb8-9de4-0fe6ccba964e.png)

# How it works...

Hundreds of modules, scripts and Desired State Configuration resources have been registered with the `PSGallery` repository. Microsoft now recommends using the repository for module management. Using the `Find-Module` cmdlet, PowerShell makes a connection to the repository and gets a list of all available modules. Then, it runs a search on the returned results based on the criteria you mention.

You can also similarly find scripts that can perform repetitive tasks. To find scripts, use the `Find-Script` cmdlet. It works similar to the `Find-Module` cmdlet, except that it finds individual scripts rather than modules.

# Installing Modules from the Repository

Now that we know how to find modules, we can proceed with getting modules and installing them. All cmdlets pertaining to `PowerShellGet` are packaged in the module called, `PowerShellGet`.

# How to do it...

We now know the name of the module that would let us manage our Docker infrastructure. Let us now try to install the module.

1.  Installation of modules may require elevated privileges. Open PowerShell with `sudo`.

```
$ sudo pwsh
```

2.  Now run the following command to install the Docker module from the repository.

```
PS> Install-Module Docker
```

![](Images/b41b716d-f624-482c-8474-96b30d3b2e87.png)

3.  In some cases, you may want to save the module locally before you install it.

```
PS> Save-Module Docker ~/PsModules
```

This way, you can simply import the module in portable mode and run the cmdlets without having to install the module in any of the system directories.

4.  To import the downloaded module, run:

```
PS> Import-Module ~/PsModules/Docker/1.3.2/Docker.psm1
```

5.  To update the installed module, run:

```
PS> Update-Module Docker
```

6.  To remove an installed module, run:

```
PS> Uninstall-Module Docker
```

Most of these functionalities work with scripts published to the PowerShellGet repository as well. Just replace Module with Script in the cmdlet and that should do the trick—you can find, save, install, update and uninstall scripts the same way you do modules.

Downloaded scripts need not necessarily be installed; they can be directly called. We will see this in the later sections.

# How it works...

What PowerShell really does when running the `Install-Module` is, save the module files in one of the locations that PowerShell looks for modules by default.

# See also

1.  Recipe: Module discovery paths in PowerShell (Creating custom modules)
2.  Recipe 3.11: Calling a PowerShell script

# Listing the Various Providers in PowerShell

One more concept before we start preparing for administration using PowerShell would be to understand **providers**.

Providers in PowerShell are a great example of the concept of **overloading** in object-oriented programming. In essence, a provider is a program that logically represents non-file-system drives as though they were drives. For instance, on Windows, the Registry is a database of configuration. In PowerShell, the Registry is a provider; this way, administrators can use PowerShell to navigate and manipulate Registry keys as though they were files. This capability is available on Linux as well, however, the providers are not as many as found on Windows.

# How to do it...

To list out the providers in PowerShell, follow these steps:

1.  Run `pwsh` to load PowerShell on the Terminal.
2.  Run the command:

```
PS> Get-PsProvider
```

![](Images/f36012e9-b8ba-4762-9952-de78c5ce0ab4.png)

Note the providers available in PowerShell, and the drives and capabilities found *within* these providers.

3.  Navigate to the Alias: drive.

```
PS> Set-Location Alias:
```

![](Images/e52ce58e-5686-4671-816a-3cdff1cc4004.png)Notice the preceding colon after the drive name (Alias: and not Alias). This is important to indicate to PowerShell that you're switching drives. Without the colon, PowerShell would simply try to look for a directory called Alias in your present working directory.

# How it works...

As of now, PowerShell providers don't seem to work as intended, in Linux. However, in due course, this should be fixed.

Providers wrap the non-file-system like structures into themselves and present them to PowerShell as though they were files and directories. These allow you to navigate complex structures as though they were simply files and directories, which are easier managed using the commands that work on the file system, such as `Get-ChildItem`.

The `Capabilities` column in the output show capabilities such as `Credentials`, `ShouldProcess` and `Filter` for each of the providers. This means that the providers support passing credentials to the core, availability of parameters such as `-WhatIf` and `-Confirm` (which are part of `ShouldProcess`) and the ability to filter output using the `-Filter` parameter. We shall learn about each of these in the following chapters.

# See also

1.  Recipe: `ShouldProcess` capabilities such as `-Confirm` and `-WhatIf` (Functions)
2.  Recipe: Using the `-Filter` parameter

# Introducing the Core and its Capabilities

In this chapter, we cover the following topics:

1.  Dissecting a .NET Core object
2.  Breaking down an output into different objects
3.  Parsing input from text to object
4.  Comparing the outputs of Bash and PowerShell
5.  Comparing Windows PowerShell and PowerShell
6.  Listing out the aliases and using them in place of cmdlets
7.  Creating a custom alias
8.  Importing/Exporting custom aliases for future use
9.  Listing out the execution policies and setting a suitable one

# Introduction

Microsoft's announcement of "open sourcing" .NET in 2014 almost stirred a storm. Many rushed to the stands (so to speak) to read about the unbelievable—how could Microsoft possibly open-source the core of their operating system? Some were cynical, others rejoiced. Then came the announcement a little louder and clearer that .NET Core was open source, not the .NET Framework. Many said .NET Core was a subset of .NET Framework.

.NET was first announced in 2000, as a new platform based on Internet standards. Along with it, by the end of the year, Microsoft published the **Common Language Infrastructure** as a standard, so that anyone who wanted, could write their own .NET framework based on those standards. .NET Framework has been the basis of Windows since the noughties.

Windows PowerShell was released to the general market in 2006, as an implementation of .NET Framework, focussed on system administrators (or sysadmins, to enable them to better manage their Windows workloads and automate tasks.

In June of 2016, Microsoft released a collaboratively refactored, more modern and efficient .NET. The .NET Core was officially born. While .NET Framework continues to rule the Windows arena, .NET Core, which is open source and cross-platform, has picked up great momentum and continues to grow. And .NET Core seems to be the way forward.

PowerShell (not *Windows* PowerShell) is based on .NET Core, and therefore, is open source, with the same vision as .NET Core to be cross-platform.

In this chapter, we will look at a very simple implementation of .NET Core and compare it to the output of PowerShell to prove that PowerShell is nothing but encapsulated .NET Core code. Along with it, we shall look at the general behaviour of PowerShell as well.

# Dissecting a .NET Core Object

.NET Core works on a cross-platform standard Common Language Infrastructure. Therefore, it has been possible to encapsulate the internal workings of Linux using .NET Core. As we would see in the future chapters, PowerShell is object-oriented, just like .NET Core. For this demonstration, we would pick a simple system class, called `System.IO.DirectoryInfo` to show information about a certain directory. We will also compare the output .NET Core object to the output of a PowerShell cmdlet which also shows information about a certain directory.

You do not have to remember the names of the .NET Core classes, methods or their syntaxes to work with PowerShell; that's the whole point of the existence of PowerShell.

# Getting Ready

If you followed along the last chapter, you should already have PowerShell installed on your Linux computer; open a terminal window and type in `pwsh` to invoke PowerShell.

Every **object** has members—**properties** and **methods**. In case you're new to the concepts of Object Oriented Programming, properties are qualities of an object (what the object has), and methods are the capabilities of an object (what the object can do). Therefore, to quote (arguably) the most overused example of properties and methods: If a horse is an object, its height, its colour, etc. would be its properties; galloping, eating, etc. would be the methods that the object supports.

# How to do it...

1.  With PowerShell, .NET Core is also installed as a dependency. Let us create an object in PowerShell, which would call a .NET class and its default constructor. This constructor requires an argument.

```
PS> New-Object -TypeName System.IO.DirectoryInfo -ArgumentList '/home/ram'
```

2.  This gives us information on the directory specified, like so:

```
Mode                LastWriteTime         Length Name            
----                -------------         ------ ----            
d-----          5/16/18  11:03 AM                ram
```

3.  There is a cmdlet in PowerShell,  called, `Get-Item`, which gives us details about a directory. Let us call this cmdlet with the same argument as before, and see what we get.

```
PS> Get-Item '/home/ram'

    Directory: /home

Mode                LastWriteTime         Length Name            
----                -------------         ------ ----            
d-----          5/16/18  11:03 AM                ram
```

4.  Close! Let us now look at the *details* of the output object we just received, using the `Get-Member` cmdlet on the output of `Get-Item`.

```
PS> Get-Item '/home/ram' | Get-Member
```

`Get-Member` shows all the members available in the output object (most PowerShell cmdlets return objects as output, not plain text). For more information, run `Get-Help Get-Member`.

This would list a series of members that are part of the output. We're primarily concerned about the very first line for now.

```
PS> Get-Item '/home/ram' | Get-Member

   TypeName: System.IO.DirectoryInfo

Name                      MemberType     Definition
----                      ----------     ----------
LinkType                  CodeProperty   System.String LinkType{get=GetLinkType;}
Mode                      CodeProperty   System.String Mode{get=Mode;}
.
.
.
```

# How it works...

Notice the very first line of the output, `TypeName: System.IO.DirectoryInfo`. That is the exact type name we used when creating the .NET object.

![](Images/c1e7e64f-6963-4c88-9e96-ee87651fba00.png)

This proves that the same task of showing information on the current working directory can be achieved by calling a .NET constructor, or by running a PowerShell cmdlet. Therefore, we infer that PowerShell cmdlets are simply encapsulated .NET code, simplified to enable administrators to work with computers, without having to worry about the underlying .NET code.

In essence, `Get-Item` calls the `System.IO.DirectoryInfo` class under the hood, with the arguments passed along with the cmdlet.

`Get-Item` can be used with any location in your file system. As long as you are authorised to access the location, PowerShell would return information about the location you pass as the argument.

Like they say:

If the C# guys can do it, so can you.

# There's more...

Read the output of the `Get-Item | Get-Member` command to understand what more information you can get about the directory you specify. Also, after we are comfortable using the `Select-Object` cmdlet, we should be able to call specific fields from the returned objects.

# See also

1.  The .NET class, [System.IO.DirectoryInfo](https://msdn.microsoft.com/en-us/library/system.io.directoryinfo(v=vs.110).aspx) (Microsoft Developer Network)

# Breaking down an output into different objects

In the previous section, we saw that an object can have properties as well as methods. These properties and methods are known as members. In the object oriented approach to programming (and by extension, administration using PowerShell), it is possible to reference these properties as well as methods of an object using the **member access operator**, which is a single dot (`.`).

# Getting Ready

Ideally, this recipe should be an extension to the previous. If you did not run the previous commands, it is suggested that you do, and then proceed with the steps below.

# How to do it...

1.  Look at the output of the following command from the previous recipe:

```
PS> Get-Item '/home/ram' | Get-Member
```

The output table contains the name of the member, the type and the definition. Take a look at the `MemberType` column; you have `Method`, and different kinds of properties such as `CodeProperty` and `Property`.

2.  Assume that we would like to see when my home directory was last written to. We would refer to this property using the member access operator. To do this, simply enclose in parenthesis the `Get-Item` command along with its argument and refer to the property using the dot operator.

```
PS> (Get-Item /home/ram).LastWriteTime

Wednesday, 18 May 2018 11:01:02
```

3.  Next, let us pick the property, `Parent`, of the object. This should give us the details of the directory which my home directory resides in.

```
PS> (Get-Item /home/ram).Parent

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---       03/05/2018     17:07                home
```

This output in itself is an object, which means that we can fetch last write time and other details of this returned object, just like how we did for `/home/ram`. How do we see when the parent folder (`/home`) was created?

4.  First, let us use the `Get-Member` cmdlet on this object and see the `TypeName` of the returned object.

```
PS> (Get-Item /home/ram).Parent | Get-Member

   TypeName: System.IO.DirectoryInfo
```

It is the same as `Get-Item` itself. Therefore, any of the members of `Get-Item /home/ram` apply to `(Get-Item /home/ram).Parent` as well.

5.  Now call the `CreationTime` property on the parent object. Simply add a dot next to `Parent`, and call the `CreationTime` property.

```
PS> (Get-Item /home/ram).Parent.CreationTime

Thursday, 3 May 2018 17:07:38
```

The `CreationTime` property is an object in itself, of the type, `DateTime`. Therefore, you can perform date and time operations on this object.

PowerShell is not case-sensitive most of the time. However, it is recommended we stick to the conventions in order to minimise errors. Especially since case sensitivity is a convention in Linux. Properties could be of different data types. The data type can be seen in the `Definition` column.

6.  Let us look at the members of the `CreationTime` object to see if we can further filter the output.

```
PS> (Get-Item /home/ram).Parent.CreationTime | Get-Member

   TypeName: System.DateTime
```

7.  Let us pick only the year property from this object.

```
PS> (Get-Item /home/ram).Parent.CreationTime.Year
2018
```

This concludes picking properties from within the returned objects. Next, let us use a method from within the returned object and create a sub-directory under `/home/ram`.

1.  First, list out the existing directories under the directory. This is done using the cmdlet, `Get-ChildItem`.

```
PS> Get-ChildItem /home/ram

    Directory: /home/ram

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       06/04/2018     13:05                Desktop
d-----       18/05/2018     16:01                Documents
d-----       18/05/2018     16:01                Downloads
d-----       06/04/2018     13:05                Music
d-----       19/05/2018     11:07                Pictures
d-----       06/04/2018     13:05                Public
d-----       06/04/2018     13:05                Templates
d-----       10/04/2018     03:41                Videos
```

`Get-Item` gives you details about the directory itself. In essence, this cmdlet deals with the current item at hand. Therefore, you have properties and methods that align with that intention. Child items, on the other hand, mean the files and directories that are *within* the said item.

2.  That is a list of standard directories in a user profile. Let us now create a sub-directory within this profile folder, using a method in `Get-Item`.

```
PS> (Get-Item /home/ram).CreateSubdirectory('test-directory')
```

To know what argument a certain method accepts, look in the `Definition` column of the output of `Get-Member`. In case of `CreateSubdirectory`, the definition is `System.IO.DirectoryInfo CreateSubdirectory(string path)`.

You should now get a confirmation.

![](Images/d5608bd8-b8e8-471a-8413-8002dc6cf776.png)

3.  Excellent. Now, list out the directories under the home directory.

```
PS> Get-ChildItem /home/ram

    Directory: /home/ram

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       06/04/2018     13:05                Desktop
d-----       18/05/2018     16:01                Documents
d-----       18/05/2018     16:01                Downloads
d-----       06/04/2018     13:05                Music
d-----       19/05/2018     11:07                Pictures
d-----       06/04/2018     13:05                Public
d-----       06/04/2018     13:05                Templates
d-----       19/05/2018     13:31                test-directory
d-----       10/04/2018     03:41                Videos
```

We can now see the new directory that we created using the `CreateSubdirectory` method.

Running `Get-ChildItem`, as you may notice, is similar to running the `GetDirectories` and `GetFiles` methods of the object returned by `Get-Item`. This is another example of encapsulation in .NET Core.

# How it works...

Using the properties and methods within a returned object is simple. Objects from within the output returned by a cmdlet can be called using the member access operator directly on the command (cmdlet including the parameter).

Calling properties after the member access operator fetches the data that's held within the property. In our case, it was the `LastWriteTime`.

Methods are functions. They may or may not require an argument. The `CreateSubdirectory` method requires a string argument, which is the name (or path) of the sub-directory we wish to create—whatever we enter in the parenthesis essentially forms the path we wish to create. In case of methods that can run without an argument, they need to be called with empty parenthesis following the name of the method, like `ToString()`, for example.

When we pass the string argument into `CreateSubdirectory`, the method runs a .NET Core routine and creates a sub-directory within the directory we specify with `Get-Item`. The internal workings of the .NET Core is beyond the scope of this book.

# See also

1.  Recipe: Selecting objects via the pipeline

# Parsing input from text to object

Moving to the object model from text could seem a little daunting at first. However, with PowerShell, it is not very hard to switch to the new model, especially given that PowerShell can convert text into objects given the right tools. In this recipe, we would look at two of the ways that PowerShell converts textual data into objects.

# Getting Ready

Before we dive into the recipe, let us give ourselves a little introduction on how text-to-object parsing is handled. One way is to use .NET's built-in functionality, and the second one that we discuss involves using a cmdlet to perform the conversion based on a delimiter.

The basic requirement for this recipe is simple: you simply need PowerShell installed on your computer. We will edit the file within PowerShell. If you would be comfortable using a text editor instead, that works as well. Most Linux distributions pack a text editor. If not, use your package manager to install Vim, Nano, Gedit, Visual Studio Code, Atom or any other text/code editor.

# How to do it...

We shall first look at converting text into an object from plain text input at the terminal. This involves using what is known as a **PowerShell Type Accelerator**. A PowerShell Type Accelerator is a an alias for .NET classes. Using these, we can call .NET classes and use many of their functionalities within PowerShell.

1.  Let us take plain text as input and convert the text into a date object. To check what sort of object your input is, use the `Get-Member` cmdlet.

```
PS> '21 June 2018' | Get-Member
```

Enclosing any text within single quotes defines the text as a **non-expanding literal string**. No explicit definition is required in this case, in PowerShell.

2.  The `TypeName` says, `System.String`. This confirms that what we entered was plain text. Let us now use a Type Accelerator and convert this text into a `DateTime` object. The accelerator for this purpose is `[DateTime]`; place this accelerator before the literal string.

```
PS> [DateTime]'21 June 2018'

Thursday, 21 June 2018 00:00:00
```

3.  Next, find the `TypeName` of the object that was returned.

```
PS> [DateTime]'21 June 2018' | Get-Member

   TypeName: System.DateTime
```

Voila, the string has been successfully parsed into date and time!

4.  It is also possible to achieve the same result with the cmdlet, `Get-Date`, when it is called with the text argument.

```
PS> Get-Date '21 June 2018'

Thursday, 21 June 2018 00:00:00
```

5.  Similarly, the `TypeName` would be:

```
PS> Get-Date '21 June 2018' | Get-Member

   TypeName: System.DateTime
```

6.  Just like we did in the previous recipe, we can now manipulate the object to show information in a more meaningful way. For instance, if you care only about the year, you would write:

```
PS> (Get-Date '21 June 2018').Year
2018
```

The other way of converting text into an object is to use cmdlets that perform such tasks. PowerShell packs a few converter cmdlets, one of which is `Import-Csv`. You may have noticed that PowerShell usually sends out output in a tabular format. This is a simple representation of objects. And `Import-Csv` converts data in delimited row-and-column structure into objects, where each row is an instance of the object itself, and each column is a property of the object.

1.  To demonstrate this, let us create a CSV file with the following content in it. At the PowerShell prompt, type:

```
PS> @'
```

2.  This would take you to the next line; PowerShell is expecting input. Paste the following sample content at the prompt.

```
WS,CPU,Id,SI,ProcessName
161226752,23.42,1914,1566,io.elementary.a
199598080,77.84,1050,1040,gnome-shell
216113152,0.67,19250,1566,atom
474685440,619.05,1568,1566,Xorg
1387864064,1890.29,15720,1566,firefox
```

3.  Go to the next line and enter the following at the `>>` prompt:

```
'@ | Out-File sample.csv
```

You could perform the same operation using the `touch` command and the text editor of your choice. The goal is to get the content into the sample file.

4.  Next, read the contents of the file using PowerShell.

```
PS> Get-Content ./sample.csv
WS,CPU,Id,SI,ProcessName
161226752,23.42,1914,1566,io.elementary.a
199598080,77.84,1050,1040,gnome-shell
216113152,0.67,19250,1566,atom
474685440,619.05,1568,1566,Xorg
1387864064,1890.29,15720,1566,firefox
```

5.  That looks like simple text. Let us look at the type name of the object to confirm that this is indeed plain text. Type in:

```
PS> Get-Content ./sample.csv | Get-Member

   TypeName: System.String
```

6.  That is plain and simple string. Let us now convert the content into a simple object. This is done using `Import-Csv`.

```
Import-Csv ./sample.csv
```

That should give you a list-like output.

![](Images/421790f7-a304-47d2-8a53-8d8b24057760.png)

7.  To confirm the output is objects, list out its members.

![](Images/2ce2642a-5e63-4f99-85ca-3dcba5ee4bcb.png)

In general, the content is a custom object, as denoted by `PSCustomObject`. The columns we had in the CSV are of type `NoteProperty`, as shown by `MemberType`.

A `NoteProperty` is a generic property, whose characteristics are similar to string. While most properties are inherited from .NET, `NoteProperty` is custom-created within PowerShell, as a name-value pair.

8.  If you would rather look at the content as a table, format the content as a table.

```
PS> Import-Csv ./sample.csv | Format-Table
```

![](Images/653c86b0-0db0-4230-9e4d-86c4a23a5109.png)

That brings us to the end of this recipe. We have successfully converted text into an object. However, note that this is just a simple conversion, and that the output of `Import-Csv` is still string-like. Although, all of the content is now objects, which are easier to handle in PowerShell.

# How it works...

Type Accelerators are another form of encapsulation of .NET code in PowerShell. Remember the first recipe in this chapter wherein we created a .NET object within PowerShell. We used the PowerShell command, `New-Object -TypeName System.IO.DirectoryInfo -ArgumentList '/home/ram'` to get information on a home directory: we created a new instance of `System.IO.DirectoryInfo`, and passed an argument to it. That was a lot of code to write. To accelerate the process, we could use, `[IO.DirectoryInfo]'/home/ram'`, (`System` is the default namespace; PowerShell would understand it without us explicitly mentioning it when calling accelerators) which outputs the same object as the former command.

With `Import-Csv` on the other hand, the process was a simple conversion of data from text into name-value pairs. This is similar to using `ConvertFrom-Text` with a `Delimiter` parameter. This way, we instruct PowerShell to convert each row of text into instances of the object: The first row in the row-column structure is taken as the property name, and the rest of the rows are data. The cells are separated using  delimiter, which was a comma, in case of the CSV file.

# There's more...

Look for more conversion cmdlets built into PowerShell. This can be done using the command, `Get-Command -Verb ConvertFrom`.

# See also

1.  More about Type Accelerators in the [Hey, Scripting Guy! Blog](https://blogs.technet.microsoft.com/heyscriptingguy/2013/07/08/use-powershell-to-find-powershell-type-accelerators/).
2.  Recipe: Using Here strings.
3.  The [different kinds of members](https://docs.microsoft.com/en-us/dotnet/api/system.management.automation.psmembertypes?view=pscore-6.0.0) in PowerShell.
4.  Best Practices Roundup: Formatting only in the end.

# Comparing the outputs of Bash and PowerShell

PowerShell and Bash are both shells, and are capable of interacting with the kernel. Just like how Bash can run on Windows, PowerShell can now run on Linux. While almost all of the aspects of which shell is better than the other is debatable, and the choice of shell is simply a matter of personal preference today, it is true that PowerShell is as powerful as .NET Core can get.

The primary difference between the two shells is, like we have seen before, that PowerShell outputs objects, while Bash returns text. Manipulation of the output in Bash involves manipulating text first, and then running further commands on the manipulated text to fetch the desirable output. PowerShell, on the other hand, handles content as objects and by design, requires comparatively less manipulation.

Structured data, as noted by Jeffrey Snover (the inventor of Windows PowerShell), is getting popular as days pass, and structured data is where PowerShell shines the most.

# Getting Ready

In this recipe, we are going to pick one example to show how simple and efficient it is to handle file metadata using PowerShell, primarily since the output is an object. We will list the files and folders within our home directory, along with the date and time of modification using both, `ls` in Bash and `Get-ChildItem` in PowerShell.

Open up two instances of the terminal if you would so like: launch `pwsh` on one.

# How to do it...

1.  At the Bash prompt, enter `ls -l` to list out all the files along with the metadata that the command shows by default.

![](Images/eaf2fd5f-b91c-43ce-8e94-a7f1d764df1e.png)

2.  Go to the terminal that has PowerShell running, and type in `Get-ChildItem` at the prompt.

![](Images/b2226dc9-7aae-4763-a1ec-249384383e49.png)

3.  Now, let us pick only the name of the folders and the last-modified date and time. This is done in Bash by passing the output of `ls -l` to `awk`.

```
ls -l | awk '{print $6, $7, $8, $9}'
```

![](Images/f56c057d-072d-4881-a844-5885d5270466.png)

4.  Next, let us pick the same information on PowerShell as well.

```
Get-ChildItem | select LastWriteTime, Name
```

![](Images/94508b98-e2da-4f79-b637-8753329401cf.png)

If you notice, the output is very similar in both the cases, however, with PowerShell, you see the names of the columns as well, which means that you don't have to look for further documentation. Also, the selection of columns is simpler in PowerShell; no text manipulation is required. On the other hand, in Bash, we use the `awk` command to manipulate the text output.

5.  Let's go one step further and create a sub-directory with a space in the name.

```
$ mkdir 'test subdirectory'
$ ls -l | awk '{print $6, $7, $8, $9}'
```

![](Images/60488ba8-6c4c-45d1-b5bf-145f2fc1134f.png)

Notice that what should have been `test subdirectory`, appears as `test`.

# How it works...

PowerShell reads content from the file system as objects, not as text. Therefore, you perform a selection of the desired columns (or as we shall later see, properties) directly. Bash, on the other hand, outputs text, columns from which are manipulated using a delimiter.

To demonstrate that this is the case, we created a new subdirectory with a space in its name, and we performed the column selection same as before, only in this case, we did not get the complete name of the new subdirectory, because the name contained a white space, which is a delimiter in `awk`.

Comparing Bash and PowerShell is like comparing apples and oranges—in more ways than one. However, understanding the differences helps us leverage each of the tools to our benefit.

# See also

1.  Recipe: Selecting objects via the pipeline.

# Comparing Windows PowerShell and PowerShell

PowerShell and Windows PowerShell are two different implementations. The former is based on a larger framework, the .NET Framework. The latter, on the other hand is a more modern framework, the .NET Core. PowerShell is cross-platform since its parent is. Windows PowerShell, on the other hand, is Windows-only, but has more capabilities than PowerShell, as of writing this chapter.

The PowerShell that this book talks about is the cross-platform PowerShell Core. This is referred to as *PowerShell*. The PowerShell that is Windows-specific is referred to as *Windows PowerShell*.

Windows PowerShell leverages the internal components and the architectural model of Windows with its capabilities enhanced by WinRM as well as Windows Management Instrumentation. In fact, most of the differences exist because of the inherent differences between Windows and Unix-like operating systems.

# Support for snap-ins

PowerShell will not support the legacy version of modules, called **Snap-ins**. Many of the snap-ins of old have been repackaged to be binary modules, and therefore, this should not be much of a concern, because future development of these should in theory work on either PowerShell, provided the system calls in the binaries can work on the system the binary is running on. For example, even if the Windows Active Directory module were repackaged into a binary PowerShell module, it would run on Windows PowerShell as well as PowerShell on Windows, but not on PowerShell on Linux because Windows Active Directory does not run on Linux.

# Convenience aliases

One important point to note is that commands like `ls` and `mkdir` are aliases in Windows PowerShell, which means, running `ls` on Windows PowerShell would run `Get-ChildItem` in the background (this is also true for PowerShell on Windows). In Linux, however, running `ls` from within PowerShell would run the actual `ls` command; `ls` is not an alias in PowerShell on Linux, it is the command itself, whose output would be plain text. You can validate this by running `ls | Get-Member` on PowerShell on Linux, and compare it with PowerShell on Windows as well as Windows PowerShell. (It is, therefore, good to stick to the best practice of not using aliases in scripts.)

![](Images/f38b4dcd-f484-4673-9559-92e752c14a42.png)PowerShell knows whether it is running on Linux, Windows or Mac OS by means of the values of the automatic variables, `IsLinux`, `IsWindows` and `IsMacOS`. On any system, only one of these variables has the value, `True`. When PowerShell sees that `IsLinux` is `True`, it would run Linux commands instead of the convenience aliases that were initially created to facilitate Linux administrators. For more information on these automatic variables, read the recipe, *Configure built-in variables*.

# PowerShell Workflows

Windows administrators who are used to PowerShell Workflows in Windows PowerShell need to note that they are absent in PowerShell. PowerShell Workflows were a little advanced, (to put it nicely), and were used in specific scenarios, where multiple cmdlets were to be run in parallel, or activities had to, say, survive a reboot. Workflows work on the Windows Workflow Foundation, which isn't cross-platform. Therefore, PowerShell Workflows will not run on PowerShell. Understand, though, that this is no loss at all.

# PowerShell Desired State Configuration

Desired State Configuration is work-in-progress as of writing this chapter. As of now, there are two codebases of DSC resources: LCM for Linux, which is managed by Microsoft's Unix team, and the other, DSC Resources for Windows PowerShell written by the PowerShell team. It would be some time before the DSC codebase becomes cross-platform.

# Listing out the aliases and using them in place of cmdlets

Aliases, as the meaning goes, are alternative names to cmdlets. They serve two purposes:

1.  Reduce the number of keystrokes
2.  Make the transition to PowerShell smoother

Traditionally, aliases were created in PowerShell so that Windows and Linux administrators did not find the new framework intimidating to work with. Regardless, aliases are best used only on the command line, and not in scripts, because some aliases are not aliases in Linux, and in general, aliases affect readability. (For instance, it would take conscious effort to realise that `gbp` stands for `Get-PSBreakPoint`.)

# How to do it...

Now that the best practice has been looked at, let us now look at listing out all the aliases in the system. Like already mentioned, it is simple to think in PowerShell. When we know that the verb to fetch any information is `Get`, and the noun in this case would be `Alias`, the cmdlet could be `Get-Alias`.

1.  Running a quick `Get-Command` on `Get-Alias` would tell us whether there indeed is such a cmdlet.

```
Get-Command Get-Alias
```

2.  Let us now run `Get-Help` to understand how to use the cmdlet.

```
Get-Help Get-Alias
```

If you're unsure about any command, or would like to reduce keystrokes without involving aliases, use tab-completion. Write a part of the cmdlet or parameter, and press the Tab key. PowerShell will complete the command for you, or show you suggestions, based on which platform you're doing this on.

3.  According to the help documentation, all the parameters for `Get-Alias` are optional (they are all enclosed in `[]`). Therefore, simply running `Get-Alias` would give us a list of all the aliases available in the current instance of PowerShell.

![](Images/1365c009-4f5b-4083-9ee8-257073c8a995.png)

4.  Let us now try to resolve the alias, `gbp` to the PowerShell cmdlet that it actually runs.

```
PS> Get-Alias gbp

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           gbp -> Get-PSBreakpoint
```

5.  Let us now look at how to do the opposite: get the alias for a certain cmdlet. If you read the help documentation for this cmdlet, you'd see a parameter called `Definition` in the second parameter set. This is the actual PowerShell cmdlet that runs when an alias is called.

```
PS /home/ram> Get-Alias -Definition Get-ChildItem

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           dir -> Get-ChildItem                                          
Alias           gci -> Get-ChildItem
```

6.  We can see two aliases as output, both of which run `Get-ChildItem` under the hood. Let us now run `dir` as well as `Get-ChildItem` and compare their outputs.

```
PS /home/ram> dir

    Directory: /home/ram

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       06/04/2018     13:05                Desktop
d-----       18/05/2018     16:01                Documents
d-----       18/05/2018     16:01                Downloads
d-----       06/04/2018     13:05                Music
d-----       20/05/2018     02:17                Pictures
d-----       06/04/2018     13:05                Public
d-----       06/04/2018     13:05                Templates
d-----       10/04/2018     03:41                Videos
PS /home/ram> Get-ChildItem

    Directory: /home/ram

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       06/04/2018     13:05                Desktop
d-----       18/05/2018     16:01                Documents
d-----       18/05/2018     16:01                Downloads
d-----       06/04/2018     13:05                Music
d-----       20/05/2018     02:20                Pictures
d-----       06/04/2018     13:05                Public
d-----       06/04/2018     13:05                Templates
d-----       10/04/2018     03:41                Videos
```

7.  The two outputs are identical. Let us now look at what type of object the commands return.

```
PS /home/ram> dir | Get-Member

   TypeName: System.IO.DirectoryInfo

Name                      MemberType     Definition
----                      ----------     ----------
LinkType                  CodeProperty   System.String LinkType{get=GetLinkType;}
Mode                      CodeProperty   System.String Mode{get=Mode;}
...
PS /home/ram> Get-ChildItem | Get-Member

   TypeName: System.IO.DirectoryInfo

Name                      MemberType     Definition
----                      ----------     ----------
LinkType                  CodeProperty   System.String LinkType{get=GetLinkType;}
Mode                      CodeProperty   System.String Mode{get=Mode;}
...
```

They returned the same object as well.

# How it works...

Aliases are nothing but mappings done within PowerShell. The short words are mapped to PowerShell cmdlets, identified by the `Definition` property in each of the aliases. Therefore, you can use the aliases to in place of full cmdlets. Aliases also support the same parameters as the cmdlet as well, since aliases are merely pointers to the right cmdlet.

# See also

1.  Best Practices Roundup

# Creating a Custom Alias

Aliases, as we saw in the previous recipe, are simply pointers to actual PowerShell cmdlets, and therefore, creating custom alias simply involves identifying a word for the alias you'd like to create, and map it to the PowerShell cmdlet that you'd like to call.

# How to do it...

1.  First, identify a word that you'd like to use as the alias. For example, let us consider `listdir`.
2.  Run listdir on PowerShell to ensure such a cmdlet (or a Linux command) does not already exist.
3.  List out the cmdlets that deal with aliases, by running:

```
Get-Command -Noun Alias
```

Remember that the nouns in PowerShell are singular. Therefore, there would be no first-party cmdlet that contains `Aliases`. If third party modules give you `Aliases` as a noun in them, they are not following the PowerShell best practice of using only singular nouns.

4.  `New-Alias` is the cmdlet we are looking for, since it creates a new alias. (`Set-Alias` is used to modify an alias that already exists.)
5.  Read the help documentation for `New-Alias` by running:

```
Get-Help New-Alias
```

The help document indicates that only the Name and the Value parameters are mandatory. We shall use only the two to create this simple alias.

6.  Run the following to create the custom alias:

```
New-Alias listdir Get-ChildItem
```

7.  See whether the alias was created as desired or not.

```
PS> Get-Alias listdir

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           listdir -> Get-ChildItem
```

8.  Also, run the alias to see what output it gives.

```
PS /home/ram> listdir

    Directory: /home/ram

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----          4/20/18   6:36 AM                Desktop
d-----          5/10/18   1:05 PM                Documents
d-----          5/16/18  11:03 AM                Downloads
d-----          4/20/18   6:36 AM                Music
d-----           5/1/18   2:19 PM                Pictures
d-----          4/20/18   6:36 AM                Public
d-----          4/20/18   6:36 AM                Templates
d-----          4/20/18   6:36 AM                Videos
```

That is the output that we are familiar with–the output of `Get-ChildItem`.

Aliases are ephemeral by default. They exist only as long as your PowerShell session exists. To use custom aliases without having to recreate them each time, export these aliases (the instructions for which are in the next recipe) and import them using your PowerShell profile. We will understand profiles in a later chapter.

# How it works...

Aliases, as already mentioned, are pointers to cmdlets. Using `New-Alias`, you create a pointer with a custom name, that points to the desired PowerShell cmdlet. This is simply a Name–Value pair.

When you run anything on PowerShell, PowerShell checks its list of cmdlets and aliases (among other definitions) to understand what you are asking for. When PowerShell encounters an alias, it looks for which cmdlet it points to, and runs the cmdlet.

# There's more...

You can add more content to your aliases, such as descriptions. Refer the help documentation for `Get-Alias` to see what more you can do with aliases.

# See also

1.  Recipe 3.8: Understanding cmdlets and parameters
2.  Recipe 2.8: Importing/Exporting custom aliases for future use
3.  Recipe 3.4: Enabling automated execution of commands for each load

# Export/Import Custom Aliases for Future Use

Aliases being ephemeral, in spite of its advantages and the intended use of aliases, could be seen as an inconvenience. In order that aliases can be reused, they need to be exported to a file and later, imported when needed. This recipe will show you how to export and import the aliases you may have created.

# Getting Ready

You need custom aliases already created for this process to be effective. If you don't have custom aliases created, the export action would only export the default aliases, which would be loaded with PowerShell anyway.

Go to the previous recipe to create at least one custom alias.

# How to do it...

1.  Ensure that your custom alias exists and runs properly. One way of doing this is to get details about the alias you created.

```
Get-Alias listdir
```

2.  Export all of the aliases loaded on your session to a file.

```
Export-Alias aliases.csv
```

CSV is the default file type. The import that we would see in the coming steps understands CSV and make the necessary associations.

3.  It is also possible to export the aliases as a script. This way, PowerShell will create a script that would contain the New-Alias cmdlet for each of the aliases in the export.

```
Export-Alias aliases.ps1 -As Script
```

4.  Look at the contents of each of the files created; the CSV file first, and then the script.

```
Get-Content ./aliases.csv
```

![](Images/56717d30-2937-4bac-89c4-634503efc8e8.png)

```
Get-Content ./aliases.ps1
```

![](Images/bdf72b32-a228-470f-ac21-ad35d4e8013a.png)

5.  Optionally, edit the file to remove all the aliases except the ones you created. The custom aliases can be found at the bottom of the list.

This concludes exporting aliases.

Let us now import aliases into our PowerShell session.

1.  Restart PowerShell.
2.  See if the alias, `listdir`, that you created exists.

```
Get-Alias listdir
```

3.  Now, import the aliases.

```
Import-Alias ./aliases.csv
```

You may receive several errors, each saying that the new alias could not be created since the alias already existed. There are two ways to handle this: the first is to remove the default aliases from the export file (which is recommended), and the second is to use the `-Force` parameter (this may still result in errors, but they would be significantly fewer).

If you exported the aliases as a script, simply call the script.

```
./aliases.ps1
```

# How it works...

The script way is straight-forward: the cmdlets are run one after the other and the aliases are created in the system just like how you created them manually.

With the CSV import, PowerShell parses the input into the Name–Value pairs (and add other parameters based on what you exported) and add them to its alias reference for the current process.

# See also

1.  Recipe 3.4: Enabling automated execution of commands for each load

# Listing out the execution policies and setting a suitable one

There was a time when running scripts on Windows computers was a piece of cake. Windows computers were highly prone to remote script executions. With PowerShell, Microsoft added a safety belt that allowed the user some control over how PowerShell scripts were loaded. Some specific models of script executions got restricted, which plugged some holes in the system.

It is important to remember that execution policies are **not** a security feature. There are ways to circumvent this fence and still run scripts. Execution policies are in place to ensure users don't accidentally run scripts without awareness.

PowerShell on Windows and Windows PowerShell contain the configuration. Running PowerShell scripts on Windows is still restricted by default. On PowerShell on Linux, this doesn't work at the moment, and based on the interactions in the community, it is uncertain whether this feature would make it to PowerShell on Linux.

An execution policy determines what type of execution of scripts is allowed. Here are the six execution policies (excluding Default):

1.  AllSigned
2.  RemoteSigned
3.  Restricted
4.  Unrestricted
5.  Bypass
6.  Undefined

There are three scopes as well:

1.  Process
2.  CurrentUser
3.  LocalMachine

A combination of an execution policy and a scope are what determine the condition which scripts can be loaded under. Microsoft has documented in detail what each of the policies is. In general, AllSigned requires that all the scripts that run on the computer are signed using a code signing certificate by a trusted certification authority. If this policy is set, PowerShell will not run unsigned scripts even if you were the one to create them.

**Restricted** is the default policy: Commands can be run, but not scripts. **RemoteSigned** allows scripts created on your own computer to run. Scripts that are downloaded from the Internet cannot be run.

**Bypass** is similar to unrestricted, however, is used in specific scenarios such as when PowerShell forms the basis of a certain application, and the application has its own security implementation.

**Unrestricted** means that all scripts and commands can run after a simple confirmation. **Undefined** means that no policy has been defined for a particular scope. Let us try to understand the concepts using the following recipe.

# Getting Ready

This recipe needs Windows to work. If you're running a pure Linux environment, you cannot work with this recipe. You may run the commands, but you would see the Unrestricted policy set at all levels.

If you can get your hands on a Windows computer, you can proceed with this recipe regardless of whether it has PowerShell or Windows PowerShell.

# How to do it...

Open a PowerShell window  by running `pwsh` or `powershell`. The `pwsh` command calls PowerShell, and `powershell` calls Windows PowerShell.

Windows PowerShell comes preinstalled on all modern Windows products; PowerShell, on the other hand, has to be installed. Note that all of the current PowerShell cmdlets will run as well on Windows PowerShell.

1.  First, run the Get-Command cmdlet to know how to work with execution policies.

```
Get-Command -Noun Execution*
```

![](Images/ad67d754-eabc-404d-bf92-3014549f8ff6.png)

2.  Let us now get help on running the cmdlet.

```
Get-Help Get-ExecutionPolicy
```

3.  We want to know the execution policy set on the machine, therefore, we would run:

```
PS> Get-ExecutionPolicy
```

![](Images/69fa2f0d-8c11-4129-9c73-e4967f4357b5.png)

This shows the execution policy currently effective on the current PowerShell session.

4.  To list out the policies set at various scopes, run the following command:

```
PS> Get-ExecutionPolicy -List
```

![](Images/5db273a2-fe7e-4915-b9ad-c590063310a7.png)

We see that the policy is only set at the LocalMachine level, and it is set at RemoteSigned, which is the same as that reflected in the previous step. The policy at the LocalUser and the Process scopes is Undefined, which made the session pick the execution policy from LocalMachine.

Let us now set the execution policy for the local machine to be Undefined and see what our session picks up.

5.  For this to work, close the current PowerShell session and open a new session as the administrator.
6.  Next, run the command:

```
PS> Get-Help Set-ExecutionPolicy
```

![](Images/e039790c-5185-4b1d-96be-38b1391f12e3.png)

7.  The help document shows that the value of the ExecutionPolicy parameter is mandatory, and that Undefined is one of the valid values it would accept. We want to set the policy at the LocalMachine scope, therefore,

```
PS> Set-ExecutionPolicy Undefined -Scope LocalMachine
```

8.  Now, list out the execution policies at the various scopes:

```
PS> Get-ExecutionPolicy -List
```

![](Images/7a2cad04-6a65-480e-9d9f-14d60b2a8e9b.png)

9.  Now, let us check the currently-effective execution policy:

```
PS> Get-ExecutionPolicy
```

![](Images/91d88fe3-665a-4ea8-b9c7-1e3ab057e777.png)

10.  Let us now set the execution policy back to how it was before we began the recipe. You may want to change the policy to suit your needs, based on what authority you have on the computer.

```
PS> Set-ExecutionPolicy RemoteSigned -Scope LocalMachine
```

# How it works...

Execution policies are nothing but conditions set on the system to avoid accidental script runs. They work at different scopes.

There are three scopes in PowerShell, as noted already. The **LocalSystem** scope is at the end of the chain. Right above it is the **CurrentUser** scope. At the top, is the **Process** scope. The level of precedence is Process > CurrentUser > LocalMachine. Therefore, if any policy other than Undefined is set at the Process scope, the session would use the policy set on the process. In case it's Undefined, it would look for the policy set on the CurrrentUser scope. If CurrentUser has the policy marked as Undefined as well, the session would apply the policy applied at the LocalMachine level. If LocalMachine has Undefined set, the session would pick the Default policy, which is based on what PowerShell has defined as the policy, which may vary based on the version of operating system. On Windows 2016, for instance, the default policy is RemoteSigned.

The policies set at the CurrentUser and LocalMachine levels are stored in the Windows Registry. The policy set on the Process scope is stored in the ephemeral environment variable, `$env:PSExecutionPolicyPreference`.

# See also

1.  [About_Execution_Policies](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-6) (Microsoft)

# Preparing for Administration using PowerShell

 In this chapter, we cover the following topics:

1.  Installing Visual Studio Code
2.  Configuring automatic variables
3.  Changing the shell behaviour using a variable
4.  Enabling automated execution of commands for each load
5.  Customising the terminal prompt
6.  Understanding standard redirection in PowerShell
7.  Calling native Linux commands from PowerShell
8.  Understanding cmdlets and parameters
9.  Running cmdlets with minimal keystrokes
10.  Finding parameter aliases
11.  Calling a PowerShell script
12.  Dot-sourcing a PowerShell script
13.  Calling a PowerShell cmdlet from outside of PowerShell
14.  Recording the cmdlets run on the PowerShell console

# Introduction

It is common notion that the more you use the terminal (as opposed to the GUI), the more efficient you are. Typing out commands is much easier and faster than clicking around the screen. However, to someone who has just begun using the terminal, it may not be so. Over time, as administrators grow more and more comfortable with the terminal, they learn to configure it for speed and efficiency, much like a trained horse. Further, most efficient administrators like automating several parts of their workflow—customising `.bashrc` and Vim scripts  are examples of it. In this chapter, we will familiarise ourselves with the different consoles and tools that work with PowerShell, and will also look at a few simple recipes which would help customise our workspace, so that we can be more efficient.

# Installing Visual Studio Code

Scripting can happen on the console itself, with Vim. It is also possible to use other editors like Gedit or even Atom to write PowerShell scripts. It is, however, recommended to use Microsoft's open source code editor, called, Visual Studio Code (or `vscode`). In this recipe, we would look at installing Visual Studio Code, and configuring it to work with PowerShell.

# Getting Ready

We would look at the steps to install `vscode` on Ubuntu. Today, most repositories contain Visual Studio Code. You may check in the software store of your distribution to install `vscode`. If not, the easiest way to install `vscode` is to download the `.deb` (or the `.rpm` package based on your distro), and run it to install the package on your computer.

# How to do it...

Installing Visual Studio Code is simple.

1.  If your Linux distribution has a software store, search the store for Visual Studio Code.
2.  If you find Visual Studio Code, install the package from there. If not, proceed with the next step.
3.  The package name for Visual Studio Code is `code`. Use your package manager to search for the package in the repository. On Ubuntu, the command would be:

```
$ sudo apt-cache pkgnames code
```

4.  If you're able to find the package in your repository, install vscode like you would any other package.

```
$ sudo apt install code
```

5.  If you were unable to find the package, go to [https://code.visualstudio.com/Download](https://code.visualstudio.com/Download) and download the right `code` package for your distro.
6.  To install VS Code, call your package manager with the path to the downloaded package.

```
$ sudo apt install install code_version_arch.deb
```

7.  If you would rather install VS Code in portable mode, download the VS Code tarball and extract its contents to a convenient location to run VS Code. Although, remember that updates to VS Code would be handled by VS Code itself, in this case.

Visual Studio Code is a powerful code editor in itself. However, it may not fully support PowerShell right out of the box. You would need to install the extension that packs capabilities which help run write and run PowerShell scripts.

1.  Launch Visual Studio Code.
2.  Click on the Extensions icon or press `Ctrl+Shift+X` to go to the Extensions pane.
3.  In the search bar, enter `powershell publisher:Microsoft` and hit Enter to search for the PowerShell package.
4.  Click on Install in the resulting package–the PowerShell package should be on top.
5.  Once the installation completes, click on Reload to reload Visual Studio Code with PowerShell capabilities.

You are now ready to develop PowerShell scripts using a friendly editor that supports almost all of the capabilities that Windows PowerShell Integrated Scripting Environment has, and more!

# How it works...

Windows PowerShell ISE was the de-facto environment to develop PowerShell scripts and even applications written in PowerShell. Then came Adam Driscoll's PowerShell extension to Microsoft Visual Studio which integrated PowerShell into the integrated development environment.

While PowerShell was being worked on, and the .NET Foundation was formed, Microsoft started working on a lightweight code editor called Visual Studio Code that packed many of the great features of Visual Studio, without all the load of the language libraries. This was enough to build PowerShell scripts; most PowerShell *script-writers* use mainly the IntelliSense features, and Visual Studio Code has them.

Using a package manager to install VS Code ensures that all the dependencies are met. Also, this method of installation ensures that the signing key is added to the system. This way, updates to VS Code can be installed through the system, such as by running `sudo apt upgrade`.

# See also

1.  [Installing Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux) (Microsoft documentation)

# Configuring automatic variables

Perhaps nothing contributes to efficiency like configurability. Configuring a system is a way of moulding it to your taste. You are the only one who knows best what works for you. Therefore, the more configurable a system is, the better it can be moulded to your use. automatic variables in PowerShell are one of the first steps to customisation in PowerShell (profiles are the other; we shall look into them shortly). In this recipe, we will list out all the automatic variables, and configure some of them to our requirements.

# Getting Ready

Read the *Listing the various providers in PowerShell* section of *Installation, Reference and Help*, to learn how to use the various providers in PowerShell.

# How to do it...

Let us first list out the variables we have. This can be done in two ways:

*   Using a cmdlet
*   Using a provider

Let us first look at using the cmdlet to list out the variables built into PowerShell.

1.  Open a terminal window. If you have one open, restart PowerShell.
2.  Find the cmdlet that works with variables.

```
PS> Get-Command -Noun Variable
```

Remember that the noun in a cmdlet is always singular. Therefore, it would be `Variable`, and not `Variables`.

3.  There are five cmdlets that deal with variables. We want to fetch a list of all variables already existing in a new session of PowerShell. Let us pick `Get-Variable`, and fetch help information for it.

```
PS> Get-Help Get-Variable
```

4.  This is the cmdlet that we need to list out all the variables predefined in the current scope.

```
PS> Get-Variable
```

That should list out all the variables predefined in the current scope.

Any variables you define would be listed here. Hence, it is important that you start a fresh session of PowerShell to see what variables have been predefined.

Let us now use a PowerShell provider to list out the variables defined in the current scope.

1.  List out the PowerShell providers. We looked at providers in the previous chapter.

```
PS> Get-PsProvider
```

2.  Change location to the `Variable:` drive of the `Variable` provider. This is done using `Set-Location`.

```
PS> Set-Location Variable:
```

3.  Now, let us list out all the available child items of the `Variable:` drive.

```
PS> Get-ChildItem .
```

The output of this was identical to that of `Get-Variable`, called without an argument.

# How it works...

PowerShell is built with some variables that control its behaviour, and administrators are allowed to modify some of them to suit the needs. Some variables, however, cannot be modified; they are contextual, and add some amount of flexibility (or modularity, as the case might be) to the shell.

One such example would be `$PWD`, which contains the path of the present directory. This variable changes itself based on the execution of `Set-Location`. Values cannot be explicitly assigned to such variables; setting values explicitly would have no effect on the behaviour of the shell.

Some variables, on the other hand, accept values, and let us control the execution of commands and scripts. We shall look at an example in the next recipe.

# Changing the shell behaviour using a variable

In the previous recipe, we took a look at the existing variables. In this recipe, we will change the value of one of the variables to control the behaviour of PowerShell. Again, remember that the change in the value is ephemeral; the values would be reset once the PowerShell process is restarted.

# Getting Ready

Read the previous recipe to understand what automatic variables that come predefined. Also, start Visual Studio Code. Follow the steps below to start VS Code.

1.  Open Applications (I'm using the Gnome DE, which shows all applications with `Super + A`).
2.  Type in `code`.
3.  Press `` Ctrl + ` `` to launch the terminal.
4.  Click on New File at the welcome screen. (Or press `Ctrl + N`.)
5.  At the bottom right of the VS Code window, you would see the file type set to Plain Text. Click on it; you would be taken to the command bar on top.
6.  Type in `powershell` at the command bar. The PowerShell Integrated Console will open at the bottom.

![](Images/4695ded0-1291-4688-85fc-14410d9643aa.png)

We are all set for the recipe now.

# How to do it...

1.  Let us run a command that would result in an error. For now, let us not focus on the syntax of the command; our only goal for now is to generate an error. At the first line of the script window, type in:

```
Get-ChildItem /home/ram/random-directory
Write-Host "Hello world!"
```

![](Images/b0b222fa-1b67-42e4-a78e-d22e94f2bc8a.png)

2.  Run the two-liner script using the `F5` key.

![](Images/104cf932-9a53-42b2-8bed-87e13ae01667.png)

PowerShell is prompt to show an error. It also displays the `Hello world!` string.

3.  Now, let us set the error action preference, using the variable, `ErrorActionPreference`. We know there's such a variable from the previous recipe. First, though, restart PowerShell. The easiest way is to click on the little bin icon at the top of the Integrated Console window. When VS Code asks if you would like to restart the session, click on Yes.

![](Images/b9254d0b-3222-4b7d-879b-2d8b4063252b.png)

4.  Now, set the `ErrorActionPreference` variable. At the PowerShell Integrated Console, enter:

```
PS> Set-Variable ErrorActionPreference SilentlyContinue
```

5.  Run the two-liner script again.

There is no error this time. And we see `Hello world!` at the console.

If you do not want the entire script appear at the prompt, make the first line of the script, `Clear-Host`; this would clear the screen before showing the output.

6.  What if you were to check whether an error was generated at all? We check the value of the automatic variable, `Error`.

```
PS> Get-Variable Error
```

![](Images/48e32e87-abde-4edd-9ca0-6cf1a296a5aa.png)

7.  The `Value` column contains some text. Let's select and expand the contents of `Value`.

```
Get-Variable Error | Select-Object -ExpandProperty Value
```

![](Images/735a62cc-1e23-4373-8710-1f1c53943594.png)

The output text is the same as what we received before we set the error action preference.

You can also simply call the `Error` variable to read all the errors that occurred in the current session.

# How it works...

By default, the error action preference is `Continue`, which means that PowerShell would display the error, and continue with the execution of the rest of the script (this effect is not noticeable when running individual commands, hence the creation of the two-liner, or three-liner in case you added `Clear-Host` at the top). By setting `ErrorActionPreference` to `SilentlyContinue`, we instruct PowerShell to record the error but not show it on the screen, and at the same time, go on with executing the rest of the script.

# See also

1.  [about_Preference_Variables, $ErrorActionPreference](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_preference_variables?view=powershell-6#erroractionpreference) (Microsoft documentation)
2.  Recipe: Error handling in PowerShell

# Enabling automated execution of commands for each load

Like we saw in the previous recipes, these changes are ephemeral; they remain as long as the session is active. There might be situations wherein administrators might require running a few commands, or loading modules to enable them to work faster. For instance, I tend to load a series of modules that help me manage Microsoft Exchange, Active Directory, VMware vSphere infrastructure, Citrix XenApp, Microsoft System Center, and other environments using PowerShell.

If you see, all of these products require different ways of loading the modules, snap-ins and scripts, and many of them require certain configuration every time you load the modules (such as connecting to VM servers with administrator credentials). These can be done using the PowerShell profile.

# Getting Ready

PowerShell by default does not create a profile during installation. It simply runs with its default configuration. Any override to this configuration would require creating and modifying the profile.

1.  Open a PowerShell console. (You could either run pwsh at the terminal or use the VS Code console. This recipe uses the terminal.)
2.  Reveal the path of your profile. To do this, simply call the automatic variable.

```
PS> $PROFILE
```

3.  Check if your profile exists.

```
PS> Test-Path $PROFILE
```

4.  If you get True as the response, you can proceed with the recipe. If the response is False, which is most likely the case, run the following:

```
PS> New-Item $PROFILE -ItemType File
```

5.  You may receive an error, saying a part of the path was not found. This is because your `~/.config/` directory does not by default contain a `powershell` directory. Adding `-Force` to the command creates this directory and creates your profile file at the location.

```
PS> New-Item $PROFILE -ItemType File -Force
```

![](Images/c6790c84-4047-427b-933e-47b24beaf1d1.png)

6.  We will now edit the profile in VS Code. At the terminal, type:

```
PS> code $PROFILE
```

# How to do it...

You should have the profile open now. It would currently be empty. Let us now customise PowerShell's error action behaviour. Remember that we said that setting `ErrorActionPreference` to `SilentlyContinue` at the terminal was temporary. Let us now ensure that `ErrorActionPreference` is permanently set to `SilentlyContinue` every time we launch PowerShell.

1.  Switch to the terminal window. If you have the window open since the last recipe, restart PowerShell.
2.  Let us see what the error action preference is at the moment.

```
PS> Get-Variable ErrorActionPreference
Continue
```

3.  Switch to VS Code. The profile should already be open for edits.
4.  At the very first line, type in:

```
PS> Set-Variable ErrorAction SilentlyContinue
```

5.  Save the profile and close the file.
6.  At the terminal, type `exit` to exit from PowerShell. Start PowerShell again.
7.  Let us now check what the value is for `ErrorActionPreference`. At the prompt, type:

```
PS> $ErrorActionPreference
SilentlyContinue
```

8.  To ensure the preference is indeed in place, type:

```
PS> Get-ChildItem /home/ram/random-directory
```

![](Images/bf5a2583-205d-4e2a-b756-4611f2977719.png)

The cursor simply returned to the prompt at the next line without throwing an error.

# How it works...

Long story short, the PowerShell profile executes every time a PowerShell session is loaded. This profile is a PowerShell script file that can contain a series of commands and functions, which would be executed just like another script.

One important point to remember is that there is a different profile for each host. For instance, there is a separate profile for PowerShell loaded on the Terminal, and a different one for the Integrated Terminal on VS Code. This is because each of the terminals has a different nature.

Execution Policies have not been implemented in PowerShell on Linux. In case PowerShell on Linux gains the safety belt in the future, the execution policy should be set to allow execution of scripts in order for the profile to load.

# There's more...

It is bad practice to set a global action preference. Empty the profile to remove the error action preference. Since the profile has nothing else, you could even delete the profile using the following command:

```
 Remove-Item $PROFILE
```

Read the best practices for more information.

# Customising the terminal prompt

In the previous recipe, we customised the error action preference using the profile. We used an already-demonstrated command to show that commands that can be run on the PowerShell console can be added to the profile as well, and this was a way to automate running a certain set of commands which could be used to increase productivity.

Now, we will take the next step and customise our console prompt. The options are theoretically endless; this recipe is just another demonstration of how flexible PowerShell is.

# Getting Ready

You need VS Code for this recipe. If you did not follow along the last recipe, follow the steps in the *Getting Ready* section of the last recipe to create a PowerShell profile, only this time, run the commands at the PowerShell Integrated Console of VS Code.

# How to do it...

Ensure that the profile is empty. If you just created the profile, you can simply proceed further. If not, clear all contents in the profile. If the error action preference is set in the profile, it would become hard to troubleshoot scripts that you create in the future.

1.  Enter the following in the main window.

```
function prompt {
  $Location = (Get-Location).Path.ToString()
  switch -Wildcard ($Location) {
    "/home/$env:USERNAME" { $Location = '~'; break }
    "/home/$env:USERNAME/Documents" { $Location = 'Documents'; break }
    "/home/$env:USERNAME/Downloads" { $Location = 'Downloads'; break }
    "/home/$env:USERNAME/Pictures" { $Location = 'Pictures'; break }
    "/home/$env:USERNAME/Videos" { $Location = 'Videos'; break }
    "/home/$env:USERNAME/Music" { $Location = 'Music'; break }
    "/home/$env:USERNAME/Documents/code" { $Location = 'Code'; break }
    "/home/$env:USERNAME/*" { $Location = $Location.Replace("/home/$env:USERNAME/", '~/'); break }
    Default { }
  }
  Write-Host "PS " -NoNewline
  Write-Host `
    ($($env:USERNAME) + "@" + "$([System.Net.Dns]::GetHostByName((hostname)).HostName) ") `
    -NoNewLine -ForegroundColor Cyan
  Write-Host "$Location" -NoNewline -ForegroundColor Green
  Write-Host ("`n> ") -NoNewline
  return " "
}
```

2.  Save the profile script file.
3.  Click on the little bin icon at the top of the Integrated Console to kill the current PowerShell session.
4.  When VS Code prompts you whether you would like to restart the session, click Yes.

Your prompt should look as shown in the image below.

![](Images/f6f8c8ed-8df5-4d42-8415-d37b24ac6e27.png)

# How it works...

The prompt is controlled by a function called `prompt`. To demonstrate this, we could use:

```
Get-Command prompt
```

The output shows that there is indeed such a command, which is of the type `Function`. To know the contents of the `prompt` function, enter:

```
PS> (Get-Command prompt).ScriptBlock
```

The output shows you the entire function you just wrote. This is, however, the function that overrode the default `prompt` function. If you clear your profile, restart the PowerShell session, and type in the command above, you would see a simple three-liner output, which is the default `prompt` function.

Now to break down the function we wrote:

First, you declare the function you are about to write. This is done using the keyword, `function`, followed by the name of the function. Since we want to work with the prompt, we use the existing function name so as to override the default functionality. The next thing that follows is the script block, which starts with a `{`.

We want the location to appear at the prompt. This is a must-have information, for obvious reasons.

If you notice, PowerShell shows the complete Home path at the prompt. While this works, we are used to the tilde for Home. Also, I know that Documents, Music and other folders reside within my Home folder, and I would rather have just the name of the folder appear at the prompt. This would mean some text manipulation. Therefore, I assign the current location to a variable, `$Location`.

Next, we perform a switch-case operation and arrive at the value for what needs to be displayed at the prompt. Don't worry about the syntaxes for now; we will look into each of those in the chapters that follow.

Later, we use a few `Write-Host` statements to construct the prompt text. The `-NoNewLine` parameter ensures that the contents of each statement do not go to the next line. When we need a line break, we explicitly add `` `n ``.

If you want to break a long-running line in a script, use the backtick (`` ` ``) character at the point where you would like to break the line and press Enter to break the line after the backtick. PowerShell would treat the line with the backtick, as well as the line that follows, as the same line. Similarly, if you would like to write two statements in the same line, use the semicolon (`;`) at the end of the first statement, and continue with the second after a space. PowerShell will treat both the clauses as separate statements, just like plain English.

Since `Write-Host` just sends text to the host, and does not return anything, we add a return statement to the function, with merely an empty space.

When we reload the PowerShell Integrated Console, the profile is loaded, and this time, the custom `prompt` function in the profile overrides the default `prompt` function, and presents us with a nice prompt, formatted just the way we defined.

# There's more...

Play around with the sequences and the contents of the `Write-Host` statements for now to customise your prompt. Once we are comfortable with the syntaxes in PowerShell, we should be able to customise the profile further.

# See also

1.  [about_Prompts](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_prompts?view=powershell-6) (Microsoft Documentation)

# Understanding standard redirection in PowerShell

When I first started using the command line interface, I was daunted by `<` and `>` and `>>` at first. Then, I entirely stopped using the command line interface for a while and went back to the Windows administrator ways, albeit with an unusual-for-a-Windows-admin level of use of keyboard shortcuts (it's all about the speed and efficiency!).

When PowerShell came along, I had forgotten about those operators; I simply went ahead and understood the concept of object and pipelines, and worked for years that way. Switching to Linux at home made me want to know the "Linux way" of using the terminal. The operators came back to haunt me. I simply installed PowerShell on Linux.

Redirection in PowerShell mainly relies on streams. And streams are covered in a different chapter. For now, we stick with the default stream, which is, `Success`.

This recipe covers the different, simple redirections to help with basic administration. We shall come back to streams while understanding the concepts of error handling.

Before we begin, let us understand that PowerShell is very different from Bash in terms of redirection, although it packs some minor similarities; similarities enough to make you not go away, but rather appreciate the flexibility of the object model, and the uniformity of use.

# How to do it...

We shall perform four activities in this recipe:

1.  Redirect output to a file
2.  Append another output to the same file
3.  Send the output of a command to the console as well as a file
4.  Accept the input of one command into another

Apart from the operators that we use in the first two activities, we will also look at the cmdlet equivalents to those operators.

1.  List out all the processes running on your computer at the moment.

```
PS> Get-Process
```

2.  The output was shown on the console. Now, let us redirect the contents into a file.

```
PS> Get-Process > processes.txt
```

3.  List out the contents of the file.

```
PS> Get-Content ./processes.txt
```

4.  Let us now append the file with the date and time stamp.

```
PS> Get-Date >> ./processes.txt
```

5.  Read the contents of the file now.

```
PS> Get-Content ./processes.txt
```

You can see that the file now contains a list of all the processes running in the system, as well as the time stamp. The time stamp got *appended* to the file.

When going the *PowerShell way*, the same results can be accomplished using the `Out-File` cmdlet. (`Out-File` has more features such as setting the encoding and new line control.) Let us accomplish the same tasks using the `Out-File` cmdlet. You may want to delete `processes.txt` before proceeding.

1.  Let us list out the currently-running processes again, and send the output to a file using `Out-File`.

```
PS> Get-Process | Out-File processes.txt
```

2.  Now, let us append the time stamp to the file.

```
PS> Get-Date | Out-File processes.txt -Append
```

If you notice, the output of `Get-Process` and `Get-Date` went directly to the file; nothing got displayed on the host.

If we want to display the output on the console as well as send the content to a file, we simply use `Tee-Object` instead of `Out-File`. If you would like, delete the file, `processes.txt` again.

1.  Run the following command.

```
PS> Get-Process | Tee-Object ./processes.txt
```

The list of running processes should be shown at the terminal.

2.  Check the contents of the file, `processes.txt`.

```
PS /home/ram> Get-Content ./processes.txt
```

As you can see, the list of processes appears in the text file as well.

Let us now proceed with learning to make cmdlets accept input from files. Linux administrators are used to making commands accept input from a file, like so:

```
$ command < input_file.txt
```

The command accepts input from `input_file.txt`, and performs operations on the input content.

In PowerShell, this is handled using `Get-Content` and the pipe (`|`). The PowerShell equivalent of a command accepting input from a file would be:

```
PS> Get-Content input_file.txt | command
```

This might seem the other way around to most of those who are not used to PowerShell. Let us break down the process into pieces and try to understand it better. For instance, let us say you have a list of files in a text file called `input.txt`.

1.  Reveal the contents of the text file.

```
PS> Get-Content input.txt
```

![](Images/cfa87d64-fffb-4078-a37e-18d89fb00bae.png)

2.  List out the contents of the current directory.

```
$ ls
```

We have five test files in the current directory, four of which are in the list (the input file). Let us say that you would like to delete the files listed in the input file, from the directory.

3.  Pass the output of `Get-Content` to the command, `Remove-Item`, through the pipe.

```
PS> Get-Content input.txt | Remove-Item
```

![](Images/f5ac1741-e892-4737-9bc2-842204050c21.png)

4.  List out the files currently present in the directory.

```
PS> Get-ChildItem .
```

Et voilà! If you compare the outputs of `ls` (before) and  `Get-ChildItem` (after); the files that were listed in the text file are no more.

# How it works...

In this recipe, we set out to understand the similarities between Bash and PowerShell. In spite of being fundamentally different from Bash, PowerShell does pack some similarities to Bash. Two of the similarities, as we saw, are passing content to files and appending content to the files.

We looked at three cmdlets in this recipe, one of which were used twice.

# Out-File

Those comfortable with Bash use the `>` for sending the output to a file, and `>>` to append the output to an existing file. in PowerShell, we use the `Out-File` cmdlet. We run a command that sends output to the standard out, and through the pipe, redirect the output to `Out-File`, which handles writing the output to a file. Usually, `Out-File` is used to send content to a text file.

When there is a need to append the content to a file, we use the `-Append` switch with `Out-File`. This way, if the file that is being written to already contains content, the content isn't overwritten (overwriting content is the default behaviour of `Out-File`).

# Tee-Object

There are situations wherein you need to send content to a file, as well as display the content on the console. This is handled using a simple call of `Tee-Object`. `Tee-Object` works like the letter T; apart from sending content to a file or a variable, it also sends the content down the pipeline. In case `Tee-Object` is the last cmdlet in the statement, the pipeline output is sent out to standard out, which in most cases is the host (or in other words, the console by default).

In our recipe, we sent the first output to the file, `processes.txt`, and the second output was not sent down the pipeline. Therefore, `Tee-Object` picked the standard out.

# Accepting input from file

This process is significantly different in PowerShell, compared to Bash. In Bash, we call the command first, and then ask it to accept input from a file. In PowerShell, we make PowerShell read the contents of the input file first, and then send the output to the command that accepts input through the pipeline.

In our recipe, we read the contents of the file, `input.txt`, which contained a list of four file names. We used `Get-Content` to read the content from the file. `Get-Content` sent the output to the standard out at first, thereby showing us the contents of the file. We then added a pipe to tell PowerShell that we need further processing, and then, added `Remove-Item` to the command chain. (`Remove-Item` deletes items, which could be directories, files or links.)

As we would see later in this chapter, the first parameter (positional parameter, position 1) of `Remove-Item` is `Path`, which is also the parameter that accepts input through the pipeline. For more information, run the following command and read about the `Path` parameter of `Remove-Item`.

```
PS> Get-Help Remove-Item -Parameter Path
```

![](Images/b1fcf9d5-5153-4ba2-a432-5bbcb8028f80.png)

# There's more...

Clean up the contents that we created for this recipe if you are the type that likes directories clean! If we need more files or directories in later recipes, we will create them as needed.

# See also

1.  Recipe 3.8: Understanding cmdlets and parameters
2.  Recipe 1.6: Looking for help information specific to a parameter

# Calling native Linux commands from PowerShell

In the chapter, *Introducing the Core and its Capabilities*, we saw how native Linux commands were not convenience aliases in PowerShell on Linux, but the commands themselves. In this recipe, we would demonstrate using Linux commands at the PowerShell prompt. Remember how we used a Bash terminal to run the commands `ls -l` and `awk` to list the contents of a directory, and separate the columns in the output, in the recipe, *Comparing the outputs of Bash and PowerShell*. We will perform the same operation on the home directory, from with PowerShell, without using any of the PowerShell cmdlets.

# Getting started

It is recommended that you have a Windows PC with PowerShell installed on it (Windows PowerShell would also do) in order to compare the outputs and see if we encounter any errors.

# How to do it...

1.  At the PowerShell prompt, type in the following command to list the contents of the directory.

```
PS> ls -l
```

You see the familiar output (albeit without any of the colours, if your terminal emulator uses colours for file names).

2.  Let us now look at the .NET Type Name of the output. For this, we would need to use the `Get-Member` cmdlet.

```
PS> ls -l | Get-Member
```

PowerShell displays, `TypeName: System.String`, which is consistent with what we saw in the aforementioned recipe.

3.  If you have a Windows PC with PowerShell (or Windows PowerShell), run the same command on it.

```
PS> ls -l | Get-Member
```

Notice the .NET Type Name here; it is `System.IO.DirectoryInfo`, and if you scroll down the console a little, you would also see `System.IO.FileInfo`.

4.  Next, at the PowerShell on Windows (or Windows PowerShell) prompt, type:

```
PS> ls -l
```

You would receive an error, stating that there was no value given to the parameter, `LiteralPath`.

![](Images/d565f397-477e-4b86-9518-f45d18ed8ab4.png)

5.  At the PowerShell prompt on the Windows PC, enter the following and press the Tab key on your keyboard, instead of Enter.

```
PS> ls -l
```

You would see that the parameter name was completed to `LiteralPath`.

6.  Press the Esc key to clear the command line.
7.  Come back to Linux, and at the PowerShell prompt, type in the following and press the Tab key:

```
PS> ls -l
```

8.  Nothing happens. Now, enter the following and press the Tab key:

```
PS> Get-ChildItem -l
```

The parameter name was completed to `-LiteralPath`. Let us take one more step and conclude this recipe.

9.  At the PowerShell prompt on Windows, run the following command.

```
PS> Get-Alias ls
```

![](Images/91a6d14f-bbab-406c-8212-2285ff34399e.png)

10.  Switch back to Linux and run the same command.

```
PS> Get-Alias ls
```

You receive an error stating that there is no such alias.

![](Images/75f2ffac-79de-4a70-af27-a3f0ade44b63.png)

# How it works...

When we run any of the Linux commands on PowerShell on Linux, PowerShell does not call the convenience aliases that were created for the benefit of Linux administrators, when Windows PowerShell was launched; these convenience aliases have not been included in PowerShell on Linux. PowerShell, instead, runs the actual Linux commands and shows the output on the console. Piping the output to other Linux commands work the same way as they do on Bash, when running them on PowerShell on Linux.

The first point to note is that `ls -l` is an actual command in Linux, and it returns the list of files and directories in the current directory, in a table format. When the same command is run on PowerShell on Windows, we receive an error, since PowerShell on Windows interprets `ls` as `Get-ChildItem`, and `-l` as the incomplete-but-definitive call to `-LiteralPath` and returns an error that the literal path was not specified.

When we run `Get-Alias` on `ls` on both the operating systems, PowerShell on Linux returns an error, while PowerShell on Windows shows the underlying PowerShell cmdlet.

The other point that pins down this fact is that the output of `ls` is string, as opposed to a system object, when the same `ls` is run on PowerShell on Windows. On Windows, PowerShell calls `Get-ChildItem` under the hood, and the output shown is that of `Get-ChildItem`. This is supported by the type name in the output of `Get-Member`, which is from the `System.IO` namespace. On the other hand, on Linux, running `Get-Member` on the output of `ls` simply returns `System.String`.

# See also

1.  [about_Aliases](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_aliases?view=powershell-6) (Microsoft documentation)

# Understanding cmdlets and parameters

Most of our scripting and administration is going to revolve around running cmdlets and chaining them. In some situations, we run a cmdlet expecting it to work a certain way, only to find out that the cmdlet threw an error, or worse, did something undesirable.

The key to getting cmdlets to do what we want them to do is  to eliminate ambiguity. In this recipe, we will learn to construct commands contextually and effectively.

# Getting Ready

Read the Help section of the first chapter, *Installation, Reference and Help*. Let us understand the notifications used in the help information that `Get-Help` shows.

While this may not be an exhaustive guide to using help, it should cover most of your daily help document reading needs. The idea is to show you the notations. These notations may appear in several combinations (parameter values in curly braces, surrounded by square brackets, for example).

| **Notation** | **Meaning** |
| `-Parameter <DataType>` | No square brackets: Mandatory parameter, named. The parameter must be called by name, and a value of DataType must be specified. |
| `[-Parameter <DataType>]` | Square brackets around the parameter-data-type-pair: Optional parameter, although, it must be called by name, and a value of DataType must be passed. |
| `[-Parameter] <DataType>` | Square brackets around the parameter name: Positional parameter. You can simply pass a value of DataType to the cmdlet, as long as the value is at the position shown by the parameter in the help text. The parameter need not be called by name as long as the position is right. |
| `[[-Parameter] <DataType>]` | Square brackets around the parameter name, and another pair of square brackets around the parameter-data-type-pair: Positional parameter, which is optional. |
| `-Parameter <DataType[]>` | Square brackets after DataType: Multi-valued parameter. This parameter accepts multiple values as input, each pair of values separated by a comma. |
| `-Parameter` | No data type: Switch parameter. Calling the parameter makes the switch $true, and not calling it uses the default value for the switch. To disable the switch, set it to false, like -Parameter:$false. |
| `-Parameter {Value1 &#124; Value2 &#124; Value3}` | Values surrounded by curly braces: Parameter that accepts predefined values as input. In this case, you would call the parameter like `-Parameter Value1`, or `-Parameter Value2`. In other words, this parameter does not accept arbitrary values. |

Bash champions take note: PowerShell needs a comma separating the values in a multi-valued parameter. Therefore, if you would like to call `Remove-Item` on three files, you would enter `Remove-Item file1, file2, file3`. If only a space separates the values (like Bash's input), PowerShell will consider the three values as values to three positional parameters, and would either throw an error, or do something you did not want it to, based on the cmdlet you call.

In general, anything surrounded by square brackets is optional. Anything surrounded by curly braces indicates predefined parameter values (the pipe separates each value). Data type followed by an empty pair of square brackets indicate array of that data type. And the position of the parameter is to be noted.

Notice the combination: `Required` is false, there is a default value as shown in the text below the parameter name, and the position is `1`. This means that you can simply call the cmdlet, and it would run itself against the default value for its first parameter. The example used here is `Get-ChildItem`.

# How to do it...

That was a long getting ready section. Let us now put this knowledge to use.

1.  Run a command to get a list of files and directories in the current location.

```
Get-ChildItem
```

2.  Let us now add a `.` to indicate the current location.

```
Get-ChildItem .
```

3.  Compare the outputs of the last two commands.
4.  Next, let us go with the following:

```
Get-ChildItem -Path .
```

Is the output the same as that of the last two commands?

5.  Run the following and note the values for each of the keys below:

```
PS> Get-Help Get-ChildItem -Parameter Path

-Path <String[]>
    Specifies a path to one or more locations. Wildcards are permitted. The default location is the current directory (`.`).

    Required?                    false
    Position?                    1
    Default value                Current directory
    Accept pipeline input?       True (ByPropertyName, ByValue)
    Accept wildcard characters?  true
```

6.  Next, create a file in the current location, called `file1` by calling the parameter by name.

```
Get-Help New-Item

.
.
.
SYNTAX
    New-Item [[-Path] <String[]>] [-Confirm] [-Credential <PSCredential>] [-Force] [-ItemType <String>] -Name <String> [-UseTransaction] [-Value <Object>] [-WhatIf] [<CommonParameters>]

    New-Item [-Path] <String[]> [-Confirm] [-Credential <PSCredential>] [-Force] [-ItemType <String>] [-UseTransaction] [-Value <Object>] [-WhatIf] [<CommonParameters>]
```

7.  We have two possibilities: `Path` and `Name`. Look for information on `Path`.

```
PS> Get-Help New-Item -Parameter Path

-Path <String[]>
    Specifies the path of the location of the new item. Wildcard characters are permitted.

    You can specify the name of the new item in Name , or include it in Path .

    Required?                    true
    Position?                    0
    Default value                None
    Accept pipeline input?       True (ByPropertyName)
    Accept wildcard characters?  false
```

If we use `Name`, we have to call it by name (no pun intended). If not, we can specify the name as part of `Path` (no alliteration intended either).

8.  Let us use `Path` first. “`-Path`” need not be written, since it is a positional parameter.

```
New-Item file1
```

9.  Try the same operation with `Name`. This time, mention the parameter name.

```
New-Item -Name file2
```

10.  If you would like, create a third file, by calling `Path` by name.

```
New-Item -Path file3
```

11.  List out the contents of the current location.

```
Get-ChildItem -Path .
```

The files are present.

12.  Let us now delete the files.

```
Get-Help Remove-Item
```

13.  Mention the file names as paths.

```
Remove-Item file1
```

14.  List the contents of the directory.

```
Get-ChildItem -Path .
```

15.  Now, let us delete multiple files in one shot. And this time, let us call the parameter by name.

```
Remove-Item -Path file1, file2
```

16.  Let us now create a directory. We need to use parameter called ItemType, which has predefined values, based on the provider (we are using `FileSystem`).

```
New-Item -Path test-dir -ItemType Directory
```

17.  Create three new files like so:

```
New-Item test-dir/file1, test-dir/file2 -ItemType File
New-Item test-dir/child-dir -ItemType Directory
New-Item test-dir/child-dir/file3 -ItemType File
```

18.  Now, let us delete the contents. Wait for a confirmation prompt to appear after running the command.

```
Remove-Item -Path test-dir
```

19.  Read the prompt. It talks something of the `Recurse` parameter.
20.  Choose `L` and press Enter to abort the process.
21.  Now, enter the following command:

```
Remove-Item -Path test-dir -Recurse
```

22.  That was quiet! List out the contents of the current directory to ensure `test-dir` is gone.

```
Get-ChildItem .
```

The directory is indeed gone.

# How it works...

Working with cmdlets is simple. There are two kinds of parameters: named and positional.

Positional parameters work based on the position. They are programmed in such a way that PowerShell understands their logical sequence and performs its actions. For instance, when moving items, the general way of working is to call the command, pass the source first and then the destination.

Therefore:

```
Move-Item /home/ram/Documents/GitHub /home/ram/Documents/Code/
```

would mean that you want to move the directory, `GitHub` to `Code`. Many PowerShell cmdlets are programmed to understand this.

Named parameters, on the other hand, are to be called by name. Help text shows them without any brackets surrounding them. Calling the positional parameters by name is optional—you are allowed to simply pass the values. However, be careful with what position or sequence you mention them in.

The best practice is to always pass parameter values, calling them by name when writing scripts. When running quick commands, on the other hand, you may omit calling positional parameters by name in the interest of speed.

Some parameters have predefined value validation added to them. These parameters accept only those values that have been defined in them. For instance, `ItemType` only accepts `File`, `Directory`, `SymbolicLink`, `Junction` and `HardLink` as values as of writing this section.

And then, there are switch parameters. `Recurse` is an example. When you call these parameters with no value, the parameters assume `True` in most cases. When you have to set them to `False`, you mention, `-Parameter:$false` (for example, `-Confirm:$false`). If you do not call the switch parameter, the parameter goes with the default value specified in the cmdlet.

# There's more

If you would like to create the files and directories again, don't run four commands. Run the following two.

```
New-Item test-dir/child-dir -ItemType Directory -Force
New-Item ./test-dir/file1, ./test-dir/file2, ./test-dir/child-dir/file3
```

The parameter, Force, creates `test-dir` when creating `child-dir`.

Go ahead and delete the entire directory if you want to, without the `Recurse` parameter. At the confirmation prompt, press Enter (`Y` is the default response).

# Running cmdlets with minimal keystrokes

Commands have been made to be short, historically. However, the situation turned into a dilemma over time, since shorter commands meant that they had to be remembered, and longer commands meant more keystrokes.

PowerShell has long commands, however, it deals with them in two ways:

1.  Aliases, which tend to be shorter.
2.  Tab completion, which require more keystrokes than aliases, but don't require remembering much.

The first way necessitates using our memory to recall command names as required. The second, on the other hand, solves the keystroke issue efficiently.

Bash users are used to getting a list of matches laid out in a nice tabular format when the tab key matches more than one strings in the context. On the other hand, the matches cycle at the cursor in Windows (which most Bash users find "weird").

Be that as it may, tab completion is a boon, and this recipe makes complete use of tab completion and simple string matching to significantly reduce keystrokes when using PowerShell cmdlets.

# Getting Ready

We use the Gnome Terminal terminal emulator for this recipe, and tab completion on PowerShell on Linux on Gnome Terminal behaves exactly the same way that it works on Bash on Gnome Terminal:

*   If only one word matches the string before the tab, the word is completed.
*   If multiple words match the string before the tab, all possible options are listed.

If you are using VS Code for this recipe, or a different terminal emulator, its behaviour may be different.

# How to do it...

Let us get right to it!

Say, we would like to get the list of files and directories within the current directory.

1.  The right way of doing this, as per best practices would be:

```
Get-ChildItem -Path .
```

2.  However, as we've seen before, the easy way of doing this would be:

```
gci
```

We would use the former way when including the cmdlet in a script. This avoids ambiguity, in most contexts that the script would run in. This usually means minimal bugs. The latter, on the other hand, is the short way of running the same cmdlet, by leveraging the user-friendly features of it, combined with the awareness of the environment as an intelligent human. This approach significantly reduces key strokes–three characters, as opposed to twenty-one.

Although, if you are writing a script and would like to reduce keystrokes, you could still do it, without having to remember things such as `gpv` means `Get-ItemPropertyValue`.

Enter: Tab completion.

3.  Follow the keystrokes mentioned below:

```
get-ch<Tab><Space>.
```

Those were ten keystrokes including <Enter>.

There may be situations wherein you would need to call a named parameter. And the named parameter might be long.

4.  Find a command that has `ComputerName` as a parameter.

```
get-comm<Tab><Space>-param<Tab><Space>computername<Enter>
```

This completes to:

```
Get-Command -Parameter computername
```

![](Images/c624b608-e1c3-4cae-91db-beeec2cef223.png)

But it throws an error. The error says, `Possible matches include: -ParameterName -ParameterType`. This is the caveat in PowerShell on Linux. Let us try again:

```
get-comm<Tab><Space>-param<Tab><Tab>
```

![](Images/e5f9420d-d558-4df5-957a-64e2e050e962.png)

5.  Read the list of possibilities and select `ParameterName`.

```
get-comm<Tab><Space>-param<Tab>n<Tab><Space>computername<Enter>
```

6.  The complete resolution of that would be:

```
Get-Command -ParameterName computername
```

And it worked.

Next, let us suspend the activity in our session for, say, five seconds. The cmdlet for this would be `Start-Sleep`.

7.  Let us first get help on the cmdlet.

```
Get-Help Start-Sleep
```

The help text says that the parameter at position one, which need not be named is `Seconds` (square brackets around Seconds in the second parameter set), and it accepts integer values.

8.  Therefore, to suspend the session for five seconds, we would use:

```
Start-Sleep 5
```

9.  If we wanted the session (or script) suspended for 100 milliseconds, we would need to use the named `Milliseconds` parameter. With tab completion, it would be:

```
start-s<Tab><Space>-mi<Tab>100
```

Which would resolve to:

```
Start-Sleep -Milliseconds 100
```

10.  You can, in fact, reduce the number of tabs when using parameter names. Just type enough for PowerShell to uniquely identify the parameter name:

```
start-s<Tab><Space>-m<Space>100
```

Which would resolve to:

```
Start-Sleep -m 100
```

If the delay was not noticeable, feel free to increase the number a little (say, 3000).

# How it works...

We have already seen how to use aliases. Aliases work just like normal cmdlets, including the syntax of their parameters. The only catch is that we have to remember the aliases. Custom aliases, as shall see in the best practices section, are a bad idea given that the aliases have to be imported everywhere we want to run scripts that have custom aliases. 

Tab completion on the other hand, reduces the number of keystrokes, but requires muscle memory. It requires some level of practice, given which, significantly improves productivity. 

Tab completion works when writing cmdlets, writing parameter names, as well as when passing pre-defined values to parameters, such as:  

```
set-exec<Tab><Space>-exec<Tab><Space>unre<Tab> 
```

Which completes to: 

```
Set-ExecutionPolicy -ExecutionPolicy Unrestricted 
```

In many situations, it is not necessary to use tab completion at all, for instance, in the case of `Start-Sleep`. There is no parameter that starts with `m` in case of the cmdlet. Therefore, using `-m` was sufficient for PowerShell to uniquely identify `-Milliseconds`. That saved us the `<Tab>` keystroke as well. 

Productivity with respect to writing scripts in PowerShell is a skill that comes with practice. While aliases sure are a shortcut to speed, they have their perils. On the other hand, using the keyboard to write scripts helps with muscle memory, which not only helps us think in PowerShell, it also helps speeding up tab completion, which works equally well when running commands at the console, or writing scripts. 

Using short parameter names is generally not a good practice while scripting; use these with a similar caution as aliases. Short parameter names affect readability, and also, might break scripts at some point in future. For instance, if you call a certain cmdlet in a script, with a short parameter name `-comp`, which at the time of the creation of the script, stood only for `ComputerName`. Later, imagine the cmdlet received an update with an added parameter, `-CompatibilityMode`; this would break the script that you wrote.

# There's more...

Try to type most commonly used cmdlets along with the parameters to practice tab completion. 

Get familiar with VS Code by typing the cmdlets in the script pane. Notice how cmdlet, parameter and parameter value completion work in VS Code. If you prefer completion to work the same way as at the console, refer my custom settings JSON in the book’s GitHub repository.

# Finding parameter aliases

We worked with aliases for cmdlets, we saw how to uniquely identify parameter names without having to type the entire parameter name, and we also looked at leveraging the power of tab completion. 

To complete the cycle, let us also look at parameter aliases. 

As you may have guessed, parameter aliases work very similar to cmdlet aliases. The primary goal of these aliases is to reduce keystrokes. 

Parameter aliases are not documented in a friendly way, however, can be easily found thanks to the object-oriented model of PowerShell. In this recipe, we shall look at how to fetch parameter aliases. 

# Getting Ready

Find all the commands that take in `ComputerName` as a parameter, with minimal keystrokes.

```
get-comm<Tab>-parametern<Tab>Cn
```

This resolves to:

```
Get-Command -ParameterName Cn
```

![](Images/7de20ecf-5174-4e9e-a5ae-9e024c717114.png)

The output was the same as what we ran a while ago:

```
Get-Command -ParameterName ComputerName
```

How did PowerShell know that `Cn` stands for `ComputerName`?

# How to do it...

Parameters are part of cmdlets, and `Get-Command` is the cmdlet that fetches information about cmdlets.

1.  For this example, let us pick the cmdlet, `Invoke-Command`.

```
Get-Command Invoke-Command 
```

2.  Examine the object that this command outputs. 

```
Get-Command Invoke-Command | Get-Member 
```

3.  The output shows a member called Parameters. Use the member access operator to pick the member. 

```
(Get-Command Invoke-Command).Parameters 
```

4.  See what members this member contains. 

```
(Get-Command Invoke-Command).Parameters | Get-Member 
```

5.  Would Values show us the information we need? 

```
(Get-Command Invoke-Command).Parameters.Values 
```

6.  Yes, that does give us something, but there is too much output. We need only the parameter names and their aliases. 

```
(Get-Command Invoke-Command).Parameters.Values | select Name, Aliases 
```

There you go.

# How it works...

We saw while reading about the Core and its capabilities, that PowerShell, most of the time, returns objects. And every object can have objects within itself. Going by the same path as that of .NET, a member access operator can be used to select the members (which could be properties or methods). Properties are addressed by simply using the property names, while methods need arguments passed to them (an empty pair of parentheses is still needed if no argument is being passed). 

The parameters of a cmdlet are objects of the output that the `Get-Command` cmdlet returns. Therefore, calling `Get-Command` with the cmdlet, `Invoke-Command` returns data about `Invoke-Command` as the output object. This can be further broken down to several other objects (members), among which, there is `Parameters`.

`Parameters` itself can be further broken down into other members, `Values` being one of them—`Values` contains the names of the parameters, as revealed by running `Get-Member`. 

We select two objects from within `Values`, called `Name` and `Aliases`. 

These parameter aliases can be used in place of parameters themselves. 

There are two caveats with parameter aliases: 

*   They are case-sensitive, which means reaching for the Shift key. 

*   They have to be remembered, even though they have a pattern to them, just like how cmdlet aliases do (`ip` for `Import` and `g` for `Get`, for instance).

# Calling a PowerShell script

PowerShell scripts are nothing but a series of PowerShell cmdlets, each in a line of a `ps1` file. These instructions are executed one after the other, similar to the good old shell script. Using VS Code makes running PowerShell scripts simpler, in that you simply have to run the script to make the script work its magic.

However, running PowerShell scripts on VS Code is not the usual way of automation for obvious reasons. Also, there are many ways to run a PowerShell script. We shall look at a very simple way of running the script in this recipe; as we progress in the book, we will also add more features to our scripts, and further, will package them into modules for future use.

# Getting Ready

This recipe uses VS Code to write the script. While any text or code editor would work for the script, we use VS Code because in my experience, VS Code is the friendliest editor for  PowerShell scripting.

1.  Open VS Code, create a new file.
2.  Create a new directory at a convenient location (`~/Code`, perhaps?).
3.  Save the empty file as `hello-world.ps1` within the directory you just created.
4.  Observe the bottom right of VS Code; it should now say, `PowerShell`.
5.  Press `` Ctrl + ` `` to close the console at the bottom to reduce distraction.

If everything is as shown in the screenshot below, you are good to go. (Ignore the colour of the status bar at the bottom, as well as the git status at the bottom-left for now.)

![](Images/23eb3582-a3de-490a-804e-16c977434c72.png)

# How to do it...

1.  At the script pane, type in:

```
Write-Host "Hello, World!"
```

2.  Save (**File** > **Save** or `Ctrl + S`) the script.
3.  Click on **Debug** in the left. Alternatively, press `Ctrl + Shift + D`. This opens the Debug pane.
4.  Press the green play-button-like **Start debugging** button.

The console should pop out and display `Hello, World!`.

5.  Let us run the script one more time. This time, we will not open the Debug pane or press buttons on the screen. Simply, press `F5`.

`Hello, World!` should again be displayed in the console.

![](Images/0ab2165b-fadb-4c0e-b8e4-b87e283c3067.png)

Let us now call the script without using the debug controls.

1.  Close the file (Ctrl + W).
2.  At the prompt on the console, type in:

```
./hello-world.ps1
```

You should see `Hello, World!` appear.

3.  Now, navigate to home.
4.  Next, type `&`, add a space, `./` and start typing the path to where you stored the script. Use tab completion just like how you would on Bash.
5.  When you reach the location of the script file, press Enter to call the file.

![](Images/7d6b31d4-f323-4db3-81a8-b7aaa3faf1b9.png)

# How it works...

The simplest way to run a PowerShell script is to debug it at the Integrated Scripting Environment. We use VS Code as our ISE of choice in this case. The other two ways of calling the script described in this recipe are from the PowerShell console. You may use the integrated console in VS Code, or a PowerShell console called at the Terminal for this purpose.

When the script is located at the present working directory, PowerShell just calls the `ps1` file and executes it. Another way of calling PowerShell scripts is to use `&` (or the **call operator**): type `&` followed by a space, followed by the path to the script file. This way of calling handles spaces in the path well.

If the path to the script contains spaces, the path would need to be surrounded by quotes. This would make PowerShell think that you are simply giving it a string value. PowerShell would, then, simply display the path as text the moment you press Enter.

When you use the `&` call operator, you tell PowerShell that you want to run a script (or a command).

Another way of calling scripts is to use `.` (or the **dot operator**), which we shall look at in the next recipe.

# Dot-sourcing a PowerShell script

In the previous recipe, we saw how to call PowerShell scripts from outside of the ISE. We gave PowerShell the path, and explicitly mentioned that we would like it to run the script, by using a call operator.

This way is ideal if you would just like the script to perform its task and not leave anything behind, like variable values and such. However, there are situations wherein we would like to run a script and, say, retain values of the variables we declared and assigned in them, or use the functions we declared in them.

In such situations where we would like the functions, variables and even aliases retained in the current session, we use dot-sourcing.

# How to do it...

If you deleted the file after the previous recipe, restore it or recreate it using the steps in the previous recipe. Then,

1.  Open the script file that you created in the previous recipe. At the second line, type the following.

```
$Message = "I was dot-sourced!"
```

2.  Save the script. Do not run it yet.
3.  Place your cursor at the integrated console, and call the script using the call operator.

```
& ./hello-world
```

4.  We declared $Message and assigned a string value to it. Call the variable to see what value it contains.

```
$Message
```

Nothing.

5.  Now, dot-source the script. (There are two dots; one is the operator, and the other after the space is reference to the current directory.)

```
. ./hello-world.ps1
```

6.  Call the $Message variable again.

```
$Message
```

![](Images/a0c0e9b2-1b76-46b1-97de-239dcda9adea.png)

# How it works...

When a script or a command is called using the call operator, the script or command is simply run without the current session (or technically, scope) being modified. The command or script runs and exits without changing anything pertaining to the session, including changes to built-in/automatic variables.

When changes to the scope are desired, the script or command must be dot-sourced. This way, whatever variables, functions or aliases are defined in it, are retained in the current scope.

# There's more...

Create a new alias using `New-Alias` within the `hello-world.ps1` script. Try to get the value of the alias after first calling the script (using the debug control, as well as using the call operator), and then, by dot-sourcing the script. Observe the outcomes.

# Calling a PowerShell cmdlet from outside of PowerShell

So far we have learnt to call cmdlets from the console, run scripts at the ISE, and call scripts in two modes. In this very short recipe, we shall learn how to call a PowerShell cmdlet from outside of PowerShell.

# How to do it...

1.  Open a Terminal window.
2.  At the prompt, type:

```
pwsh -h
```

3.  Read the syntax for the command.
4.  At the prompt, type:

```
pwsh -c Get-ChildItem
```

![](Images/23321ef5-fc49-4e61-a77e-e957c0051db9.png)

5.  Let us now run the `hello-world.ps1` script.

```
pwsh -f ./Documents/code/github/powershell/chapter-3/hello-world.ps1
```

![](Images/705055a1-23b9-4322-bb0b-ee77122284eb.png)

# How it works...

PowerShell is not an application that runs on top of Bash. PowerShell is a shell itself. However, it can be called from with Bash just like another application. Like applications, the `pwsh` command takes in arguments, which are then processed by PowerShell.

The two main ways we may want to use PowerShell from within Bash is to run a single command, or call a script file. You can even call a script block, however, this must be done from within PowerShell. In most cases, running single cmdlets or calling a script should suffice.

In general, when calling `pwsh` with cmdlets, make `-Command` (or `-c`) the last parameter, since anything that comes after the cmdlet itself is considered cmdlet arguments. Same goes for `-File` as well.

When a script is designed to accept arguments, the script arguments can be passed after the script name, just like with cmdlets.

# Recording the cmdlets run on the PowerShell console

Often, there are situations in which you perform a series of tasks on your PowerShell console, and after quite some trial-and-error, come across a solution. And then, you wish you had recorded everything you did on the console. You could still copy content from the console, so you try to scroll up. But you can only go so far. Your command history (a little like Bash history) can help you, but sometimes, that feels limited as well.

A few months ago, we were troubleshooting a sync issue between two of their software update distribution systems which were supposed to work in sync. After some of us were done beating around the GUI, (of course) we decided to pick PowerShell to fix the issue. We ran a series of commands, and after a few hours of fighting with the systems, the systems yielded, and we were back up and running.

Our managers asked for all the steps that we took to achieve this, so that they could be documented for future use. Of course I cannot tell you all the steps that we took—because: a) scope of the book, and b) agreements with our clients—but I can tell you what can help in such situations.

# How to do it...

Start PowerShell at the terminal, or use the PowerShell Integrated Console on VS Code.

1.  Run the following command:

```
Start-Transcript -Path ./command-transcript.txt
```

2.  You can also simply run the cmdlet without any arguments; it would automatically create a text file with an auto-generated file name. Get the current system date and time

```
Get-Date
```

3.  List out all the files and directories in the current location.

```
Get-ChildItem .
```

4.  Create a new directory.

```
New-Item test-transcript -ItemType Directory
```

5.  Create a new file within the directory.

```
New-Item -Path test-transcript/testing-transcript.txt -ItemType File
```

6.  Add content to the file.

```
@'
In publishing and graphic design, lorem ipsum is a placeholder text commonly used to demonstrate the visual form of a document without relying on meaningful content (also called greeking).
Replacing the actual content with placeholder text allows designers to design the form of the content before the content itself has been produced.
—Wikipedia
'@ | Out-File ./test-transcript/testing-transcript.txt -Append
```

7.  Delete the directory.

```
Remove-Item -Path ./test-transcript -Recurse
```

8.  Stop recording what you did.

```
Stop-Transcript
```

9.  You should have now received the location of the transcript file. Read the contents of the file.

```
Get-Content -Path ./command-transcript.txt
```

![](Images/3b8eda4d-a326-4155-b8ea-67f3d63f7aa3.png)

# How it works...

A transcript created by running `Start-Transcript` stores all of your actions and the console output of all of the commands you ran, in a text file. The transcript also contains some of other useful information pertaining to the context the commands were run in.

A transcript file is a little more than a history file, in that the former contains the output of the commands, apart from the commands themselves.

The `Start-Transcript` cmdlet does not require any argument at all; it can create a text file at the user's home, with a unique name to ensure that no other transcript is rewritten. In other words, `Path` is an optional parameter.

This concludes this chapter about preparing for administration using PowerShell. It's time to crack your knuckles and refill your coffee mug. Did I tell you coffee speeds up thinking in PowerShell? Placebo, you say? Let's not get into an argument right now.

# First Steps in Administration using PowerShell

In this chapter, we cover the following topics:

1.  Working with date properties
2.  Working with date and time functions
3.  Working with currently running process to measure resource consumption
4.  Launching and stopping a process
5.  Finding the owner of a process
6.  Invoking an application based on the file type
7.  Installing the CronTab module
8.  Scheduling jobs in PowerShell
9.  Removing scheduled jobs in PowerShell

# Introduction

As per Harvard Business Review, a way to effectively learn is to cycle between *information feasting* and *information fasting*. Given that we have familiarised ourselves (and perhaps a little overwhelmed by the volume of the last chapter), we will take a lighter approach to our first steps to administration using PowerShell.

So far, we have seen how to run cmdlets, what their parameters are, how to set and use aliases, etc. In this chapter, we would learn how to use some basic utilities, work with processes, and call applications.

Also, even though the title of the book says Linux, most of the recipes in the book should work on Windows as well (especially PowerShell 6.0 on Windows); minor modifications may be required, such as using the backslash in paths.

# Working with date properties

PowerShell is best learnt, starting with simple cmdlets. And `Get-Date` is one of the simplest-yet-not-completely-leveraged cmdlets present in PowerShell. In this recipe, we shall play with dates and see how they can be used in different scenarios. As always, the possibilities with PowerShell are quite more than a book can cover. In the interest of brevity, we will look at just enough to enable you to launch yourself gracefully into the world of PowerShell automation; the rest, you would be able to handle by yourself.

# Getting Ready

If you followed along the previous chapters and performed all the exercises mentioned in them, you should be good to go. Otherwise, go to the chapter, *Installation, Reference and Help*, and get yourself a copy of PowerShell. Come back here to continue. This recipe uses only the terminal, so there is no need for anything else.

# How to do it...

Before we start working with dates, let us make a simple call for the date.

1.  Display the current date and time.

```
PS> Get-Date

Saturday, 16 June 2018 12:14:07
```

2.  Find out what members this returned object has.

```
PS> Get-Date | Get-Member
```

![](Images/2fa6a427-d4fb-4f66-a683-816c5e5d09d4.png)

A whole bunch of properties and methods.

3.  Attempt to display the date like 16/06/2018.

```
PS> $Date = Get-Date
PS> "$Date.Day/$Date.Month/$Date.Year"
```

![](Images/5e6589ce-2bd7-48fd-83f3-13864445c379.png)

The colours do not look right.

4.  Change the command as follows. The syntax should look better now, based on your terminal theme. (Don't worry about why the change works for now; we shall look at it when dealing with variables at a later point.)

```
PS> "$($Date.Day)/$($Date.Month)/$($Date.Year)"
16/6/2018
```

But that was a lot of work. Is there an easier way?

5.  Look in Help to see what parameters you get.

```
PS> Get-Help Get-Date
```

There is a `Format` parameter.

6.  Type the following to get the short date.

```
PS> Get-Date -Format d
```

Try the following as the values for `Format`: `g`, `U`, `yyyy/MM/dd` and `yyyyMMddhhmmss`.

![](Images/58296173-4b02-41ea-881a-9f97745811eb.png)

7.  If you're more comfortable with the UNIX formatting of date, use the `Uformat` parameter.

```
PS> Get-Date -Uformat %d/%m/%Y
```

Let us take one more step to pass a custom date to the system and fetch a little information from it, leveraging the members of the object that is output by `Get-Date`.

8.  Find what day Halloween falls on, in 2018.

```
PS> (Get-Date -Day 31 -Month 10 -Year 2018).DayOfWeek 
Wednesday
```

9.  If you know how date in your locale works, pass the date as follows and get the same information.

```
PS> (Get-Date 31/10/2018).DayOfWeek
```

10.  If you remember the concept of Type Accelerators, use it to get the information you need.

Remember to use the YMD or MDY format when calling the `DateTime` accelerator, in order to avoid errors.

```
PS> ([datetime]'10/31/2018').DayOfWeek
```

To avoid ambiguity, spell out the month.

```
PS> ([datetime]'31 October 2018').DayOfWeek
```

# How it works...

The `System.DateTime` class in .NET packs a good-enough amount of properties and methods. The `Get-Date` cmdlet leverages these properties and methods by means of encapsulation. The `Get-Date` cmdlet, by default, pulls the current date and time of the system, and allows you to pick child objects from it, or quickly tie them together as *formats*.

Besides these operations, the cmdlet also allows you to pass simple string formed like date and time, and converts the input string into the `DateTime` object.

While `Get-Date` takes into account your current locale, the type accelerator, `DateTime`, seems to work on YMD- or the MDY-formatted date-time.

# See also

1.  The [DateTimeFormatInfo](https://msdn.microsoft.com/library/system.globalization.datetimeformatinfo.aspx#Remarks) Class | Remarks (Microsoft Developer Network)
2.  Recipe 2.3: Parsing input from text to object (Type Accelerators)

# Working with date and time functions

In the previous recipe, *Working with date properties*, we focused on the properties that the `DateTime` object has. The parameters we saw for `Get-Date` also worked on these properties. In this recipe, we shall look at methods within the `DateTime` object, and learn to use them to our benefit. The main idea behind this recipe, though, is to make you comfortable using methods that are part of the output objects.

# How to do it...

Let us first start with converting local time into UTC.

1.  At the prompt, type in `Get-Date` and list out the members of the output object.

```
PS> Get-Date | Get-Member
```

2.  There is a method, called `ToUniversalTime`. Call the method.

Reduce keystrokes by using tab-completion.

```
PS> (Get-Date).ToUniversalTime()
```

Compare the output to your local time.

3.  Next, let us see what day it would be, exactly thirty-five days from today.

```
PS> (Get-Date).AddDays(35)
```

4.  If you would like to see what time it would be after three hours and eighteen minutes:

```
PS> (Get-Date).AddHours(3).AddMinutes(18)
```

5.  Next, find out how many days have passed since the World Environment Day, 2016.

```
PS> (Get-Date).Subtract((Get-Date '5 June 2016'))
```

![](Images/f40255e1-1726-409d-ab88-f5eae0366a3b.png)

# How it works...

The object that is returned by `Get-Date` has several methods just like how it has properties. In this recipe, we use the methods to manipulate date the way we need it. Methods are called with arguments. When you do not want to specify any argument, ensure still to call the methods with an empty pair of parentheses.

Methods can be chained in the way we did in adding hours as well as minutes. As long as the output object does not change, in most cases, you should be able to call methods pertaining to the object by chaining them. If, for instance, you convert the date object into string at the first method, the second method should be a string-input-enabled method. When in doubt, use the `Get-Member` cmdlet on the output to see what methods it would support.

When you look at `Get-Member` run against the `DateTime` object, you see that the `Subtract` method accepts `DateTime` as its argument. Hence the use of `Get-Date` *within* the argument. Passing a cmdlet output as an argument to a method requires the cmdlet, along with the parameters that are passed, to be enclosed within an additional pair of parentheses–`Subtract((Get-Date '5 June 2016'))` as opposed to `Subtract(Get-Date '5 June 2016')`–so that the inner command is executed first to get a value, and then, passed to the method.

# Working with currently-running processes to measure resource consumption

A good chunk of administration involves working with processes on a given computer. PowerShell contains cmdlets that enable you to work with processes on a computer. In this recipe, we will list out all the processes running in the system, and fetch the amount of resources the processes are collectively consuming.

In the following chapter, *Passing data through pipelines*, we would look at other options such as filtration and so on, using what we learn in this recipe.

# How to do it...

As we already discussed, our goal here is to work with processes.

1.  List out the cmdlets that help you work with processes.

```
PS> Get-Command -Noun Process
```

Remember that PowerShell uses only singular nouns.

We get five cmdlets. What we initially need is Get-Process.

2.  Run the cmdlet to see what it shows.

```
PS> Get-Process
```

The output is a long table of processes, the memory they are consuming, the CPU time they are using, etc.

3.  Get the total count of processes currently running in the system.

```
PS> (Get-Process).Count
```

4.  Now, fetch the average of the pages of memory used by the processes. The term for this is Working Set, denoted as WS.

```
PS> Get-Process | Measure-Object -Property WS -Average
```

5.  There are other fields in the hash table as well. Let us get all of that information.

```
PS> Get-Process | Measure-Object -Property WS -Average -Sum -Minimum -Maximum
```

6.  Get the average, sum, minimum and maximum for both, the working set, as well as the CPU.

```
PS> Get-Process | Measure-Object -Property WS, CPU -Average -Sum -Minimum -Maximum
```

![](Images/4352fcb8-f849-4aa5-8832-54d1d1d7f056.png)

# How it works...

The cmdlet, Get-Process, gives out an entire table of all the processes running in the system. Think of each row as an individual object, and the entire table as an array of these rows. Count (or in other words, length) is, logically, a property of an array. Therefore, we call the cmdlet, and on the object that is output, we run a counting operation. This gives us how many processes are running in the system at the moment.

The next cmdlet we see is an important one, as well: `Measure-Object`. This cmdlet is designed to perform measurements on the objects that are output. In our case, we pick the property, `WS` to perform measurements on. If no property is specified, PowerShell will pick the property based on its definition in the output object.

`Measure-Object` is capable of performing some neat arithmetic calculations on the output object. We use this capability of the cmdlet to fetch the average first, and then, the sum, the minimum value, and the maximum value as well. The `Property` parameter accepts a string array as input (`Get-Help Measure-Object -Parameter Property`). Therefore, we specify WS as well as CPU (separated by commas) in the cmdlet, and then perform the measurement operation.

# Launching and stopping a process

All pro-terminal administrators launch and stop processes from the terminal all the time. This usually happens at the terminal prompt on Bash. With PowerShell, the process is not very different. This recipe will show you how to work the processes. And by the way, this recipe where you go on a full information fast.

# Getting Ready

Open VS Code. If the status bar at the bottom is blue, chances are that a folder is open in VS Code. VS Code saves the location it is open at, and so, even if you start a session of VS Code after a fresh reboot, you would still see a folder open. We need the folder closed. To do this, press Ctrl + Shift + N (or go to File > New Window). Close the window where a folder is open.

# How to do it...

If you listed out the commands in the previous recipe, scroll up to find what cmdlets might help you with this recipe.

1.  At the prompt, type in the following to start Visual Studio Code.

```
PS> Start-Process code
```

Ensure that the status bar at the bottom is not blue. If it is blue, read the *Getting Ready* section of this recipe. Press Ctrl + Shift + E or click on Explorer icon on the left sidebar of VS Code. There should not be any directory open there.

2.  Open VS Code at the directory you created the `hello-world` script.

```
PS> Start-Process code -ArgumentList /home/ram/Documents/code/github/powershell/
```

Press Ctrl + Shift + E or click on Explorer icon on the left sidebar of VS Code. Do you see the directory open?

Now, let us stop the VS Code process.

3.  List out the processes running in the system and see if anything matches `code`.

```
PS> Get-Process | grep code
```

4.  If you want the PowerShell way of doing it, run the following command and note the name in the `ProcessName` column:

```
PS> Get-Process *code*
```

5.  PowerShell deals with objects; `grep` outputs text. Therefore, now that we know that the exact name of the process is `code`, we directly get details on the process.

```
PS> Get-Process code
```

That gives us a valid output.

6.  Stop all the `code` processes.

```
PS> Stop-Process code
```

That would not work; the cmdlet accepts a `System.Diagnostics.Process` object as input.

7.  Enclose `Get-Process` within parentheses and pass the input to `Stop-Process`.

```
PS> Stop-Process (Get-Process code)
```

8.  Now, see if there is a `code` process running any more.

```
PS> Get-Process code
```

![](Images/d4e99014-7a79-4f58-9d80-a711853638b3.png)

The best way of stopping a process is using its ID.

9.  I am running `dconf-editor` on my PC right now, and would like to close it. You may choose any process to stop; play safe, though.

```
PS> Get-Process dconf-editor
PS> Stop-Process -Id 20608
```

# How it works...

The cmdlet, Start-Process, works with paths. In case of `code`, though, Linux knows the path where the package is installed. Therefore, simply calling the package by "command" is sufficient.

The VS Code process accepts directory/file location as an input. Therefore, we add the `ArgumentList` parameter and pass the path to the process as an argument. This opens that directory in VS Code.

Stopping a process requires a .NET object as input by default; `Stop-Process` would not accept string as the default input. Therefore, we enclose the `Get-Process` cmdlet within parentheses, so that it gets executed first and outputs a `System.Diagnostics.Process` object, which is then processed by `Stop-Process`.

In order to be exact with respect to which process we would like to stop, we use the Process ID, and pass it as the argument to `Stop-Process`.

# Finding the owner of a process

In the recipe, *Working with currently-running processes…*, we listed out the processes running in the system. The table did not show us the process owner. In this recipe, we look at working with processes started by a certain owner.

# How to do it...

The `Get-Process` cmdlet can fetch us this information.

1.  At the prompt, type the following to get all the parameters that the `Get-Process` cmdlet accepts.

```
PS> Get-Help Get-Process
```

2.  We see a parameter `IncludeUserName` (the name suggests it is a switch parameter). Get more information on it.

```
PS> Get-Help Get-Process -Parameter IncludeUserName
```

![](Images/c0afced1-67c8-48e2-bb2a-faff5025c2b6.png)

3.  Run the command:

```
PS> Get-Process -IncludeUserName
```

4.  Filter out the processes started by you. We will use `grep` for this operation, until we learn how to filter in PowerShell.

```
PS> Get-Process -IncludeUserName | grep ram
```

5.  Count the number of processes running under your name.

```
PS> (Get-Process -IncludeUserName | grep ram).Count
```

6.  If you would like to use the `Measure-Object` cmdlet, you can.

```
PS> Get-Process -IncludeUserName | grep ram | Measure-Object
```

7.  Let us now see how what amount of working set all of the processes started by you consume.

```
PS> Get-Process -IncludeUserName | grep ram | Measure-Object -Property WS -Sum
```

![](Images/ca96880c-e0ef-4261-9578-d0b31a8234e2.png)

There is an error.

# How it works...

`Get-Process` does not show you the process owner information by default. In some situations, it may be necessary to have this information. In this simple recipe, we use the help documentation to get all the parameters and use the `IncludeUserName` switch parameter to get the process owner information.

In the next step, we filter out the processes started by a certain user, and then, count the number of processes. We do the same using `Measure-Object` as well, and notice that the output is the same. `Measure-Object` has "object" in its name, but worked on text that was output by `grep`. At the same time, it said at the next step that the value of `Property` is invalid.

The answer to why `Measure-Object` worked when counting, is in the step that precedes it. We know that if an array is output, PowerShell can count the number of elements in the array. `Measure-Object` is also capable of the same: measuring what can be measured in string arrays—`Count` works on string arrays.

However, when we tried to fetch the total working set, `Measure-Object` could not get us that. The reason is that the output of `grep`, as we have seen before, is plain text.

```
PS> Get-Process -IncludeUserName | grep ram | Get-Member
```

# There's more...

Something perhaps a few steps ahead, but, what if we wanted to get that working set information anyway, from the output of `grep`? Simple challenge, accepted.

```
PS> Get-Process -IncludeUserName | grep ram | awk '{print $1}' | ForEach-Object {[Double]$_} | Measure-Object -Sum
```

![](Images/a7449853-658a-4dc1-bb60-82cb93f4e8f3.png)

Do not worry too much about how that works, for now. Once we read and understand looping through available elements, we will have a better understanding of how we got this to work. For now, understand that we converted each of the returned strings into `double` values using the `Double` type accelerator. Then, we did a `Measure-Object` and found the sum.

Of course, with only PowerShell, this would be much simpler.

# See also

1.  Recipe 2.4: Comparing the outputs of Bash and PowerShell.

# Invoking an application based on the file type

So far, we have seen how to use `Start-Process` to start an application. That involves, in many cases, launching the application, and from the application, opening a file that you want to work on, using the application. In this recipe, we will leverage the concept of file association, and a proper calling cmdlet to launch an application. In fact, we will go a little further than that.

# How to do it...

Download a few images from the web to work with this recipe. They could be anything, just ensure that all of them are of the same file type.

1.  Navigate to the location where you saved the image files.
2.  At the prompt, type in the following command to open your image viewer, and the files in it.

```
PS> Invoke-Item -Path *.png
```

3.  Now, create a text file in the same location.

```
PS> New-Item file-1.txt -ItemType File
```

4.  Now, invoke all the files in their respective applications.

```
PS> Invoke-Item *
```

# How it works...

In the recipe, *Calling a PowerShell cmdlet from outside of PowerShell*, we called a PowerShell script from Bash by first invoking PowerShell and then passing the script as an argument to the `pwsh` command. The process is very similar in PowerShell as well, as seen in *Launching and stopping a process*.

The `Invoke-Item` cmdlet relies on the internal file association to open the files. The real use of `Invoke-Item` is when opening multiple files, whether of the same kind, or different kinds of files within the same path using the respective applications that handle them.

# Installing the Crontab PowerShell module 

In this recipe, we will discuss the installation details of a PowerShell module to manage Cron jobs using PowerShell on a Linux machine.

There are times when there is a need for performing administrative tasks or scheduling a script to execute automatically at given time. Linux distros, by default, come with a scheduling utility, called, Crontab, which allows any given tasks to be run automatically in the background at a given time. Cron is a time-based scheduler program. It generates events based on the definition in the `crontab` file.

# How to do it...

The PowerShell crontab wrapper module is not available in the PowerShell repository as yet. You must download the files manually to install the module. The simplest way is to clone the PowerShell repository and install the module from within its `demos` directory.

If you would rather only install the CronTab module alone, download the `<repo>/demos/crontab` *directory* manually. Then, start PowerShell as super-user, and navigate to `crontab`. Continue from step 4.

1.  Clone the PowerShell repository on to your computer.

```
$ mkdir ~/code
$ git clone https://github.com/PowerShell/PowerShell.git
```

2.  Start `pwsh` as a super-user.
3.  Go to the `demos/crontab/CronTab` directory within the repository. This is where the module manifest is placed.

```
PS> Set-Location ~/code/PowerShell/demos/crontab
```

4.  Use the `Import-Module` cmdlet on the module manifest to import the module.

```
PS> Import-Module -Name ./CronTab/CronTab.psd1
```

5.  To list the components of CronTab module use the `Get-Module` cmdlet.

```
PS> Get-Module -Name CronTab | Format-List
Name : CronTab
Path : /home/PacktPub/CronTab.psm1
Description : 
ModuleType : Script
Version : 0.0
NestedModules : {}
ExportedFunctions : {ConvertTo-CronJob, Get-CronJob, Get-CronTab, Get-CronTabUser...}
ExportedCmdlets : 
ExportedVariables : 
ExportedAliases : 
```

6.  To list the available command types of `CronTab` module use  the `Get-Command` cmdlet.

```
PS> Get-Command -Module CronTab  
CommandType Name Version Source
----------- ---- ------- ------
Function ConvertTo-CronJob 0.0 CronTab
Function Get-CronJob 0.0 CronTab
Function Get-CronTab 0.0 CronTab
Function Get-CronTabUser 0.0 CronTab
Function Import-CronTab 0.0 CronTab
Function Invoke-CronTab 0.0 CronTab
Function New-CronJob 0.0 CronTab
Function Remove-CronJob 0.0 CronTab
```

# How it works...

When you download theCronTab module,  the following files get copied to the CronTab folder from the URL mentioned in the recipe, and these files contain the module data.

1.  CronTab.ps1xml
2.  CronTab.psd1
3.  CronTab.psm1

The `Import-Module` cmdlet registers the cmdlets available in the module into the PowerShell session and makes the module ready for use. The Import-Module cmdlet is run against the module manifest, which is the `psd1` file. 

When you run the `Get-Command` cmdlet, you get a list of all the cmdlets available in the module.

# Scheduling jobs in PowerShell

In this recipe, we will see how to schedule a job using PowerShell cmdlets.

# Getting Ready

1.  Log in to the terminal using SU privileges.
2.  Open a PowerShell console using the `pwsh` command.
3.  Import the module (refer the recipe: Installation of the Crontab PowerShell module).

# How to do it...

1.  First, check the existence of the command or scripts that you want to schedule from a terminal 

```
$ pwsh -f "/tmp/DataLoading.PS1;"
```

2.  To run the script based on a schedule, use the `New-CronJob` cmdlet.

```
PS> New-CronJob -Command 'pwsh -f "/tmp/DataLoading.PS1;"' -Minute 0,15,30,45 | Out-Host

PS> New-CronJob -Command 'pwsh -f "/tmp/DataLoading.PS1;"' -Minute */15 | Out-Host

PS> New-CronJob -Command 'pwsh -f "/tmp/DataLoading.PS1;"' -Minute */15 -Hour 10-12 | Out-Host 

PS> New-CronJob -Command 'rm -rf /tmp/clr*' -Minute 15 -Hour 1 | Out-Host 

PS> New-CronJob -Command 'pwsh -f "/tmp/DataLoading.PS1;"' -Minute */15 -Hour 10-12 -DayOfWeek sun,tue,fri -Month Jan,Mar,Jun,Sep,Dec | Out-Host
```

3.  To get the list of currently scheduled jobs, run the `Get-CronJob` cmdlet.

```
PS /home/PacktPub> Get-CronJob |Format-Table -AutoSize 
Minute Hour DayOfMonth Month DayOfWeek Command
------ ---- ---------- ----- --------- -------
2 * * * * python ./pythonexmaple.py
5 1 * * * rm -rf /tmp/clr*.*
15 * * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 * * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
0,15,30,45 * * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 10-12 * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 10-12 * Jan,Mar sun,tue,fri /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
```

4.  To view the contents of scheduled jobs in the crontab configuration file, use `Get-CronTab`. 

```
PS > Get-CronTab 
2 * * * * python ./pythonexmaple.py
5 1 * * * rm -rf /tmp/clr*.*
*/15 * * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
0,15,30,45 * * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 10-12 * * * /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 10-12 * Jan, Mar, Jun, Sep, Dec sun, tue, fri /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
```

# How it works...

The PowerShell implementation of `crontab` technically a wrapper, which encapsulates the `crontab` commands that work in Linux. Why use PowerShell to schedule jobs if the underlying functions are that of `crontab`? The reason would be the uniformity of usage, the consistency and the object-oriented approach. If you know to use PowerShell, that is all you need in order to be able to use `crontab` as well. That is the goal.

The New-CronTab cmdlet is used to define new tasks. The parameters available define the frequency with which the tasks are to be executed. The Cron jobs are executed with the same privileges as with which the `New-CronTab` cmdlet was executed. In other words, if you launched PowerShell as a super-user and ran New-CronTab to define a schedule, the commands that would be run on the specified schedule would be run with super-user privileges.

In the steps, the command to run is listed using `-Command` parameter.

Let us also look in brief how what inputs the New-CronTab accepts. There are two ways to run a command every 15 minutes: The first is where each minute is specified:

```
0,15,30,45 * * * * /path/command
```

Alternatively,  you can simplify the same to `*/15`.

```
*/15 * * * * /path/command
```

Range can also be specified for scheduling a job. In our example, the job runs at 10 A.M,11 A.M and 12 P.M hours using the range option.

```
*/15 10-12 * * * /path/command
```

In the last example, (the Names format), the job is scheduled to run using the DayOfweek (Sun, Tue, Fri) and Month (Jan, Mar) parameters.

```
*/15       10-12 *          Jan,Mar sun,tue,fri /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
```

The Cron Table configuration is read using `Get-CronTab` cmdlet. Each line represents a record of metadata about the scheduled job; it specifies the frequency and the command/script that should be executed.

The caveat as of now is that if you setup Cron jobs incorrectly they appear to silently fail. Cron has an own reserved `syslog` facility, so you should have a look at the `/etc/syslog.conf` file (or the equivalent file in your Linux distro) to see where messages from `cron` are sent. The common destinations include `/var/log/cron`, `/var/log/messages` and `/var/log/syslog`.

# Removing the jobs in PowerShell

In this recipe, we're going to see the steps to remove the entries from the CronTab file.

# How to do it...

That we have created entries into the `cron` configuration file, let us attempt to remove those entries.

1.  List the jobs using the `Get-CronJob` cmdlet. This will get you the list of jobs that are created by reading the `CronTab` file

```
PS> Get-CronJob | Format-Table -AutoSize
```

2.  Now, apply a conditional logic to segregate the required job entries using `Where-Object` clause. You will read more about this in the chapter, *Passing Data Through Pipelines*.

```
PS > Get-CronJob | Where-Object {$_.Month -match 'Jan'} | Format-Table -AutoSize 

Minute Hour DayOfMonth Month DayOfWeek Command
------ ---- ---------- ----- --------- -------
*/15 10-12 * Jan,Mar,Jun,Sep,Dec sun,tue,fri /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
*/15 10-12 * Jan,Mar sun,tue,fri /usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"
```

4.  Remove the entries using `Remove-CronJob`.

```
PS > Get-CronJob | Where-Object {$_.Month -match 'Jan'} | Remove-CronJob 

Confirm
Are you sure you want to perform this action?
Performing the operation "Remove" on target "/usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"".
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"): Y

Confirm
Are you sure you want to perform this action?
Performing the operation "Remove" on target "/usr/bin/pwsh -c "cd /tmp/; ./DataLoading.PS1;"".
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"): Y
PS /home/PacktPub> 
```

# How it works...

When we would like to remove cron jobs, we list out the cron jobs and then, pass the job objects via the pipeline to the cmdlet, `Remove-CronJob`, to remove the jobs from the configuration file.

# Passing Data through the Pipeline

In this chapter, we cover the following topics:

1.  Selecting columns from the output
2.  Limiting the number of items returned by a cmdlet
3.  Expanding selections
4.  Filtering objects
5.  Grouping the output
6.  Sorting the output
7.  Taking actions on the returned objects
8.  Understanding pipeline-enabled parameters
9.  Importing content into PowerShell

# Introduction

It is time for some information feasting now. In the previous chapter, *First Steps in Administration using PowerShell*, we looked at a few simple concepts such as working with dates and processes. In doing so, we learnt a thing or two about using PowerShell as well, for example, measuring the output objects.

In this chapter, we will learn to use one of those things that make PowerShell highly efficient and friendly: The Pipeline.

Most Linux administrators would have used the pipeline in their shell commands or shell scripts. And most administrators who use any form of shell scripting would be aware that the pipe sends the output of one command as input to the next. It is also true in case of Bash (and its derivatives) that the pipe sends *text* from the preceding command to the succeeding one.

Most PowerShell cmdlets output objects. And the pipeline in PowerShell sends the output *object* to the next command. When we run a PowerShell command (and not a Linux command) in PowerShell, we get a table-like output in most cases. We may think that it is all of the output.

When we ask PowerShell to get any information, it pulls out entire the object in the background. This object (or a package that contains a lot of objects) is then processed using PowerShell's built-in formatting rules in order for it to be displayed on the host. To quote Microsoft:

What you see onscreen is a summary of information, and not a complete representation of the output object.

Therefore, more often than not, what you see on the screen as the output of a certain command, is just a tip of the iceberg! Just that the *submerged* part was chosen not to be displayed based on the formatting rules. In this chapter, we will use the pipeline to get more from the objects, than is displayed on the screen by default, and leverage the capability of the pipeline to get more out of PowerShell than meets the eye.

# Selecting columns from the output

When my brother saw me exploring `awk`, he said, 'Boy, have we overused this command!' Of course, not everything displayed on the screen is important—or even necessary. In this recipe, we learn to separate the columns in PowerShell, without using the Linux command, `awk`.

# Getting Ready

Go to a directory that has some files that we can play with. If you do not have such a directory, create one and create some files in there. Let the files be of different extensions, so that we can use them in the future recipes as well.

If you have not already, clone the git repository, [https://github.com/PacktPublishing/PowerShell-6.0-Linux-Administration-Cookbook](https://github.com/PacktPublishing/PowerShell-6.0-Linux-Administration-Cookbook). There is a quick-and-dirty script, `Initialize-PacktPs6CoreLinuxLab.ps1` under the directory, `chapter-05`. Run the script to get the necessary files.

# How to do it...

The `awk` command works with text, and based on the delimiters in the output text, separates the output into columns. This separated output is displayed as columns again, using a the `print` function, like in C. PowerShell works a little differently.

Let us get started.

1.  If you did not create files, please do so. Here are some commands you could use to create the files.

```
PS> New-Item ./random/cities -ItemType Directory -Force
PS> Set-Location ./random/
PS> New-Item random-text.txt, himalayas.jpg, crunched-numbers.csv, bangalore.jpg, screenshot-001.png, screenshot-002.png, screenshot-003.png, demo.doc, my-plugin.rb, ./cities/mumbai.html, ./cities/nyc.html, ./cities/cairo.html, ./cities/dubai.html, ./cities/paris.html -ItemType File
```

2.  You may also want to download some real multimedia content, just so we get the `length` (file size) property for future use. Just download any random images or media files.
3.  Navigate to the location where you saved the files. I have them in a directory called `random` in my home directory. You would, too, if you used the script.

```
PS> Set-Location ./random/
```

Use tab-completion to complete the cmdlet as well as the path.

4.  List out the contents in the current location.

```
PS> Get-ChildItem -Path .
```

![](Images/fc1b8222-bc35-4723-bc80-b3c548ec789f.png)

5.  Let us say, you do not require the `Mode` column.

```
PS> Get-ChildItem -Path . | Select-Object LastWriteTime, Length, Name
```

![](Images/66a9b353-b59f-4822-9b84-ea92bae58933.png)If you notice, select does not seem to follow the naming or capitalisation convention that PowerShell uses. How is that? Run `Get-Command select` to find out.

6.  This sequence does not really make sense to you in the current context. Shuffle the columns.

```
PS> Get-ChildItem -Path . | Select-Object Name, Length, LastWriteTime
```

![](Images/3f839c8d-22b8-45c0-bbf9-913af8c94295.png)

That looks much better.

7.  Now, change the column name of `LastWriteTime` to `Modified`.

```
PS> Get-ChildItem -Path . | Select-Object Name, Length, @{Name='Modified'; Expression={$_.LastWriteTime}}
```

Notice the name of the last column now, and compare it with the previous output.

8.  Now, pick just the year; not the entire date.

```
PS> Get-ChildItem -Path . | Select-Object Name, Length, @{Name='Modified'; Expression={$_.LastWriteTime.Year}}
```

9.  See how many days have passed since the last change.

```
PS> Get-ChildItem -Path . | select Name, Length, @{Name='DaysSinceModification'; Expression={[math]::Round(((Get-Date) - $_.LastWriteTime).TotalDays)}}
```

# How it works...

If you ran `Get-Command select`, you would have understood by now, that `select` is in fact an alias for `Select-Object`. As already established, PowerShell outputs objects. These objects are then formatted using built-in formatting rules to show on the screen a certain way.

When we use the `Select-Object`, we override the formatting rules by specifying which objects need to be shown to us. While the primary objective of `Select-Object` is to pick the columns we need, the cmdlet also allows us to sequence the output columns.

PowerShell also gives us the freedom to modify the name of the columns returned. In such a case, we use a *hashtable* to specify the name that we want, and what data we want shown under the column. You can even perform calculations on the data returned, and make this a calculated property. At the last step, we subtract the date of last modification from the current date, pick the total number of days that have passed since, and then, use the `Round` method of the `[math]` accelerator to get a rounded figure of the number of days since the last modification.

The concept of `$_` or `$PSItem`.

# There's more...

Try `Select-Object` with other cmdlets such as `Get-Command`, to select only those columns that you need.

# See also

Recipe : Creating and initialising a simple hash table.

# Limiting the number of output objects

In the previous recipe, *Selecting columns from the output*, we saw how the `Select-Object` cmdlet can be used to select only the columns we want. In this recipe, we will learn to limit the output of a cmdlet to a subset of the total items returned.

# Getting ready

Ensure that you are at a location that has a few files. List out the contents of the current directory and count the number of items returned. If the number is less than five, you may want to consider adding more items to the directory.

1.  Enter the following command to count the number of files and directories at the current path.

```
PS> (Get-ChildItem -Path .).Count
```

2.  If you would like to reduce keystrokes, given that we are only running commands at the terminal, you could use the alias and the defaults of the cmdlet.

```
PS> (gci).Count
```

Those parentheses are required; the parentheses work almost similar to how they work in mathematics: the instruction within the parentheses is processed first. In this case, we want `gci` executed first, and then, the `Count` property from within the returned object picked.

3.  Get the list of parameters `Select-Object` has.

```
PS> Get-Help Select-Object
```

We see parameters like, `First` and `Last`, and they accept integer values.

# How to do it...

Navigate to the directory where you have the files.

1.  Select only the first five files and directories from the returned list, using the `First` parameter.

```
PS> Get-ChildItem . | Select-Object -First 5
```

2.  Let us say you would like to pick the last five elements.

```
PS> Get-ChildItem . | Select-Object -Last 5
```

3.  To skip the first three objects:

```
PS> Get-ChildItem . | Select-Object -Skip 3
```

4.  If you would like to skip the last two objects:

```
PS> Get-ChildItem . | Select-Object -SkipLast 2
```

5.  To pick the fourth element from the output:

```
PS> Get-ChildItem . | Select-Object -Index 3
```

6.  Now, combine it with what we learnt in the previous recipe. Pick only the file names and the last modified time of the first four elements.

```
PS> Get-ChildItem . | select -Property Name, LastWriteTime -First 4
```

# How it works...

This is a simple recipe that helps you work with the number of items returned in the output. With `Select-Object` in PowerShell, we need not loop through output, while simultaneously counting, to only get the number of elements that we want. The `Select-Object` cmdlet has that functionality built in.

The parameter names are self-explanatory. Except perhaps the `Index` parameter, which works exactly how numbering of array elements works with most programming languages: it starts with zero. Therefore, the fourth element in the array would have an index of `3`, and not `4`.

The parameters, `Property` and `First` can be combined together since they both feature in the same parameter set in the help documentation for `Select-Object`.

# Expanding the properties within properties

So far from what we have seen, two things are clear to us:

1.  An object output feels richer and makes using it easier.
2.  An object can have more objects within it.

We have handled the first point using the `Select-Object` cmdlet, wherein we picked only the objects properties that we needed, and omitted the rest. This recipe is designed to break down the second point for better understanding.

Let us step into this recipe with one thing in our mind: objects can contain objects within them, which in turn can contain more objects within them. To demonstrate this, we shall use the `Get-Process` cmdlet.

# How to do it...

Let us begin with listing out the processes; we shall look at all the properties the `Get-Process` cmdlet gives us and look for complex ones.

1.  Select all the properties that are part of the output of the `Get-Process` cmdlet. Pick only the first object, so your console is not filled with content.

```
PS> Get-Process | Select-Object -Property * -First 1
```

Observe the property, `Threads`.

2.  Select the name of the process, the ID and the threads.

```
PS> Get-Process | Select-Object -Property Name, Id, Threads
```

3.  List out all the threads for the `pwsh` process.

```
PS> Get-Process pwsh | Select-Object -ExpandProperty Threads
```

4.  A lot of content is output. Say, we want just the ID, the priority, and the start time of the resulting output.

```
PS> Get-Process pwsh | Select-Object -ExpandProperty Threads | Select-Object -Property Id, PriorityLevel, StartTime
```

This gave us the ID, the priority level and the start time of all the threads that are running under `pwsh`.

5.  What if we use `ExpandProperty` on the ID?

```
PS> Get-Process pwsh | Select-Object -ExpandProperty Threads | Select-Object -ExpandProperty Id
```

![](Images/9a082625-cdef-4a3d-ab7a-dc865b01364f.png)

# How it works...

The default parameter for `Select-Object`, as we have seen, is `Property`. It accepts property names and shows their values in the output. The parameter can be used to fetch values of multiple properties (`Name`, `Id`, `Threads`).

However, some properties have more complex objects within them, like how we saw in case of the `Threads` property of the object returned by `Get-Process`. A simple way to identify complex objects is to see if they are enclosed in curly braces.

The `ExpandProperty` parameter accepts only a single property name as input and expands the property to show its objects. This can again be piped to `Select-Object` (or any other relevant cmdlet) for further processing.

In cases where the object is not complex, `ExpandProperty` simply shows the output without its header. If you notice the output of `ExpandProperty`, it does not contain the name of the expanded object itself (`Threads` in our case); it contains only the value. The value, in turn has multiple properties within it.

In case of simple properties, using `ExpandProperty` simply strips off the property name from the output.

# Filtering objects

In the recipe, *Limit the number of items returned by a cmdlet*, we saw how to restrict the output content based on a number. In this recipe, we would look at filtering the output based on a certain criterion, and not a number.

# Getting ready

Go back to read the recipe, *Working with date properties*, if you have not read it already. This recipe uses one of the properties from the date object to filter content. While it is not critical to understand filtration of objects, it still demonstrates the simplicity of filtration based on object properties.

# How to do it...

Navigate to the location where you created files for use with this book.

1.  List out the contents of this directory to see what content you have. (If you are like me, you would have even forgotten where you created this directory, and what content you put in.)

```
PS> Set-Location ~/random
PS> Get-ChildItem -Path .
```

Notice the names of the properties you got.

2.  Now, pick only those files that are larger than `0` bytes.

```
PS> Get-ChildItem -Path . | Where-Object -Property Length -GT -Value 0
```

3.  Pick out all the JPG files from the lot. To do this, add another condition to the existing condition. Although, this time, use the `FilterScript` parameter instead of `Property`.

```
PS> Get-ChildItem -Path . | Where-Object -FilterScript {$_.Length -GT 0 -and $_.Extension -EQ '.jpg'}
```

4.  Add a condition to get only those files whose names start with 'c'.

```
PS> Get-ChildItem -Path . | Where-Object -FilterScript {$_.Length -GT 0 -and $_.Extension -EQ '.jpg' -and $_.Name -CMatch '^c'}
```

5.  Now, choose those files which were created before the 30th minute of any hour.

```
PS> Get-ChildItem -Path . | Where-Object -FilterScript {$_.Length -GT 0 -and $_.Extension -EQ '.jpg' -and $_.Name -CMatch '^c' -and $_.LastWriteTime.Minute -LT 30}
```

![](Images/b3ae5d4b-631d-4e62-9ee6-c0c105aebfb5.png)

# How it works...

Filtration of the output is very simple in PowerShell. Given that the content output is an object, we could simply use the properties from within the object for the filtration.

This recipe shows two modes of filtration:

1.  Using one property and comparing its value to the input,
2.  Using a filter script, that uses multiple values, and multiple conditions.

The `Property` parameter accepts only one property. A conditional operator and a value for comparison are added to the statement to filter the output.

The `FilterScript` parameter, on the other hand, can handle more complex filtration, for example, when we need the output to meet several conditions.

A significant difference between using `Property` and `FilterScript` is the use of the automatic variable, `$_`. This variable contains the *current object* in the pipeline. For example, in this recipe, we pass the object from `Get-ChildItem` to `Where-Object` through the pipeline. The automatic variable, `$_`, contains the object returned by `Get-ChildItem`, so that `Where-Object` can process it. `$_.LastWriteTime`, in this case, picks the `LastWriteTime` property from the object returned by `Get-ChildItem`.

Also, the `LastWriteTime` object is of type `System.DateTime` or `DateTime`. (Run `(Get-ChildItem .).LastWriteTime | Get-Member` to know more.) Therefore, it is possible to break it down further into days, hours, minutes, and so on, which is the reason, `$_.LastWriteTime.Minute` could be used for filtration.

# There's more...

Try out the `Where-Object` cmdlet on other outputs, such as that of `Get-Process`.

# Grouping the output

There are situations where we could group the objects that were output, so that we could handle each group better, or simply for a more organised output. In this recipe, we will look at passing the output of one cmdlet through the pipeline to Group-Object and group the output based on a property.

# How to do it...

To group objects based on a property, we use the `Get-ChildItem` cmdlet on the files that we created for use in this book.

1.  Navigate to the location where you created or downloaded the files.

```
PS> Set-Location ~/random
```

2.  List out only the files (exclude the directories).

```
PS> Get-ChildItem -Path . -File
```

Or use the *shorthand* version.

```
PS> gci -File
```

3.  Group the objects based on the extension.

```
PS> Get-ChildItem . -File | Group-Object Extension
```

4.  The shorthand version of this would be:

```
PS> gci -File | group Extension
```

![](Images/126cd1df-e553-47c3-becf-a56acb92fb78.png)

5.  Use the `Select-Object` cmdlet to only show the extension and the number of files in each extension.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension | Select-Object -Property Name, Count
```

6.  Is there a simpler way to do this?

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension -NoElement
```

7.  Now that we know how to handle grouping and expanded property selection, let us pick only the JPG files from the lot.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension | Where-Object Name -EQ .jpg | Select-Object -ExpandProperty Group
```

![](Images/f0b16425-bada-4fba-ad2d-f7c9a62124a9.png)

# How it works...

What we did in this recipe was certainly non-intuitive, considering we could use just `Where-Object` along with the `Get-ChildItem`. However, the intention of this recipe was to demonstrate the use of `Group-Object`. The `Group-Object` cmdlet creates groups based on the criteria we specify, and names the groups on the criteria. In our case, the criteria for grouping was the extension, and hence, the names of the groups were the extensions.

Each of these groups contains its elements, which are objects in themselves. If we simply want the count and the names of the groups, we use the `NoElement` parameter. If we want only the elements, we use the `ExpandProperty` parameter of the `Select-Object` cmdlet and expand all the elements. The elements thus expanded are the objects of the cmdlet preceding the `Group-Object` cmdlet (`Get-ChildItem` in our case).

If `Where-Object` and other cmdlets could do what `Group-Object` could in a complicated way, why have it in the first place? Read on until *Taking actions on the returned objects* to know more.

# There's more...

If you have gotten a hang of tab completion, you need not even select the properties that are not shown by default. All you have to do is type `Group-Object` after the pipe, add a space and press Tab; PowerShell will show you what objects are available to use for grouping. Try it with:

```
PS> Get-ChildItem . -File | Group-Object<Space><Tab>
```

# See also

Recipe 05.07: Taking actions on the returned objects 

# Sorting the output

It is time for another simple cmdlet, which would build towards the recipe, *Taking actions on the returned objects*. In this recipe, we will sort the output objects to meet our requirements.

# How to do it...

We will continue to use the directory and the files we created for the book. If all of your files are of zero bytes, download a few files with content. The file type does not matter.

1.  List out the files in the directory.

```
PS> Get-ChildItem -Path .
```

2.  Filter the output to have only files.

```
PS> Get-ChildItem -Path . -File
```

3.  Pipe the object to the `Sort-Object` cmdlet to sort the output based on the file size.

```
PS> Get-ChildItem -Path . -File | Sort-Object -Property Length
```

4.  The shorthand for the expression would be:

```
PS> gci . -File | sort Length
```

5.  Sort the files, the largest file to the smallest file.

```
PS> Get-ChildItem -Path . -File | Sort-Object -Property Length -Descending
```

6.  Pick the largest three files in the lot.

```
PS> Get-ChildItem -Path . -File | Sort-Object -Property Length -Descending -Top 3
```

7.  Create two files, and, using a text editor, add some content into both of them. (Or use the following script block to create some random text.)

```
PS> $($i = 0; while ($i -lt 520) {(-join ((65..90) + (97..122) | Get-Random -Count 8 | ForEach-Object {[char]$_})).ToString(); $i++}) -join ' ' | Out-File ./random-text-1.txt; Start-Sleep -Seconds 60; $($i = 0; while ($i -lt 500) {(-join ((65..90) + (97..122) | Get-Random -Count 8 | ForEach-Object {[char]$_})).ToString(); $i++}) -join ' ' | Out-File ./random-text-2.txt
```

8.  Now, sort the files in the directory, first, by size, and then, the name.

```
PS> Get-ChildItem -Path . -File | Sort-Object -Property Length, Name
```

Observe the output that you get.

9.  Sort the list in the descending order.

```
PS> Get-ChildItem -Path . -File | Sort-Object -Property Length, Name -Descending
```

![](Images/98feda49-fc08-4af2-8a63-c814f055239c.png)

# How it works...

This recipe is another demonstration of passing objects through the pipeline. In the help documentation for `Sort-Object`, we see a parameter called `InputObject`. This parameter is a generic term used in PowerShell for a parameter whose input comes through the pipeline.

`Sort-Object` accepts input from the pipeline, and sorts the content based on the property specified. If a property is not specified, the default property for the object output from the preceding command is used for sorting. If there are multiple properties are input, the sorting happens based on the order in which the properties are specified.

Sorting can happen in the ascending order (default), or the descending order.

# Taking actions on the returned objects

We have been using the pipeline throughout this chapter to perform various activities on the objects. We have been passing objects from one cmdlet to another, and in fact, taking actions on the objects being returned. This recipe, in the technical sense therefore, is nothing new. However, in order to get ourselves more comfortable using the pipeline, and to show that the pipeline is not just used for selection, filtration and sorting, we will use the pipeline to also perform some deletions.

# Getting Ready

If you do not have files within the demo directory that we created, please go ahead and create some files. Make sure some of the files have some content in them.

Let us say that you have been given a requirement. There is a certain team which would like the top two largest files of each type, deleted from a directory. If there is only one file of a certain type, that file has to be left alone.

# How to do it...

Here is an outline of the steps you would want to take:

1.  Get all the files at the path specified.
2.  Group the files by file type (extension).
3.  Filter out those groups that contain more than one item.
4.  Expand each group, sort the files by size (length).
5.  Pick the two largest files in each group.
6.  Delete the files.

While we are working on a sandbox directory, and that we are taking precautions not to delete anything important, it is still better to only prototype the action using ShouldPerform (the WhatIf parameter). This way, the files would not be actually deleted, but PowerShell would only tell you what it would do if the command is run.

Let us get cracking.

1.  List the contents of the current directory and group the output based on the extension.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension
```

2.  Filter to discard lone files of each extension.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension | Where-Object Count -GT 1
```

3.  Now comes a loop construct. We will look at how that works in a future chapter. For now, just know that it works. The goal here is to only leverage the pipeline.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension | Where-Object Count -GT 1 | ForEach-Object {$_.Group | Sort-Object Length -Bottom 2}
```

![](Images/c1ae6403-f6e6-48bf-a8cb-188092d3f16e.png)

4.  Delete these files using the `Remove-Item` cmdlet. Use the `WhatIf` switch if you do not want the files actually deleted.

```
PS> Get-ChildItem -Path . -File | Group-Object -Property Extension | Where-Object Count -GT 1 | ForEach-Object {$_.Group | Sort-Object Length -Bottom 2} | Remove-Item -WhatIf
```

# How it works...

When any cmdlet reads an object through the pipeline, it reads the entire contents of the object. And any cmdlet that is designed to accept input through the pipeline picks the right property from the object, and then takes actions on the objects. In the case of this recipe, it was the `Path` property that was picked in order to identify the files to delete.

To know if a certain cmdlet accepts input from the pipeline, run `Get-Help` on the cmdlet with the `Full` parameter, and see if the value for `Accept pipeline input?` is true. The `InputObject` parameter of `Where-Object`, or the `Path` parameter of `Move-Item` are a couple of examples.

# Understanding pipeline-enabled parameters

Understanding pipelines is not so much of a requirement if you plan to use PowerShell for only running commands on the console; it is well encapsulated, and the cmdlets are well designed to be able to handle passing objects between cmdlets. However, if you plan to create custom functions and modules, the concept of the pipeline is something you would want to understand well.

In this recipe, we will look into the two ways cmdlets accept input. At the point where we create functions, we will look at how to enable pipeline input for parameters.

# How to do it...

We will mostly use the help documentation to demonstrate the two different kinds of pipeline input.

1.  At the prompt, type the following command:

```
PS> Get-Help Get-Item -Parameter Path
```

![](Images/ece35564-34f0-4beb-a575-83b29dc0208e.png)

It says the parameter accepts string input, and accepts input by property name as well as by value.

2.  Type the following to see if a valid string is accepted.

```
PS> '/home/ram/random' | Get-Item
```

![](Images/2f9fadc6-7b06-4d05-a0f3-3232e4d88ab8.png)

3.  Let us try something similar with `Get-Date`.

```
PS> Get-Help Get-Date -Parameter *
```

The Date parameter accepts values through the pipeline. However, the type is DateTime, and not string.

4.  Try sending a valid string through the pipeline to see if it gets converted into date.

```
PS> '21 June 2018' |  Get-Date
```

It did convert the string into date and time.

![](Images/9bf14887-e102-4518-aba5-ef0f00939e1d.png)

5.  Now, let us go back to getting details of the current directory. This time, however, we would pick only the FullName property of the object.

```
PS> Get-Item . | Select-Object FullName
```

6.  Pass this through the pipeline to the `Get-ChildItem` cmdlet.

```
PS> Get-Item . | Select-Object FullName | Get-ChildItem
```

There is an error.

![](Images/4b9eb33e-158a-47c3-91fa-81c8373590b4.png)

7.  Change the property name to `LiteralPath`.

```
PS> Get-Item . | Select-Object @{Name = 'LiteralPath'; Expression = {$_.FullName}}
```

8.  Pass the object to `Get-ChildItem` through the pipeline.

```
PS> Get-Item . | Select-Object @{Name = 'LiteralPath'; Expression = {$_.FullName}} | Get-ChildItem
```

That worked.

# How it works...

There are two kinds of input through the pipeline:

1.  `ByPropertyName`
2.  `ByValue`

The `ByValue` type is perhaps the most common. If a parameter accepts input through the pipeline by value, it would look for the data type that matches the defined data type in the output, and pick the output as input for itself. In case the data type is not the same as that defined, but can be converted to the required type, the parameter would convert the value into the data type it takes in, and processes it. This happened in the case of `Get-Date`, where we sent the date as a string, and passed it through the pipeline to `Get-Date`.

In case of `Get-Item`, the `Path` parameter accepted string input and processed the command. In case of `Get-Date`, the `Date` parameter converted the string into a `DateTime` object and processed the request.

`ByPropertyName`, as compared to `ByValue`, looks for a property of the *exact same name* as the parameter. In our case, `LiteralPath` of `Get-ChildItem` threw an error when we passed the `FullName` property, even though it was essentially the literal path of the object, and a string value. The reason for the error was that the property was not called `LiteralPath`. When we changed the name of the property to `LiteralPath`, `Get-ChildItem` accepted the input through the pipeline, and gave us the desired output.

# Importing content into PowerShell

Administrators managing multiple computers need to have some sort of input fed into cmdlets so they can automate tasks. While most Linux administrators are familiar with sending input to files, the important point with PowerShell is that apart from taking file-based input (read: `Get-Content`),  PowerShell is also capable of *importing* input. This imported input is a PowerShell object.

In this recipe, we will look at two kinds of import cmdlets and learn to work with them.

# How to do it...

In the recipe, *Parsing input from text to object*, we used `Import-Csv` to import a comma-separated values file to convert the data contained within to a PowerShell object. Let us recapitulate what we learnt, however this time, now that we know how to work with objects, we will use the imported content in some way.

Before we import content, let us first export some content into a CSV file. This way, we would have some relevant content to manipulate.

1.  Navigate to the location where you created files for this chapter. List the contents of the directory. While the book uses (and recommends) complete cmdlets even at the console (using tab-completion of course), feel free to use aliases if you want.

```
PS> Get-ChildItem -Path . | Select-Object Name, FullName, CreationTime, LastWriteTime, Extension, Length
```

2.  Export the contents to a CSV file.

```
PS> Get-ChildItem -Path . | Select-Object Name, FullName, CreationTime, LastWriteTime, Extension, Length | Export-Csv ./file-list.csv
```

3.  Open the file in a spreadsheet processor like LibreOffice Calc or even a text editor to view its contents.

```
PS> Get-Content ./file-list.csv
```

That was a plain text representation of the object returned by `Get-ChildItem.`

4.  Import the contents of the CSV file to convert this text into an object.

```
PS> Import-Csv ./file-list.csv
```

5.  Find the type of the object returned by this command.

```
PS> Import-Csv ./file-list.csv | Get-Member
```

The object type is `System.Management.Automation.PSCustomObject`.

6.  Check if this is the same as that returned by `Get-ChildItem`.

```
PS> Get-ChildItem . | Get-Member
```

7.  The object returned by `Import-Csv` is different. Is it possible to treat it just like we do other objects? Get the `CreationTime` using the member access operator.

```
PS> (Import-Csv ./file-list.csv).CreationTime
```

8.  Get just the year.

```
PS> (Import-Csv ./file-list.csv).CreationTime.Year
```

9.  Find the type of object returned by the last command.

```
PS> (Import-Csv ./file-list.csv).CreationTime | Get-Member

    TypeName: System.String
```

10.  Attempt to convert the `LastWriteTime` into a `DateTime` object. Pick just the first record, though.

```
PS> Get-Date (Import-Csv ./file-list.csv | Select-Object CreationTime -First 1).CreationTime
```

11.  What if we had to retain all the objects within the object returned by `Get-ChildItem`, including their object types?

```
PS> Get-ChildItem -Path . | Export-Clixml ./file-list.xml
```

12.  Now, import the contents of the XML to the session.

```
PS> Import-Clixml ./file-list.xml
```

13.  Find out the type name of the object returned by the import command.

```
PS> Import-Clixml ./file-list.xml | Get-Member
```

14.  Pick the `CreationTime` property and find its type.

```
PS> (Import-Clixml ./file-list.xml).CreationTime | Get-Member

    TypeName: System.DateTime
```

15.  Pick just the year.

```
PS> (Import-Clixml ./file-list.xml).CreationTime.Year
```

# How it works...

Importing content from a CSV is a straightforward process. The columns in a CSV are separated by commas. PowerShell creates an object from the input content, with each column making a property of a PowerShell custom object. Operations that we perform on objects can be performed on the `PSCustomObject`, however, the only limitation with `Import-Csv` is that the properties cannot be multi-valued, nor can they have other sub-properties within them. There could be ways to achieve multi-valued properties with CSV, but they would involve some manipulation after the object is imported within PowerShell. One such way is to separate the values of the property with a delimiter, and then, after the import, split the delimited value.

On the other hand, a CLIXML (or a Common Language Infrastructure XML) is a complete .NET object. When a PowerShell object is exported to CLIXML, the object is retained as it is. That is, the CLIXML retains all the properties (of theoretically any depth), and the methods that were part of the output object. In other words, it can be said that a CLIXML export is almost lossless in terms of the members of the object.

# See also

Recipe: Generate random text using ASCII characters

# Using Variables and Objects

In this chapter, we are discussing the following topics:

1.  Using environment variables
2.  Storing the output of an instance of a .NET Core object
3.  Creating custom properties to an object
4.  Creating a custom object from a returned object
5.  Understanding extension of type data
6.  Retaining object modifications across sessions
7.  Removing custom type data

# Introduction

Variables are important to programming since they act as containers of information stored during the program execution. Although piping makes PowerShell highly versatile, they still cannot replace variables, because objects passed through the pipeline must be consumed immediately, and not all scripts work that way, given our varied requirements.

We are all aware of the various data types: `int`, `double`, `string`, `char`, `array`, etc. Two other important types of variables in PowerShell are *hashtables* and *objects*. A hashtable is a dictionary table formed with key–value pairs. An object, as we have seen, could be as complex and as simple as it can get in PowerShell, holding values of different kinds.

In PowerShell, objects can be stored into variables. For instance,

```
$Processes = Get-Process
```

would store all the processes into the variable, `$Processes`.

One more point to remember with variables is the scope. By default, variables have a local scope, meaning, they are valid within the function that they are specified in. Global variables are valid across the program. In general, it is a best practice to use local variables, though.

Global variables are declared and used with the `$Global:` prefix, such as `$Global:MyVariable`.

# Using environment variables 

In this recipe, you will learn about environment variables. When interacting with the system through a shell session, there are many pieces of information that the Shell requires in order to determine the program access, the available resources, default configuration, system properties, etc. Some of these settings are configured within the system as variables and these settings are commonly called the *EnvironmentVariables*.

While hard-coding this information during installation is one way to go, it makes the entire system a monolith that cannot be reconfigured without what is known as nuking-and-paving. With environment variables, another layer of flexibility is introduced.

# How to do it...

Let us start working with an environment variable using the following steps:

1.  To Display environment variable, type in `Get-ChildItem env:` or `Get-Item env:` and press enter

```
PS> Get-ChildItem env:
PS> Get-Item env:
```

2.  `Env:` is also a PowerShell provider, and works just like a file system. Therefore, you could also `Set-Location` at `Env:` and use `Get-ChildItem .` to list out the variables available in your system.
3.  To display the value of the specific environment variable, run the following command.

```
PS> Get-ChildItem Env:/PATH | Select-Object value | Format-Table -Wrap
```

After typing `Get-ChildItem Env:/`,  You can use tab-completion to populate all environment variables. 

4.  Do a `Get-Member` on the `PATH` environment variable to find its type.
5.  Before changing the environment variable, list the `PATH` variable using `$env:PATH | Get-Member`. It is a string. Save the contents someplace safe.
6.  Now, update the `PATH` environment variable by adding the path of `sqlcmd` tool executable to $`env: PATH` variable. The operation is a simple addition of a string to the existing value.

You could add any location to `PATH`. If you insist on getting `sqlcmd`, head over to [Microsoft docs](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?view=sql-server-linux-2017) for SQL Server 2017 for instructions to get yourself a copy.

```
PS> $env:PATH = $env:PATH + ':/opt/mssql-tools/bin'
PS /root> sqlcmd
```

The output of the preceding code block is illustrated in the following image:

![](Images/1e6b48cb-4403-4d84-aac1-56e43f0a78b9.png)

7.  Let us exit the session, launch a new session,  check the `PATH` variable, and run the `sqlcmd` executable.

```
PS> sqlcmd 

sqlcmd : The term 'sqlcmd' is not recognized as the name of a cmdlet, function, script file, or operable program.
```

# How it works...

As we saw in *Listing the various providers in PowerShell*, `Env` is a provider that contains environment-specific configuration. Most of these configuration options are also exposed to us as environment variables. We are able to use the cmdlets `Get-ChildItem` and `Get-Item` to list the values of the available environment variables because `Env:` is a drive within the `Env` provider. As environment variables do not have child items, `Get-Item` and `Get-ChildItem` return the same output.

Since these variables determine how your session behaves with you, changes made to these values are ephemeral. In other words, the value of `$env:PATH` is picked from the configuration on your Linux computer. The manual change made to `$env:PATH` made within a PowerShell session remains as long as the PowerShell session is alive. Changes made to $env:PATH does not change the value within the system itself.

If you would like to make a certain change permanent, edit the `.bashrc` or the **`~/.bash_profile` **configuration files. If you would like to use PowerShell instead of Bash, make the change in your PowerShell profile. Instructions on how to do that can be found in the recipe, *Enabling automated execution of commands for each load*, in the chapter, *Preparing for Administration using PowerShell*.

# There's more...

You can also access environment variables using  .NET type accelerator and its methods.

```
PS> [environment]::GetEnvironmentVariable("PATH")
```

# See also

1.  About Environment variables: `Get-Help about_Environment_Variables`
2.  Recipe 1.11: Listing the various providers in PowerShell
3.  Recipe 3.4: Enabling automated execution of commands for each load

# Storing the output of an instance of a .NET Core Object

.NET is object-oriented, and works on classes and objects. PowerShell, being an extension to this framework, allows you to work with the .NET framework and COM interfaces in order to perform many system administration tasks. This way, you are not limited only to the tasks that can be performed using cmdlets.

In this recipe, we will define a simple class from within PowerShell.

# Getting Ready

We recommend using Visual Studio Code for this recipe. To know how to install and configure it, visit the recipe, *Installing Visual Studio Code* from the chapter, *Preparing for Administration using PowerShell*.

# How to do it...

Launch Visual Studio Code and address any immediate requirements it asks for.

1.  Open a new file in Visual Studio Code and set the file type as PowerShell.
2.  Type in the following in the script pane. The file does not have to be saved.

```
class Person {
    [string]$Name
    [Int32]$Age
    [int32]$Salary

    Person () {}

    Person ([string]$Name, [int32]$Age) {
        $this.Name = $Name
        $this.Age = $Age
    }

    [int32] sal ([int32]$Salary, [int32]$Comm) {
        return $Salary * $Comm
    }
}
```

3.  To find constructors of a class, call the static method, `New`; type in the following at the prompt.

```
PS> [Person]::New
```

4.  This gives us two functions of the same name; these are overload definitions. Now, create a new object by passing in the parameters.

```
PS> [Person]::New('Prashanth',34) 
```

![](Images/6134d77a-3052-4d39-b0ba-c260b5982fd6.png)

5.  Now, let us invoke the constructor the PowerShell way, which in turn calls the .NET constructor. This creates an instance of the Person class (which, by definition, is an object).

```
PS> $Person = New-Object -TypeName Person -ArgumentList 'Prashanth', 34
```

6.  To list the properties of the object (and by extension, the class), run the `Get-Member` cmdlet.

```
PS> $Person | Get-Member 

PS> $Person | Select-Object Name, Age, Salary | Format-Table -AutoSize 

PS> $Person.sal(200,2)
```

![](Images/8daf5696-50c8-40ac-b1f9-a9114d7c13b9.png)

7.  Next, Let us take a look at the other samples. Let us use system-defined class libraries.

```
PS> $MailClient = New-Object -TypeName System.Net.Mail.SmtpClient 'packtpub.smtpdomain.com'
PS> $Message = New-Object System.Net.Mail.MailMessage('pjayaram@packtpub.com', 'pjayaram@packtpub.com', 'Subject', 'Welcome to Packt!')
PS> $MailClient.Send($Message)
```

8.  Let us see another example of password encryption using `System.Management.Automation` class objects.

```
PS> $User = 'Prashanth' 
PS> $Password = 'Y94b^E$85CBLU%at' 
PS> $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force 
PS> $Credentials = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $SecurePassword 
PS> $Credentials | Get-Member
```

![](Images/6cb687d1-a002-45c1-917f-d2a18d39014e.png)

# How it works...

The goal of this recipe is to demonstrate how PowerShell works hand-in-hand with .NET, and objects that are created the *.NET way* can be called (and stored) easily in PowerShell. First, we declare a class with the keyword, `class`. We then declare its parameters, and then, create two constructors: one default and one parameterised.

We also create a method called `sal`. We define its return type as `int32`, and defined two parameters. Within it, we define what needs to be returned.

Back at the PowerShell prompt, we call the static (method of the class, not of an object) `New` method. The syntax is to mention the class name, followed by two consecutive colons (`::`) to call it in the global namespace, followed by the name of the method.

If you follow the steps, you'll also see an example of using the two different system class libraries, `System.Net.Mail.SmtpClient` and `System.Net.Mail.MailMessage`, and the instantiation of a method by integrating the output of mail-message with the SMTP-client object.

Next, we use the system class library `System.Management.Automation.PSCredential`. In this example, we send some text to `ConvertTo-SecureString` which takes input as plain text and converts it to a secure string. Then, we pass the encrypted string to the `PSCrendital` system class to store the user name and the secure string into the `$Credentials` variable. 

# See also

1.  Recipe 3.1: Installing Visual Studio Code

# Adding custom properties to an object

PowerShell cmdlets are capable of allowing the administrators to work with most tasks. However, there are some situations where the returned objects don't satisfy the administrative needs of a certain script. In such situations, we may need to create our own custom objects based on the available .NET classes, or at least, add a custom property to the object.

While a string is an object of `System. String` type, the `Get-Process` cmdlet returns an object of type `System.Diagnostics.Process`, `Get-ChildItem` returns an object with the type `System.IO.FileInfo`, a custom-created object has the object type, `PSCustomObject`.

# How to do it...

Let us now proceed to create a custom object.

1.  To create a custom object, use `New-Object` cmdlet. 

```
PS /home/PacktPub> New-Object -TypeName PSCustomObject
```

2.  That was not of much use to us. Let us add a few properties into it, along with their values and store these values in a variable.

```
PS> $MyCustomObject = [pscustomobject]@{ 
  Name = 'Prashanth Jayaram'
  Title = 'PowerShell'
  Publisher = 'Packt' 
}

PS> $MyCustomObject
```

3.  To add properties to an object, use the `Add-Member` cmdlet.

```
PS> $MyCustomObject | Add-Member -MemberType NoteProperty -Name 'Location' -Value 'United States'
PS> $MyCustomObject
```

4.  To remove a property from an object, use the following command.

```
PS> $MyCustomObject.PsObject.Properties.Remove('Location')

PS> # To see if the property is still available, run:
PS> $MyCustomObject.Location
```

5.  To access properties, you can use the member access operator (`.`).

```
PS> $MyCustomObject.Name 
Prashanth Jayaram

PS> $MyCustomObject.Title 
PowerShell

PS> $MyCustomObject.Publication 
Packt
```

# How it works...

Creating an object is straightforward. All you have to do is tell PowerShell that you are creating a custom object, by calling the `[psobject]` accelerator and specifying the properties you would like to add to the object. After the accelerator is called, we specify the names of the properties, and assign values to them. Records are added one at a time, using the hash literal notation (`Name = 'Prashanth'`).

It is easy to confuse a hashtable with a PSObject at this stage, given that we use the hash literal notation when creating the object. Remember that they are very different from each other. We will get into the details of what a hashtable is in the chapter, *Arrays and Hashtables*.

We mention three properties in the custom object we have created: `Name`, `Title` and `Publisher`. If we would like to add additional properties in the future, we can simply use the `Add-Member` cmdlet, where we specify the object (we pass the object through the pipeline), we specify the name of the property, and assign a value to it.

Removing a property is a little more complex, since we do not have a `Remove-Member` cmdlet, nor are the members we use in the step easily discoverable. For instance, `[PSCustomObject] | Get-Member` does not reveal `PsObject` being its member. We call the `Remove` method within the `Properties` object, which is within the `PSObject` object of the custom object we created. (So many objects!)

Accessing properties in an object is as simple as using the member access operator with the property name.

# See also

1.  Recipe: Creating and initialising a simple hashtable

# Creating a custom object from a returned object

We now know how to create a custom object from scratch. In this recipe, we will use a returned object, and modify the returned object to create a custom object. When we look at loops, we will extend this capability to create versatile custom objects; in production environments, this capability can be used to do more!

# How to do it...

The first step to learning something is to simplify it. Therefore, we will select only one instance of an object and work with it.

1.  Get all the processes, select only the name, ID, working set and the start time, pick the 5th process in the list, and assign it to a variable.

```
PS> $Process = (Get-Process | Select-Object Name, Id, WS, StartTime)[4]
```

2.  Let us say that we did not like the names of the properties in the object. Let us change the names.

```
PS> $CustomProcess = New-Object -TypeName PSObject -Property @{
  ProcessName = $Process.Name
  ProcessId = $Process.Id
  WorkingSet = $Process.WS
  StartedAt = $Process.StartTime
}
PS> $CustomProcess
```

![](Images/a42cf4a5-4cb5-4112-9157-fd017a8d4192.png)

3.  But that is not the sequence we specified. Let us get them in sequence.

```
PS> $CustomProcess = [ordered]@{
  ProcessName = $Process.Name
  ProcessId = $Process.Id
  WorkingSet = $Process.WS
  StartedAt = $Process.StartTime
} 
PS> New-Object -TypeName PSObject -Property $CustomProcess
```

![](Images/609d4d23-847e-4300-9453-0071a046f302.png)

4.  Recreate the object with information on how long the process has been running for instead of when it was started.

```
PS> $CustomProcess = [ordered]@{
  ProcessName = $Process.Name
  ProcessId = $Process.Id
  WorkingSet = $Process.WS
  RunningMins = [math]::Floor(((Get-Date) - $Process.StartTime).TotalMinutes)
}
PS> New-Object -TypeName PsObject -Property $CustomProcess
```

![](Images/9708bd11-619f-45c9-8842-7aac2c1ac587.png)

# How it works...

In this recipe, we created a custom object (`$CustomProcess`) from an output object (`$Process`). The properties within `$Process` can be accessed using the member access operator. Values from `$Process` are treated as values for the properties in `$CustomObject`, however, the names in `$CustomObject` are different. In this recipe, we also used a calculated property, `RunningMins`.

An important point to note here is that the outcome of this recipe can also be achieved using calculated properties along with `Select-Object`. However, in situations where object versatility is important and the number of instances of the objects is significantly larger, it is simpler to use a custom object. We will extend this capability in future chapters, after we learn to use looping constructs.

The other point to note is the use of the `[ordered]` accelerator. More often than not, the properties of custom objects do not appear in the sequence we mention them in. In this recipe, we separate the hash literal notation from the creation of the custom object. We first create an ordered hashtable with the property names as well as the property values, and then, specify the created hashtable for the `Property` parameter of the `New-Object` cmdlet to create the custom object with the properties showing in the sequence we want.

# See also

1.  [Creating .NET and COM Objects](https://docs.microsoft.com/en-us/powershell/scripting/getting-started/cookbooks/creating-.net-and-com-objects--new-object-?view=powershell-6) (Microsoft Docs)

# Understanding extension of Type Data

In the recipe, *Selecting columns from the output*, we used a hashtable to set the name and the expression for a custom-named column. Later, we also used a small calculation within the `Select-Object` statement to get a calculated output. If you tried to select the column by the new name, that would have worked, too. Technically, you have already extended the object. But what is type data anyway? And why do we need a recipe to extend it when we can work with `Select-Object`?

Going too deep into what type data is and how to work with them along with .NET classes and objects could potentially make the concept an "advanced" one. Historically, most of us learners have procrastinated learning "advanced" topics. Therefore, we will stick to the simple parts of it, and work only with PowerShell for now. This recipe will serve as a launchpad to help you understand what it is by making it simple and fun, keeping it away from anything "advanced", in the interest of learning.

There are two options to extend the type data:

1.  Using PowerShell cmdlets (to understand how it all works)
2.  Using an XML file (for portability)

# Getting ready

To understand what we are talking about, here, you need to have read the following recipes:

1.  Selecting columns from the output
2.  Creating a custom object from a returned object

Let us come back to the question: Why extend type data when we can use `Select-Object`?

Efficiency. While you could change the name, add a calculation, and reference the calculated property with the new name, that change would have existed only in that context. If you added it to a variable,  as in the last recipe, *Creating a custom object from a returned object*, where we did some nifty changes to the names and also created a custom `NoteProperty`, that would be a long way to go about it. Enter: extension of type data.

The rule of the thumb is,  If you do something repetitively, there's an issue: you haven't considered automating it. For example,  if you run:

```
PS> Get-ChildItem -Path . | select Name, Length, @{Name='Age'; Expression={[math]::Round(((Get-Date) - $_.LastWriteTime).TotalDays)}}
```

instead of:

```
PS> Get-ChildItem -Path . | select Name, Length, Age
```

and you do it fifteen times a day, you should consider extending the object to give you what you care about.

# How to do it...

Navigate to the location where you created files for lab usage.

1.  Enter the following command:

```
PS> $FilesWithAge = Get-ChildItem . | Select-Object Name, Length, LastWriteTime
```

2.  Now, add a property to the variable, `$FilesWithAge`; the property should be the age of each file, in days.

```
PS> $FilesWithAge | Add-Member -MemberType ScriptProperty -Name Age -Value { [math]::Round(((Get-Date) - $this.LastWriteTime).TotalDays) }
```

3.  Add another property to it, called `ComputerName`, which is the name of your local host.

```
PS> $ComputerName = hostname
PS> $FilesWithAge | Add-Member -MemberType NoteProperty -Name ComputerName -Value $ComputerName
```

4.  Add another property, as an alias to `LastWriteTime`, called `Modified`.

```
PS> $FilesWithAge | Add-Member -MemberType AliasProperty -Name Modified -Value LastWriteTime
```

5.  To format it like a nice table, use the following:

```
PS> $FilesWithAge | Format-Table -AutoSize
```

![](Images/8be1b9ba-03be-4dd0-825e-63cb802c0205.png)

6.  Now, delete the variable. And query the files within the current directory (because that is what the variable actually held).

```
PS> Remove-Variable FilesWithAge
PS> Get-ChildItem .
```

You do not see the `Age`, the `ComputerName` or the `Modified` properties. Try `Get-Member` if you would like.

Next, we see how to extend the type data itself, so that every time you run `Get-ChildItem`, you also get the three properties we added to the variable.

7.  Get what object is returned when you run `Get-ChildItem`.

```
PS> Get-ChildItem | Get-Member
```

8.  You get `System.IO.DirectoryInfo` as well as `System.IO.FileInfo`. We pick `System.IO.FileInfo`. Run the following commands.

```
PS> $ComputerName = hostname 

PS> Update-TypeData -TypeName System.IO.FileInfo -MemberType NoteProperty -MemberName ComputerName -Value $ComputerName

PS> Update-TypeData -TypeName System.IO.FileInfo -MemberType AliasProperty -MemberName Modified -Value LastWriteTime

PS> Update-TypeData -TypeName System.IO.FileInfo -MemberType ScriptProperty -MemberName Age -Value { [math]::Round(((Get-Date) - $this.LastWriteTime).TotalDays) } 
```

9.  Query the contents of the current location and optionally, format the output like a table.

```
PS> Get-ChildItem . | Select-Object Name, Length, ComputerName, Age, Modified | Format-Table -AutoSize
```

![](Images/c5b3b81f-1763-4c48-8193-e924941e8b58.png)

10.  Do the same for any directory in the file system, the only condition being that the directory should contain at least one file, and not just more directories.

```
PS> Get-ChildItem ./cities/ | Select-Object Name, Length, ComputerName, Age, Modified | Format-Table -AutoSize
```

# How it works...

In the first section, we added members to the objects within a certain variable. This was a command-line-prompt-style extension to the recipe, *Creating a custom object from a returned object*, which was, by all means, a little more efficient in the context. However, the changes we made to the object remained only while the variable, `$FilesWithAge`, was valid. The object returned by `Get-ChildItem` was not modified at all.

There is an important point to note here: `$this`. We have come across the automatic variable, `$_` (or `$PSItem` after PowerShell V3) when dealing with objects passed through the pipeline; the variable holds the current instance of the object in the pipeline. However, when we have to perform an object extension, we use the automatic variable, `$this`. Why? Because, the property being referred to is being referred *within* the parent object (the object returned by `Get-ChildItem`). External methods would be able to use `$_`. In a way, `$_` does not even exist yet, when performing the member addition. Also, `$this` in fact, refers to the object itself, that is returned by `Get-ChildItem`, and not just an instance of it.

When we would like to get a member as part of the object itself, throughout the session, irrespective of the validity of a certain variable or the object instance, we *extend the type data itself*. Therefore, no matter what context you run the cmdlet in, you would get the additional members you added. Of course, the formatting rules in PowerShell may still not let those members appear in the output by default. You can always call the specific members, though, such as using `Select-Object` for properties, or simply using the member access operator on the properties: `(Get-ChildItem .).Age`.

For this, we use the `Update-TypeData` cmdlet. `Update-TypeData`, in this context, requires the `TypeName`, which as we have already seen, can be determined using `Get-Member` on the returned object.

We mention four things in the `Update-TypeData` statements: 

1.  The type name
2.  The member type
3.  The member name
4.  The member value

Member type accepts several values, of which we use three:

1.  `AliasProperty`, which is simply a reference to another member within the object. The new property is just another name to an existing property. Therefore, the `Value` parameter can just take the name of the existing member.
2.  `NoteProperty`, which is a static value. In our case, we can use the host name as the static value.
3.  `ScriptProperty`, which is essentially a calculation. We calculate the time span between the date when it was last modified and the current date. This calculation is the `Value` for the member, and accepts a script block.

This modification to the object would be valid as long as the session is valid; the change is not persistent across sessions. That brings us to the next recipe, making object modifications stick across sessions.

# See also

1.  Recipe 5.1: Selecting columns from the output

# Retaining object modifications across sessions

In the previous recipe, Understanding extension of Type Data, we used the `Update-TypeData` cmdlet to add members. However, we said that the update was valid as long as the session was. Now, there could be two ways by which to make the type data stick across sessions:

1.  Using the PowerShell profile.
2.  Using an XML file

PowerShell profile is straightforward. However, usually, the type data extension and formatting rules are packaged as part of PowerShell modules. And adding code to the profile is not particularly helpful in that case. In this recipe, we will write a simple XML (`.ps1xml`) file that we will load in order to extend the type data.

# Getting Ready

Restart your PowerShell session so that the custom data type extension is discarded.

# How to do it...

We need an XML file. You can either use the `New-Item` cmdlet to create one, or simply use your favourite text editor. We use Visual Studio Code for this recipe. 

1.  Open your text editor and create a new empty file, and save it as `CustomTypes.ps1xml`.
2.  Add the following content to the XML file. Ensure not to change the case.

```
<?xml version="1.0" encoding="utf-8" ?>
<Types>
 <Type>
   <Name>System.IO.FileInfo</Name>
   <Members>
     <AliasProperty>
       <Name>Modified</Name>
       <ReferencedMemberName>LastWriteTime</ReferencedMemberName>
     </AliasProperty>
     <ScriptProperty>
       <Name>Age</Name>
       <GetScriptBlock>[math]::Round(((Get-Date) - $this.LastWriteTime).TotalDays)</GetScriptBlock>
     </ScriptProperty>
     <NoteProperty>
       <Name>ItemType</Name>
       <Value>File</Value>
     </NoteProperty>
   </Members>
 </Type>
</Types>
```

3.  Save the file at a convenient location.
4.  Back at the Terminal (or the PowerShell Integrated Console), enter the following command to update the type data using the XML. Notice the `PrependPath` parameter.

```
PS> Update-TypeData -PrependPath ~/Documents/code/github/powershell/chapter-06/CustomTypes.ps1xml
```

5.  Now, list out all the files within any directory of your choice.

```
Get-ChildItem . -File | Select-Object Name, Length, Age, Modified
```

You should see the new properties that you created.

![](Images/fc352f31-1676-4f6f-b492-31380f2aa080.png)It is advised to never modify the PS1XML files in the `$PSHome` directory. They are digitally signed by Microsoft and could be replaced with new versions during upgrades or patches.

# How it works...

Custom types and formats are mostly used while creating custom modules. Rarely do administrators require modifying the types or formats for stock PowerShell modules. And when you do require modifying custom types or formats, create a new PS1XML; do not modify the stock files, since they are digitally signed, and modifying them would break your setup.

Think of this PS1XML file as a regular XML file. Here is a simpler way of showing the structure. Remember that each type and each of the members within, must have a name.

```
Types
-- Type
---- Members
------ [The custom properties and methods you define]
```

In essence, using the XML for type extension is not very different from how we performed type extension in the last recipe, except this uses an XML file, which makes the setup more portable. When we work on creating our custom modules, we will look at packaging the types along with the modules, and at that time, we will look in detail, how to work the paths. For now, we load the XML by manually specifying the exact path to the file. If you would like to load these custom types for every session of yours, you can easily call the PS1XML from your profile. The portability aspect here is that the XML can easily be shared or deployed; only the loading would be manual, or through the profile—much simpler than adding cmdlets to profiles.

When updating the type data using cmdlets, we used the parameters `Name` as well as `Value`, along with the `MemberType` parameter. PowerShell understood the context and set up the types accordingly. In case of XML, though, one must remember to use the correct tags for each of the member types. For instance, for `AliasProperty`, the tags within should be `Name` and `ReferencedMemberName` (shown below); for `ScriptProperty`, they should be `Name` and `GetScriptBlock`; for a `NoteProperty`, the tags would be `Name` and `Value`.

```
<AliasProperty>
   <Name>Modified</Name>
   <ReferencedMemberName>LastWriteTime</ReferencedMemberName>
</AliasProperty>
```

Also, remember *not* to enclose the entire script block in braces when placing the statement within the `GetScriptBlock` tag:

```
<GetScriptBlock>
 [math]::Round(((Get-Date) - $this.LastWriteTime).TotalDays)
</GetScriptBlock>
```

and not:

```
<GetScriptBlock>
 { [math]::Round(((Get-Date) - $this.LastWriteTime).TotalDays) }
</GetScriptBlock>
```

When loading the XML, we use the `PrependPath` parameter to load our XML *before* the built-in types are loaded. To load them after the built-in types, there is no need to use the `AppendPath` parameter, unless the situation really needs it, since `AppendPath` is the default. Why do the parameters matter? They determine the precedence of loading the types.

The XML file shown may *look like* having a large number of items. Use the indent guide in Visual Studio Code to guide you through reading the XML. The file, in reality, is very simple to read. And reading it will help you understand how the properties are defined.

# See also

1.  [The Update-TypeData cmdlet](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/update-typedata?view=powershell-6) (Microsoft Docs)
2.  [The Types.ps1xml file](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_types.ps1xml?view=powershell-6) (Microsoft Docs)

# Removing custom type data

Now that we know how to create and update type data, the next step for us is to learn to remove the type data. And removing the type data requires us to get the type data first. In this recipe, we learn the process to remove type data; whether it was updated using cmdlets or an XML.

# How to do it...

The first step is to understand that a cmdlet can output one or more types of objects. For instance, in our case, `Get-ChildItem` output `System.IO.DirectoryInfo` as well as `System.IO.FileInfo`. Let us learn to work with these guys.

1.  Get the type of the object returned by the cmdlet.

```
PS> Get-ChildItem | Get-Member | Select-Object TypeName -Unique
```

2.  There are two types returned. We created the custom members in the second type. Assign this to a variable.

```
PS> $TypeData = Get-ChildItem | Get-Member | Select-Object -ExpandProperty TypeName -Unique -Last 1
```

3.  Get the type data information. Expand its members to see if the custom members are shown.

```
PS> Get-TypeData -TypeName $TypeData | Select-Object -ExpandProperty Members
```

![](Images/cebc3c44-9586-4735-8b2e-b76d90b35c56.png)

4.  Now, remove the type data.

```
PS> Remove-TypeData -TypeName $TypeData
```

# How it works...

The process is straightforward. If you query the help information for the `TypeName` parameter of `Remove-TypeData`, you would notice that it accepts the type name accepts input via the pipeline by property value as well as the property name. Recall the recipe, *Understanding pipeline-enabled parameters*, and look at the object returned by `Get-TypeData`, for more insight.

The `Remove-TypeData` cmdlet removes the type data from the current session. This removal is as ephemeral as the type addition is. Therefore, the *default* types and formats are not permanently removed by the cmdlet; the reason why you can run this within PowerShell, without administrator privileges. Also remember that the underlying XML *files* are not deleted either: custom or stock.

# See also

1.  Recipe 5.8: Understanding pipeline-enabled parameters

That concludes the chapter. It is time to take a break, so it helps you assimilate what you learnt. Later, experiment with different data types, create variables, see what type of objects they contain, and what members each object contains. We did not explicitly talk much about variables in this chapter other than environment variables, but we used variables almost in every recipe in the chapter. Ponder over (or better yet, practically try out) these questions:

1.  What can be assigned to a variable?
2.  What does the variable contain; the entire object?
3.  Can I refer to one single property of the object that a variable contains, if at all it contains the entire object?
4.  Can I assign a certain member and not the entire object to a variable?
5.  What if the member is a whole object in itself? (Hint: Use `Get-Member` on the variable to find out.)
6.  What happens when I use `Select-Object` with `-ExpandProperty` and assign the value to a variable? What type is the variable then?

That would help you understand more about the variables, now that you have used them so much.

# Flow Control using Branches and Loops

In this chapter, we cover the following topics:

1.  Using If–ElseIf–Else conditions to control script flow
2.  Using Switch–Case conditions to control script flow
3.  Learning to use delays
4.  Writing a basic looping construct
5.  Writing a more complex loop on a predefined array
6.  Using the For loop construct
7.  Using the While loop construct
8.  Cleaning empty directories using the Do–While construct
9.  Cleaning empty directories using the Do–Until construct

# Introduction

Just like Working with Strings, this Flow Control is also a favourite part of PowerShell to me.

Most Linux administrators and Bash scripters would already be familiar with the concepts such as the loops and branches, that cover these recipes. The only main difference we would see is that we would deal with objects, and a more readable, streamlined process of scripting.

# Using If–ElseIf–Else conditions to control script flow

We have seen how the operators work. Try out more of the operators until it sort of becomes a second nature to you. Most of the flow control as well as filtration in scripts happen using these operators.

In this recipe we are going to look at conditional script flow, also known as *branching*. In essence, branching works on two conditions (correct: `$true` and `$false`). And this is generally achieved using two constructs:

1.  The If–ElseIf–Else construct
2.  The Switch–Case construct

In this recipe, we will give ourselves a simple problem to solve: find if today is a weekend.

# Getting Ready

These recipes require you to try them, in order to understand how they work. And these work better on an Integrated Scripting Environment (preferably, Visual Studio Code) than at the prompt. To run the scripts in VS Code, use the F5 key. Also, these recipes should work identically on Windows PowerShell 3.0+ as well: the syntaxes for these constructs are exactly the same in PowerShell and Windows PowerShell.

# How to do it...

Open a new PowerShell file in Visual Studio Code.

1.  Enter the following in the code pane to simply find if it is a weekend.

```
$Date = Get-Date

if ($Date.DayOfWeek -in 'Saturday', 'Sunday') {
    Write-Host 'We party on weekends!' -BackgroundColor Yellow -ForegroundColor Black
}
```

2.  If you would like to get an output on weekdays as well:

```
$Date = Get-Date
if ($Date.DayOfWeek -in 'Saturday', 'Sunday') {
    Write-Host 'It is a weekend!'
}
else {
    Write-Host 'It is a weekday.'
}
```

3.  If you would like to jazz it up a little, and use the whole of `if`–`elseif`–`else`:

```
$Date = Get-Date

if ($Date.DayOfWeek -in 'Saturday', 'Sunday') {
    Write-Host 'We party on weekends!' -BackgroundColor Yellow -ForegroundColor Black
}
elseif ($Date.DayOfWeek -eq 'Wednesday') {
    Write-Host 'Half the week is over, and I want to do so much more!'
}
else {
    Write-Host 'Work is worship. Ahem!'
}
```

In general, `Write-Output` is a better cmdlet to use than `Write-Host`. `Write-Host` writes the output *only* to the host; this output cannot be sent to anything else without manipulation. Use `Write-Host` only on occasions that need it.

# How it works...

Simple branching could work with just the If statement. The statement checks for truth, and executes the code block based on the outcome of the condition. In case of either–or, where there are only two conditions, use If–Else. When there are more than two possible outcomes, use If–ElseIf–Else. The `else` block is the catch-all.

# Using Switch–Case conditions to control script flow

If–ElseIf–Else work when you have outcomes coming in categories (weekdays being five days, weekends being two). When the outcomes are specific and/or too many in number, it could be a little tedious to use the  If–ElseIf–Else construct. To understand this better, let us give ourselves a scenario.

The dress code at your workplace is decided by a child, who likes everyone wearing the colours of the rainbow. Since she doesn't like anyone working weekends, is not a big fan of orange, and absolutely hates yellow, she has come up with the following scheme (she does not yet know of "Monday Blues"): Red on Mondays, Violet on Tuesdays, Indigo on Wednesdays, Blue on Thursdays, Green on Fridays and Orange during the weekends.

# How to do it...

This situation would require a whole round of If–ElseIf–Else statements to program. A more efficient way of handling the situation is to use the Switch–Case construct.

1.  Open a new PowerShell file and add the following content to it:

```
$Date = Get-Date

switch ($Date.DayOfWeek) {
    'Monday' { Write-Output 'Red' }
    'Tuesday' { Write-Output 'Violet' }
    'Wednesday' { Write-Output 'Indigo' }
    'Thursday' { Write-Output 'Blue' }
    'Friday' { Write-Output 'Green' }
    Default { Write-Output 'Orange' }
}
```

2.  If you would rather omit `Default` and use a wildcard matching for the weekends:

```
$Date = Get-Date

switch -Wildcard ($Date.DayOfWeek) {
    'Monday' { Write-Output 'Red' }
    'Tuesday' { Write-Output 'Violet' }
    'Wednesday' { Write-Output 'Indigo' }
    'Thursday' { Write-Output 'Blue' }
    'Friday' { Write-Output 'Green' }
    'S*' { Write-Output 'Orange' }
}
```

# How it works...

Like we can see, it is more efficient to write, execute as well as troubleshoot a Switch–Case construct in such situations, rather than writing a series of if–elseif–elseif–elseif–...–else statements. To define a catch-all action in Switch–Case, use `Default`.

The Switch–Case construct also supports wildcard (`-Wildcard`) and regex (`-Regex`). In general, it is not a good practice to omit `Default` unless *all* the possible outcomes have been covered.

The working of Switch–Case is simple: it checks the condition against *all the values* among the definitions, and whenever it finds a condition to be true, it executes the corresponding script block. Therefore if three conditions among five are met, the three script blocks will be executed. This is a little unlike If–ElseIf–Else, which exits out of the branching construct the moment the first `$true` is met and the script block is executed. Therefore, if you want only one outcome from the construct, consider adding the `break` keyword in every script block to break out of the construct the moment a `$true` is encountered. For example:

```
...
    'Monday' {
        Write-Output 'Red'
        break
    }
...
```

Of course, in this particular situation, it is not necessary, since the outcome would be exclusive.

# Learning to use delays

PowerShell usually runs one statement after another; the current statement must return the buffer (so to speak) for the next step to begin execution. However, in some cases, you still require a wait; situations where the buffer could be returned before the desired outcome is achieved.

While setting up something like this may require some manipulation, to keep it simple, let us just assume that we need five seconds to register what day it is (sure, disbelief works), before being instructed what to wear.

# How to do it...

Let us combine the two scripts from the previous recipe, *Using conditions to control script flow*.

1.  Open a new file and type the following:

```
$Date = Get-Date

if ($Date.DayOfWeek -in 'Saturday', 'Sunday') {
    Write-Host 'We party on weekends!' -BackgroundColor Yellow -ForegroundColor Black
}
elseif ($Date.DayOfWeek -eq 'Wednesday') {
    Write-Host 'Half the week is over, and I want to do so much more!'
}
else {
    Write-Host 'Work is worship. Ahem!'
}

Start-Sleep -Seconds 5

$Date = Get-Date

switch ($Date.DayOfWeek) {
    'Monday' { Write-Output 'Wear red.'; break }
    'Tuesday' { Write-Output 'Wear violet.'; break }
    'Wednesday' { Write-Output 'Wear indigo.'; break }
    'Thursday' { Write-Output 'Wear blue.'; break }
    'Friday' { Write-Output 'Wear green.'; break }
    Default { Write-Output 'Poor you, working today. Wear orange.'; break }
}
```

![](Images/9586edab-e1bb-444a-a119-28584db1a57b.png)

# How it works...

The reason this is a separate recipe is that it is part of flow control, and is useful in some specific situations. The `Start-Sleep` cmdlet accepts `Seconds` or `Milliseconds` as input, and waits for that amount of time before processing the next instruction.

# Writing a basic looping construct

Automation is perhaps only half-complete without loops. After all, the point of automation in most situations is making the computer do what is repetitive. There are six looping constructs in PowerShell in all:

1.  Looping using `Foreach-Object`
2.  The Foreach loop
3.  The For loop
4.  The While loop
5.  The Do–While loop
6.  The Do-Until loop

The `Foreach-Object` looping construct is perhaps the simplest of them all.

Let us imagine that we have a list of five guests to a certain event, and you would like to greet them each individually.

# How to do it

Let us assume that the guests are Mr Jain, Mr Jacobs, Ms Sanders, Mr Shah and Mr Hugo.

1.  Open a new file in Visual Studio Code and, in the script pane, type the following.

```
$GuestsRaw = Read-Host "Enter the guest names, separated by commas"
$Guests = $GuestsRaw -split ",$([regex]'[\s]*')"

$Guests | ForEach-Object { Write-Output "Welcome, $PSItem!" }
```

2.  Run the script, and at the prompt, type in the names of the guests:

```
PS> Mr Jain, Mr Jacobs, Ms Sanders, Mr Shah, Mr Hugo
```

# How it works...

You first take in the input through a prompt from the host. The raw guest list is taken in. PowerShell then splits the input string based on the commas and a regular expression match (necessary so it would work whether the input contains a space after the comma or not: not all users are alike). We use the `-split` and cast operators for the operation.

The loop part comes in at `Foreach-Object`. You pass the array object into the pipeline. The `Foreach-Object` cmdlet picks up the array, and processes one element at a time. When referring to the element within the loop, you use the `$PSItem` (a.k.a. `$_`) automatic variable, since the object has been passed through the pipeline.

# Writing a more complex loop on a predefined array

In the last recipe, Writing a basic loop construct, we wrote a simple loop by passing content through the pipeline. Now, let us consider that we have these same guests, but specific seats have been allotted to them. We would like to show the seats to the guests. You have the following table in a CSV format.

| **Name** | **Seat** |
| Mr Jain | A-12 |
| Mr Jacobs | C-28 |
| Ms Sanders | B-17 |
| Mr Shah | M-22 |
| Mr Hugo | E-08 |

# How to do it...

The assumption here is that each row has forty seats, and the aisle goes through the centre of the hall.

1.  If you have not cloned the repository, you could create your own CSV file. Either copy the comma-separated content from below, or create a CSV using PowerShell.

```
PS> @'
Name,Seat
Mr Jain,A-12
Mr Jacobs,C-28
Ms Sanders,B-17
Mr Shah,M-22
Mr Hugo,E-08
'@ | Out-File -Path './chapter-08/05-Write-GuestSeatDetails.csv'
```

2.  Open a new PowerShell file in Visual Studio Code and type the following script:

```
$Guests = Import-Csv './chapter-08/05-Write-GuestSeatDetails.csv'

foreach ($Guest in $Guests) {
    $RowIdentifier = [byte][char](($Guest.Seat -split '-')[0].ToUpper())
    $RowNumber = ($RowIdentifier - 64).ToString()

    switch -Regex ($RowNumber) {
        '1(1|2|3)$' { $RowNumber += 'th'; break }
        '.?1$'      { $RowNumber += 'st'; break }
        '.?2$'      { $RowNumber += 'nd'; break }
        '.?3$'      { $RowNumber += 'rd'; break }
        Default     { $RowNumber += 'th'; break }
    }

    $SeatNumber = ($Guest.Seat -split "-")[1]

    if ($SeatNumber -gt 20) {
        $Side = 'right'
    }
    else {
        $Side = 'left'
    }

    Start-Sleep -Seconds 1
    Write-Host "Welcome, $($Guest.Name)! " -NoNewline
    Start-Sleep -Seconds 1
    Write-Host "Your seat is in the $RowNumber row, to the $Side the aisle."
}
```

3.  Run the script.

![](Images/05449802-4f16-462e-a2a1-6ddfb8a26793.png)

# How it works...

The main idea here is the use of `foreach`. When using the Foreach loop construct, you refer to each element with a variable; variables are not identified with an index in this case. For every iteration, in our case, `$Guest` picks one value from `$Guests`, in sequence, so that the current element can be referred using `$Guest`.

The seat numbers have a pattern: an alpha row identifier, followed by a hyphen, followed by the numeric seat identifier.

The seat number is a string. We split it at `-`, pick the first element in the resultant array, convert it to uppercase (in case it already isn't), convert this letter to a character, and then, use the `[byte]` cast operator to find its ASCII identifier. And yes, we subtract 64 from it (so `A` becomes `1`).

To be able to use the number with switch–case without errors, we convert the number back to a string. We make the number friendly for use in a sentence. We take the second (numeric) part of the array to see which side of the aisle the seat is located on. We combine all these to get the resultant greeting-and-guidance strings, which are displayed after a delay of one second each.

# Using the For loop construct

The Foreach loop and the For loop are different in that the latter uses an index to perform operations. We need a variable to control the flow, whose values form a range. Let us re-implement the same solution as that in *Writing a more complex loop on a predefined array*, but with a For loop construct instead.

# How to do it...

The assumptions made are the same as that in *Writing a more complex loop on a predefined array*.

1.  Open a new file and paste the following content into it.

```
$Guests = Import-Csv './chapter-08/05-Write-GuestSeatDetails.csv'

for ($CurrentGuest = 0; $CurrentGuest -lt $Guests.Length; $CurrentGuest++) {
    $Guest = $Guests[$CurrentGuest]

    $RowIdentifier = [byte][char](($Guest.Seat -split '-')[0].ToUpper())

    $RowNumber = ($RowIdentifier - 64).ToString()

    switch -Regex ($RowNumber) {
        '1(1|2|3)$' { $RowNumber += 'th'; break }
        '.?1$'      { $RowNumber += 'st'; break }
        '.?2$'      { $RowNumber += 'nd'; break }
        '.?3$'      { $RowNumber += 'rd'; break }
        Default     { $RowNumber += 'th'; break }
    }

    $SeatNumber = ($Guest.Seat -split "-")[1]

    if ($SeatNumber -gt 20) {
        $Side = 'right'
    }
    else {
        $Side = 'left'
    }

    Start-Sleep -Seconds 1
    Write-Host "Welcome, $($Guest.Name)! " -NoNewline # Subexpression `$Guest.Name` to be computed first.
    Start-Sleep -Seconds 1
    Write-Host "Your seat is in the $RowNumber row, to the $Side the aisle."
}
```

2.  Run the script.

# How it works...

Some of you might be pointing out that the `foreach` construct was simpler than the `for` construct in this case, and you would be right. In my stint as an administrator, I may have used the for construct less than ten times over the last three years, compared to hundreds of times I used `foreach`. The For construct has its own uses; use with a predefined array is of the less-efficient ones.'

Regardless, `for` works as long as the object is an array. `$CurrentGuest` is the index we use, which ranges from 0 through the total elements in `$Guests` – 1\. The loop starts with the index being initialised at 0 in this case, and after every iteration of the script block, the index is incremented (`$CurrentGuest++`).

One operation where `for` would be more efficient than `foreach` is if every *alternate* guest had to be greeted (rude, I know). In that case, the third part of the definition of `for` would have been `$CurrentGuest += 2`.

`$CurrentGuest + 2` instead of `$CurrentGuest += 2` would make this loop infinite, since the value of `$CurrentGuest` would not be changed at all.

# Using the While loop construct

We shall create two scripts in this recipe: the first one to establish the similarities between For and While, and another to lay the foundation to understanding the Do–While and Do–Until constructs. This way, the learning would be incremental, and understanding, easier.

For the first script, the scenario is the same as described in the last recipe, *Using the For loop construct*. For the second, the task is to take the year number as input and find the date for Mothers’ Day in that year.

# How to do it

First, continue with the assumptions you had for the previous recipe.

1.  Open a new file and paste the following content into it.

```
$Guests = Import-Csv './chapter-08/05-Write-GuestSeatDetails.csv'
$CurrentGuest = 0

while ($CurrentGuest -lt $Guests.Length) {
    $Guest = $Guests[$CurrentGuest]

    $RowIdentifier = [byte][char](($Guest.Seat -split '-')[0].ToUpper())
    $RowNumber = ($RowIdentifier - 64).ToString()

    switch -Regex ($RowNumber) {
        '1(1|2|3)$' { $RowNumber += 'th'; break }
        '.?1$'      { $RowNumber += 'st'; break }
        '.?2$'      { $RowNumber += 'nd'; break }
        '.?3$'      { $RowNumber += 'rd'; break }
        Default     { $RowNumber += 'th'; break }
    }

    $SeatNumber = ($Guest.Seat -split "-")[1]

    if ($SeatNumber -gt 20) { $Side = 'right' }
    else { $Side = 'left' }

    Start-Sleep -Seconds 1
    Write-Host "Welcome, $($Guest.Name)! " -NoNewline
    Start-Sleep -Seconds 1
    Write-Host "Your seat is in the $RowNumber row, to the $Side the aisle."

    $CurrentGuest++
}
```

2.  Run the script; the output should be the same as that of the last recipe.
3.  Now, create a new PowerShell file and add the following code:

```
$Year = Read-Host "Enter the year (YYYY) you would like to find Mothers’ Day for"

$CurrentDay = Get-Date "01 May $Year"

while ($CurrentDay.DayOfWeek -ne 'Sunday') {
    $CurrentDay = $CurrentDay.AddDays(1)
}
$MothersDay = $CurrentDay.AddDays(7)

Write-Output "Mothers’ Day falls on $($MothersDay.ToLongDateString())."
```

4.  Run the script. Enter any year and you should get the date for Mothers’ Day for that year.

# How it works...

Every finite looping construct requires three things:

1.  The starting point
2.  The stopping point
3.  The way to proceed towards the stopping point

In case of the Foreach construct, the entire logic is pre-coded. It takes an entire array, finds the starting and stopping points, and moves towards the stopping point one step at a time. The For construct has these parameters declared in the loop declaration statements itself, each parameter separated by a semicolon.

The While loop is not very different. Its starting point is defined outside of the loop, the stopping point is the only condition passed, and the operation on the index is specified within the loop. These three parameters have been highlighted in the scripts. The initialisation should happen outside the loop so it is not modified during the course of the loop. The operation on the index should happen for every iteration so the loop moves in some direction. Therefore, this operation falls within the loop.

Be a little careful with the while loop; you are more prone to getting an infinite loop, because it is easy to forget to add the starting point or the operation to move towards the stopping point.

Now to Mothers’ Day. We first get the date object for the 1^(st) of May for that year, so we can manipulate it using its members. This date is the starting point. We then specify the condition, 'keep the loop going if the day is not a Sunday.' Then, we add one day, every iteration. After every iteration, the variable is checked against the condition. Finally, when the first Sunday is encountered, the variable comes out of the loop. We then add a week to it to find the second Sunday, and output the long date version of the value of `$MothersDay`.

# Cleaning empty directories using the Do–While construct

In the last recipe, we found the second Sunday of May using the year as input. We used a While loop for that. The While loop checks the condition before even starting the iteration. If the condition returns $false at the very beginning, the loop would not even begin; for instance, if you input the year as `2016`.

Do–While is a little different; the loop is executed once whether the condition is true or not. The condition is checked only *after* the first iteration.

The scenario for this recipe is that we want to delete all empty directories within a certain directory.

# Getting ready

In order to work with this recipe, let us create a few empty directories within `$HOME/random`. Use the input file that is part of the git repository of this book to get the directories created.

```
PS> Get-Content ./chapter-08/08-input-file.txt | ForEach-Object { New-Item $($PSItem -replace '\.', "$HOME/random") -ItemType Directory }
```

# How to do it...

If you run the following recipe within the `random` lab directory, all its empty subdirectories will be deleted.

1.  Open a new file and paste the following content into it.

```
do {
    $AllDirectories = (Get-ChildItem -Path $HOME/random -Recurse -Directory).FullName
    $EmptyDirectories = $AllDirectories | Where-Object {(Get-ChildItem $PSItem).Count -eq 0}
    $EmptyDirectories | Remove-Item
} while ($EmptyDirectories.Count -gt 0)
```

2.  Let us add some logging to it so we know what is happening.

```
$Iteration = 0
do {
    $AllDirectories = (Get-ChildItem -Path $HOME/random -Recurse -Directory).FullName
    $EmptyDirectories = $AllDirectories | Where-Object {(Get-ChildItem $PSItem).Count -eq 0}
    $EmptyDirectories | Remove-Item

    "Iteration $Iteration. Removed the following $($EmptyDirectories.Count) directories."
    $EmptyDirectories
    $Iteration++
} while ($EmptyDirectories.Count -gt 0)
```

![](Images/c622064b-ee5e-4f8c-8898-3b6fcb535608.png)

# How it works...

The execution is similar to the While construct, however, as shown by `Iteration 0`, the Do–While construct executes the script block once without checking the condition. In our case, we queried the empty directories within the loop. If we had placed this query outside of the loop, we would have had to place it within as well, for loop control. That is inefficient programming.

PowerShell found nine empty directories during the execution of the script block. When the condition check happened after the execution, `9` was evaluated to be greater than `0`. The loop ran again. This time, the value of `$EmptyDirectories.Count` was evaluated to be `4`. The loop ran again, and this time again, the value was `4`, greater than `0`; the condition was still `$true`. During the next run, `$EmptyDirectories.Count` was evaluated to be `2`, then `1`, and then, during the last run, `0`. At this time, the outcome of the condition became `$false`, and the loop exited. Essentially, the loop statement was, 'Go on *while* the count is *more than* zero.'

# See also

1.  Recipe 5.7: Taking actions on the returned objects

# Cleaning empty directories using the Do–Until construct

It is easy to confuse between Do–While and Do–Until, since they both share a lot of similarities. However, the difference between them is in fact, pretty clear. The Do–While loop executes as long as the outcome of the condition check is `$true`, and exits the moment it becomes `$false`. Do–Until is the opposite: the loop continues as long as the condition check returns $false, and stops the moment it the condition check returns `$true`.

Let us use the same scenario of cleaning up empty folders, but this time, use the Do–Until loop.

# How to do it...

You would need to rerun the command to create those empty directories.

1.  Open a new file and paste the following content into it.

```
$Iteration = 0
do {
    $AllDirectories = (Get-ChildItem -Path $HOME/random -Recurse -Directory).FullName
    $EmptyDirectories = $AllDirectories | Where-Object {(Get-ChildItem $PSItem).Count -eq 0}
    $EmptyDirectories | Remove-Item
    $Count = $EmptyDirectories.Count

    "Iteration $Iteration`nRemoved the following $Count directories. '$Count = 0' is $($Count -eq 0)"
    $EmptyDirectories
    $Iteration++
} until ($Count -eq 0)
```

2.  Notice the change in the behaviour this time and compare it with the run of Do–While.

![](Images/368f892a-96c9-4179-b2aa-56ae1c662904.png)

# How it works...

This time, it was made evident in the interactive output how it works. The first run happened without checking for the condition. At the end of the run, the condition was checked for. `9` is greater than `0`, and not equal. The outcome was `$false`, so the loop continued. It went on this way until the count came down to `0` (making the outcome of the condition `$true`), at which point, the loop exited. Essentially, the loop statement was, 'Go on *until* the count *becomes* zero.'

That concludes our chapter on flow control. I hope that you had a nice time learning the techniques, and that this chapter helps you with a good chunk of automation work you wish to carry out after learning to use PowerShell.

# Working with Strings

*Coming soon...*

# Performing Calculations

In this chapter, we discuss the following topics:

1.  Performing arithmetic operations
2.  Performing calculations on the output
3.  Working with the administrative constants
4.  Working with calculated properties
5.  Working with binary numbers
6.  Performing base conversions

# Technical Requirements

Here are the technical requirements to work with this chapter.

1.  PowerShell installed on the computer. Refer *Installation, Reference and Help* for steps.
2.  Visual Studio Code (recommended). Refer the recipe, *Installing Visual Studio Code* in the chapter, *Preparing for Administration using PowerShell*.
3.  Some throw-away files for the recipes. Use the script, `Initialize-PacktPs6CoreLinuxLab.ps1` from within the `ch05` directory of the book's GitHub repository.

The scripts used in this chapter are available at: [https://github.com/PacktPublishing/PowerShell-6.0-Linux-Administration-Cookbook/tree/master/ch09](https://github.com/PacktPublishing/PowerShell-6.0-Linux-Administration-Cookbook/tree/master/ch09).

# Introduction

Performing calculations is an integral part of automation. Of course PowerShell allows for this; it also takes things up a level by providing administrators with what is called Administrative Constants, which help ease calculations. We will look into these concepts in the following recipes. We will first look at common arithmetic operations, and then, move towards using the concepts on outputs using Calculated Properties like we saw in *Passing Objects Through the Pipeline*.

We will also look at cases where we could ease automation using binary numbers to identify flags, perform base conversion, and finally, use some of .NET Accelerators/cast operators to simplify scripting.

# Performing arithmetic operations

As administrators, we do not use much of arithmetic operations like the sin, cos, log and exp operations. However, it is possible to do all of them on PowerShell, since PowerShell can leverage .NET. In general, we may use these operations as administrators: `Abs` (as in absolute), `Ceiling`, `Floor`, `Round` and `Truncate`. In this recipe, we will use three of these methods, based on the scenario we have. Use of the other methods is very similar. Here is the scenario:

You have an application that creates logs throughout the day. These logs consume a lot of space. You would like to clean up logs that are between 30 and 31 days old. You are not allowed to use a dual condition for comparison.

Create a function that looks for files of 30 days of age. Your script should also say how much of the log space was cleared, rounded off to the nearest megabyte.

# Getting Ready

Run the script, `Initialize-PacktPs6CoreLinuxLab.ps1` from within the `ch05` directory of the book's GitHub repository. This is just so we have some files to work on. Next, run the script, `Set-LastWriteTime.ps1` from within the `ch09` directory of the repository.

If you would like to specify a path other than `~/random` for the content, add `-Path '//your/custom/path'` to the last line of the script. Ensure you do this in both the scripts.

# How to do it...

Navigate to the directory that contains your lab files; here is where all the action happens. If you did not specify a custom -Path when running the scripts, it should be `~/random`.

1.  Open the terminal and, using a code editor (`vi`, `nano` or VS Code), create a new file called `Clear-LogFiles.ps1`. Remember, CamelCase is just a convention.
2.  Enter the following content. I suggest typing it by yourself rather than copy-pasting it.

```
$Today = Get-Date
$TotalFileSize = 0

$FilesToDelete = Get-ChildItem . -Recurse -File | Where-Object {[math]::Floor(($Today - $_.LastWriteTime).TotalDays) -eq 30}

Write-Host "The following files will be deleted:"
Write-Host $FilesToDelete.FullName

foreach ($File in $FilesToDelete) {
    $TotalFileSize += $File.Length
    Remove-Item -Path $File -WhatIf
}

Write-Host "Total space cleared: $([math]::Round($TotalFileSize/[math]::Pow(1024, 2))) MB"
```

There is no need to actually delete the files. If you would like to anyway, remove the `-WhatIf` switch from line 12.

It is recommended to use Visual Studio Code to write this script since its IntelliSense auto-completion is very helpful. You could write this script at the terminal itself, in which case, use shorter versions of parameters and tab-completions as necessary.

# How it works...

The `[math]::` accelerator allows us to use the methods of the `System.Math` class. The `Round()` method accepts one or two arguments; in case of a single argument, the rounding happens to the nearest integer. The optional second parameter specifies the number of digits after the decimal point.

The `Pow()` method is almost self-explanatory: 1024² in our case. The `Floor()` method brought down numbers from 30.00 to less than 31, down to 30.

This is what we did:

1.  Listed out the files to delete: we subtracted the `LastWriteTime` from today, and performed a Floor operation on it since we were not allowed to use the `-and` operator.
2.  Displayed the files.
3.  We performed a remove operation on each of the files, while also adding the size of each of the files to `$TotalFileSize`.
4.  In the end, we divided `$TotalFileSize` by 1024² and rounded it off to the nearest MB.

# See also

1.  [System.Math Methods](https://msdn.microsoft.com/en-us/library/system.math_methods(v=vs.110).aspx) (Microsoft documentation)

# Performing calculations on the output

In the last recipe, we performed some nifty calculations on the objects themselves, and listed out files that were 30 days old. In the process, we also output the total amount of space to be cleared. In this recipe, we will output this information as a PowerShell object, and also, perform a small calculation during output. Here is the scenario:

Modify the script you created in Performing Arithmetic Operations to output a structured PSCustomObject. The output should have the total number of files in the directory, files that are 30 days old, and the total amount of space cleared (without any calculations). Also, separately, show the amount of space cleared by the cleanup, in MB.

# Getting ready

If you don't have the lab files or you deleted the files in the previous recipe, run the script, `Initialize-PacktPs6CoreLinuxLab.ps1` from within the `ch05` directory of the book's GitHub repository. Next, run the script, `Set-LastWriteTime.ps1` from within the `ch09` directory of the repository.

# How to do it

We will simply build on the previous recipe to save ourselves some time and effort. The changes from the script in the previous recipe have been emboldened.

1.  Open your favourite code editor, enter the following in the file and save the file as a `ps1` file.

```
$Today = Get-Date
$TotalFileSize = 0

$AllFiles = Get-ChildItem . -Recurse -File
$FilesToDelete = $AllFiles | Where-Object {[math]::Floor(($Today - $_.LastWriteTime).TotalDays) -eq 30}

foreach ($File in $FilesToDelete) {
    $TotalFileSize += $File.Length
    Remove-Item -Path $File -WhatIf
}

New-Object -TypeName psobject -Property @{
    TotalFiles = $AllFiles.Count
    FilesToDelete = $FilesToDelete.Count
    SpaceCleared = $TotalFileSize
}
```

2.  Call the PowerShell script.

```
& $HOME/Documents/code/github/powershell/ch09/02-Clear-LogFiles.ps1
```

Here is a glimpse of what that outputs.

![](Images/23e66bdf-6918-40c5-a598-2fcce9dc03f6.png)

3.  Now, pick just the `SpaceCleared` parameter.

```
(& $HOME/Documents/code/github/powershell/ch09/02-Clear-LogFiles.ps1).SpaceCleared
```

Notice the reference to the `SpaceCleared` property, and the output just before the prompt.

![](Images/f40eaf52-ba68-4227-8ced-94c8e9a8dfdf.png)

4.  Divide the output by 1024² to get the value in MB.

```
(& $HOME/Documents/code/github/powershell/ch09/02-Clear-LogFiles.ps1).SpaceCleared/[math]::Pow(1024, 2)
```

Similar to the one above; the total space cleared in MB.

![](Images/82f3680a-fbf5-46d3-9d2e-614f73356e49.png)

# How it works

Not only cmdlets and functions, but scripts also output objects. In the previous recipe, this was a string object; in this, it was a `PSCustomObject`. This way, even though the information gathered from both the recipes was the same, we were able to process the output further by running calculations on the fly.

# There's more

1.  Perform a `Round()` operations on `SpaceCleared` to get the output in MB, with two digits after the decimal point.
2.  Show the number of files that were omitted from deletion.

Assign the output object of the script to a variable: `$FileCleanupInfo = (& //path/to/02-Clear-LogFiles.ps1)` in order to make things easier.

# Working with Administrative Constants

The one thing that may have irked a few of us was how difficult it was to convert the `Length` property to MB. We had to go `[math]::Pow(1024, 2)`. Simplify the output of the previous recipe.

Also, imagine that you have these files loaded on a 250 GB SSD, and you would like to see what percent of space was cleared.

# Getting ready

If you don't have the lab files or you deleted the files in the previous recipe, run the script, `Initialize-PacktPs6CoreLinuxLab.ps1` from within the `ch05` directory of the book's GitHub repository. Next, run the script, `Set-LastWriteTime.ps1` from within the `ch09` directory of the repository.

# How to do it

We will use the same script as the previous recipe.

1.  Assign the object returned by the previous recipe to a variable.

```
$FileCleanupInfo = (& //path/to/02-Clear-LogFiles.ps1)
```

2.  Call the `SpaceCleared` property and divide it by Administrative Constants.

```
$FileCleanupInfo.SpaceCleared/1KB
$FileCleanupInfo.SpaceCleared/1MB
$FileCleanupInfo.SpaceCleared/1GB
```

Notice how the results are not just the numbers divided by powers of 1000.

![](Images/d156b713-9b47-4582-b8d7-5a9526c42753.png)

3.  To show how much of space got cleared from a 250 GB SSD:

```
($FileCleanupInfo.SpaceCleared)/(250*1e9)*100
```

An almost negligible number in our case, but here it is.

![](Images/5e03aa51-3d22-4c06-81fd-6b2eb4acd117.png)

# How it works

PowerShell has been created with administrators in mind. Given that we rely on a myriad of file operations on a regular basis, PowerShell contains administrative constants. These constants represent powers of 1024 (1024¹, 1024², 1024³...).

Hard drive and flash drive manufacturers usually use powers of 1000 to represent drive sizes. In our recipe, we use the scientific notation to convert the size of the drive into bytes.

# Working with calculated properties

If you read through the recipe, *Selecting columns from the output* in *Passing Data through the Pipeline*, you may skip this recipe. This recipe has been created in the interest of context as well as those who have skipped the said chapter/recipe.

Calculated properties is another form of performing calculations on the fly. Here is the scenario:

You need a report of all the files present in a certain directory, with the names of the files, the last modified date, the full paths and the sizes in MB.

# Getting ready

If you don't have the lab files or you deleted the files in the previous recipe, run the script, `Initialize-PacktPs6CoreLinuxLab.ps1` from within the `ch05` directory of the book's GitHub repository. Next, run the script, `Set-LastWriteTime.ps1` from within the `ch09` directory of the repository.

# How to do it

This is going to be a one-liner.

At the terminal, type the following and press Enter.

```
Get-ChildItem -file -rec | Select-Object name, lastwritetime, @{n = 'Size'; e = {[math]::Round($_.Length/1MB, 3)}}
```

# How it works

A calculated property takes in two things: the name of the property and the expression that would produce the desired result. Technically, this is a hashtable with `n` (or `Name`) and `e` (or `Expression`) being the two name-value pairs. The `Expression` in itself is a script block. When broken down into lines, the query looks like this:

```
Get-ChildItem -File -Recurse | Select-Object Name, LastWriteTime, @{
    Name = "Size"
    Expression = {
        [math]::Round($PSItem.Length/1MB, 3)
    }
}
```

Since we separated the `Name` and the `Expression` by a line, we don't need the semicolon anymore.

Calculated properties come in handy in situation where you don't really want to create a new script, but instead, want some information at the terminal itself, as though running a query. The value of Name is the name of the property, and the values in the column are determined by the expression.

# Working with binary numbers

In the interest of specificity, we are going to use the hexadecimal notification for this recipe. If you have worked with colours on your computer, chances are that you are aware of RGB. The levels of these primary colours are commonly represented as numbers ranging from 0 to 255 (24-bit colours). You may have also come across the hexadecimal representation of these colours, especially if you worked with HTML/CSS.

The scenario here is to write a simple script that converts any given hexadecimal code into decimal RGB.

# How to do it

We will assume that the input is going to be with or without the `#` (as in, `55bc9a` or `#55bc9a`).

1.  Open a new PowerShell file and type the following:

```
$Rgb = Read-Host "Enter the hexadecimal RGB value"
$TrimmedRgb = $Rgb.Substring($Rgb.Length - 6)

$R = $TrimmedRgb.Substring(0, 2)
$G = $TrimmedRgb.Substring(2, 2)
$B = $TrimmedRgb.Substring(4, 2)

"Here are the R, G and B levels for the supplied hex value:"
$R, $G, $B | ForEach-Object { [int]("0x" + $PSItem) }
```

2.  Run the script.
3.  Enter any valid hexadecimal RGB value, with or without the preceding `#`. Press Enter.

Here is an example.

![](Images/94d666b2-56dd-468c-8133-e16db174148d.png)

# How it works

First, how the script works to separate the R, G and B values. We first trim the hexadecimal string to exclude the `#` in case there is one. We need the last 6 characters of the string. Therefore, we PowerShell to begin the substring at 1 in case there is a `#` and 0 in case the string is 6 characters long. We then pick two characters at a time, starting at 0 (of the trimmed string), 2 and 4.

The conversion happens at the last line. First, we instruct PowerShell that we would like an integer output using the cast operator. Then, we tell PowerShell that the string is a hexadecimal string by adding `0x` to its beginning.

This is a simple way of converting hexadecimal into integer. Next, we will look at a few other conversions.

# Performing base conversion

The last recipe was a simple conversion using a cast operator and string addition. Next, we will look at converting an integer into multiple bases such as octal, hexadecimal and binary strings.

# How to do it

The input will be taken as a string. The output would also be string, but the octal, hexadecimal and binary representations. We will use a .NET accelerator for this.

1.  Open a new PowerShell file and type the following:

```
$InputString = Read-Host "Enter an integer"

Write-Host "Octal representation: " -NoNewline
Write-Host "$([Convert]::ToString($InputString, 8))"

Write-Host "Hexadecimal representation: " -NoNewline
Write-Host "$([Convert]::ToString($InputString, 16))"

Write-Host "Binary representation: " -NoNewline
Write-Host "$([Convert]::ToString($InputString, 2))"
```

2.  Run the script and enter an integer to get the octal, hexadecimal and binary representations of it.

Do not forget to try negative numbers as well.

![](Images/fc10c26b-d796-43b9-ac9b-15eba90fa9af.png)

# How it works

This recipe leverages the `[System.Convert]` .NET accelerator. The input and the output of the script are strings.

The `ToString()` method accepts input in the form of int64. When only one argument is passed, the integer is output as it is, except the object type is no more `int`, but `string`. The optional second argument passed to the method is the base: `2` stands for decimal, `8` stands for octal and `16` stands for hexadecimal.

# There's more

When I was learning PowerShell, I came across this recipe by Lee Holmes, where he showed how file attribute flags worked in PowerShell. To see what attributes are available in PowerShell for files and directories, and see their decimal and binary representations, enter the following at the PowerShell prompt.

```
PS> [Enum]::GetValues([System.IO.FileAttributes]) | Select-Object `
@{ n = 'Property'; e = { $_ } }, 
@{ n = 'Decimal'; e = { [int]$_ } },
@{ n = 'Binary'; e = { [Convert]::ToString([int]$_, 2) } }
```

This is what the command gives you.

![](Images/7dcf63f7-fa21-48b0-8d58-cb8e3480c39e.png)

That brings us to the end of this chapter. Basic arithmetic calculations have been omitted since they are no different from any of the most common languages.

# Using Arrays and Hash Tables

*Coming soon...*

# Handling Files and Directories

*Coming soon...*

# Building Scripts and Functions

*Coming soon...*

# Advanced Concepts of Functions

*Coming soon...*

# Getting Under the Hood: Debugging and Error Handling

*Coming soon...*

# Working with the Environment

*Coming soon...*

# Security in PowerShell

*Coming soon...*

# Enterprise Administration using PowerShell

*Coming soon...*

# Best Practices Round-up

*Coming soon...*

# PowerShell and Cloud Operations

*Coming soon...*

# Using PowerShell for SQL Database Management

*Coming soon...*