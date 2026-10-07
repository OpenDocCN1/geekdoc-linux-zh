# FOSS

and the sandboxes created by the user this same access.

When you run any of the install commands we will see in a few moments, you'll be prompted for your password. This is because Flatpak carries out system installs by default. What this means is that a program is installed for all users and that its files will be

Alternatively, if you use the --user flag then it's installed for your account (you shouldn't be prompted for a password). In this case it will be in $HOME/.share/Flatpak. This is useful if you don't have an administrator account, or if you want to run a bleeding-edge version of a program that's installed on your system.

The nice thing about Flatpak is that it works without root, you have the ability to run any application. Application has rights (through your user account) to create an on-screen window, which allows it to access resources. Flatpak as a user, resources from the host system are limited by what you could access with a "normal" program.

![](bbox=[0.638, 0.096, 0.935, 0.176])

![](bbox=[0.638, 0.184, 0.935, 0.276])

With the right tools, one could see LibreOffice running at the same time on the same machine. Is it magic? No, just Flatpak.

# QUICK TIP

If you installed Flatpak and your first program, you may find no icon for it in the system menu. Log out and log back again. This will reload the DATA environment which Flatpak added its own paths.

# Installing Flatpak

The first thing you need to install is Flatpak (the package format) Flatpak (the application). Most distros provide it in their repositories. If not, you can issue the following to get up and running:

+   sudo add-apt-repository ppa:flatpak/stable
sudo apt install flatpak

The version of Flatpak you use is the one that was packaged with the current version of your distro. If you're on a long-term support, like Ubuntu's 16.04 (Xenial), this may mean you won't get the latest features. Installing from the PPA is the recommended way to make sure you have the most recent version.

# Flatpak hubs

Flatpak seems to have collections of software, just like RPM or DEB repositories. Flatpak itself hosts the first hub you add: Flatpak. Register with your system user manager, or at the terminal using the following command:

```
flatpak remote-add --if-not-exists FlatHub https://flathub.org/repo/flatpakrepo
```

+   flatpak remove

# >> ROUNDING FLATPAK

This article comes at when Flatpak recently introduced two significant developments. The first is the project's v1.0 release, which came on August 20, 2018. As a benefit of this, the release brings the new "feature-complete" battery, with all the resources needed to run the apps. So what's next?

# On the menu

There are a couple of different application types that need to be packaged as Flatpak. The first is commercial applications. If it's feasible for the community to pick these apps, it's better to package everything else.

Flatpak is a single format for packages that work across distros, and the apps can help reduce support costs. Some examples of typical (free) programs in Flatpak include Steam, Slack, and Discord.

We continue in this article to discuss the support by most major GUI package managers. There are also tools to help develop package applications as Flatpaks. If you're a quick-coder, check the "Build" section of Flatpak (help) for some ideas on some of the tools you might use.

But the launch of installing Windows is arguably more interesting. The Wine project (www.winehq.org) allows Flatpak to run Windows applications by providing the connection between Linux and an installed Windows application in a format that is simple to import. It promises to do away with all the configuration-difficulty that comes with Wine-based installs, making it much easier.

Another type of application that makes a Flatpak useful is large applications. Complex size, making the updates painful and even less so. So, LibreOffice, which is a nearly 200MB app, and Android Studio, is included; both are available as somewhat convenient Flatpak.

Flatpak platforms are completely different OS (at least if they move them). Developers and users sure don't need to worry about the idiosyncrasies of one distro on top of another. Just wrap your app up as a Flatpak, and you're good to go.

# Installing Flatpak programs

Installing applications from Flatpak will feel very familiar if you are accustomed to using apt or either your

112