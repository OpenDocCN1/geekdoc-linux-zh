# Tutorial

# Firejail

You can see the Firetools window and an indicator for running the app in the system tray. To start any app, double-click it, or right-click and select Run. To monitor the running apps, right-click anywhere in the GUI and select Tools; all the running apps will be listed. To add a new app in Firetools, right-click the GUI and click Edit. Fill in the relevant details with the Command section value as the Firejail app name.

![](bbox=[0.2, 0.25, 0.56, 0.36])

# 05 Firejail features

The core technology behind Firejail is Linux namespaces. This lightweight visualisation technology is used as the first step of isolating the application.

The application container is built automatically when the sandbox starts and is destroyed when the sandbox is closed. The container is based on the file system currently installed. Firejail can attach a new TCP/IP networking stack to the sandbox, which comes with its own routing table, firewall and set of interfaces. This stack is independent of the host network stack. Networking operations supported by Firejail are: create new interfaces, move existing interfaces, assign addresses, hostname support, DNS support, Linux netfilter support and traffic shaping. The security profile file is located in the /etc/firejail directory and it describes the file system container, the security filters and network configuration. Appimage in Firejail does native format packaging. Add `--appimage` to mount the package and run it inside the sandbox. Firejail provides sandbox auditing and monitoring. It can point out gaps in security profiles. It provides options to track all the aspects of sandboxed applications. Monitoring of CPU/memory/bandwidth usage, tracing system calls, monitoring exec and fork events can be done using Firetools.

![](bbox=[0.2, 0.66, 0.56, 0.78])

# 06 Building custom profiles

All the custom profiles are stored within the `~/.config/firejail` directory. Pass Firejail command-line configuration options to the program using profile files. To build a custom profile for any app, first create the `.config/firejail` directory in your home directory:

```
$ cd ~ 
$ mkdir -p .config/firejail 
$ cd .config/firejail
```

Copy the default security profiles used by Firejail into this directory using:

```
$ cp /etc/firejail/app_name.profile app_name.
```

Here, `app_name` is the name of the app that you're creating a custom profile for. Now edit the new profile. You can comment out lines, blacklist directories, whitelist files, etc. Once modified, save and close the file, then start your application using:

```
$ firejail app_name
```

As a profile file with the same name as the application is present in the `~/.config/firejail` directory, it will be loaded. You can also create a profile file in the `/etc/firejail` directory. If the profile file with app name is present in both the directories, `~/.config/firejail` takes precedence over `/etc/firejail`. A profile file can also be created at a different location and specified while starting the application.

# 07 Building whitelist profiles

Whitelist profiles are more restrictive profiles and are built using Firejail's whitelisting feature. The custom profiles we created in the last section are also called blacklisted profiles, in that you blacklist the files the application is not allowed to use. Here, files that are necessary for the application to run are listed while everything else is not accessible. To create a whitelist profile, first create a simple Bash sandbox using `--private`:

```
$ firejail --private
```

Now start the app in this Bash session and list all the files within it using:

```
$ find .
```

Locate the directory/file that needs to be whitelisted, then exit and close the sandbox. Then, as before, create a new profile in the `~/.config/firejail` directory with the name `app_name.profile`. Enter the following as the content of the file:

```
$ app_name profile
mkdir ~/, directory_name
whitelist ~/directory_name
include /etc/firejail/whitelist-common.inc
include /etc/firejail/default.profile
```

Here, we are whitelisting `directory_name`, which is within the `app_name` directory structure. Session configurations are included from `whitelist-common.inc`.

# 08 Firefox sandboxing

Start a Firefox process by executing: