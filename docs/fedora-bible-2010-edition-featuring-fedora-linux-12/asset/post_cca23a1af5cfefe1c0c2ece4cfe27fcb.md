
The preceding message appeared when the AC power was disconnected, the power was reconnected, the laptop's lid was closed, and the lid was again opened.

## Fixing Your System with the FirstAidKit

Starting with Fedora 10, a new package called FirstAidKit helps you fix many issues that may strike your system. Built on top of a pluggable architecture, FirstAidKit is an automated recovery tool that applies common techniques to try to rescue your system.

To use the FirstAidKit, you first need to install the package:

```
# yum install firstaidkit
```

The most common way to run the program is to let it do what it thinks ought to be done—this is the whole automated part of the recovery tool. To do so, run the following command:

```
# firstaidkit -a
```

The program reports what it finds and the actions it takes.

To see a list of the available plug-ins, use the following command:

```
# firstaidkit --list
```

See [https://fedorahosted.org/firstaidkit/](https://fedorahosted.org/firstaidkit/) for more on the FirstAidKit.

## Choosing Software Alternatives

Because several software packages are available for every major service available in Linux (such as mail, printing, Java environments, and so on), there will be times when people using the system will prefer one service over another. Software packages that have been designed to work with the `alternatives` system can be configured in Fedora to let an administrator choose which of the alternatives to a particular service he or she wants to use by default.

### Selecting Java alternatives

If you are developing Java applications, an addition to the alternatives feature lets you switch between using a proprietary Java virtual machine (JVM) or using the Open JDK (openjdk), to using the GNU compiler for Java (gcj). Type the following to see which implementation of Java is currently in use on your system:

```
# alternatives --display java
```

### Selecting mail alternatives

The main use of the alternatives feature allows you to choose the mail transport services. If the sendmail, exim, and postfix Mail Transport Agents are installed, as an administrator you can choose which of those services is the default for sending and receiving e-mail.

As an administrator, you still need to configure each alternative service to work. Descriptions for configuring sendmail and postfix mail-transport agents are contained in Chapter 18.

In terms of defining which alternative you want for mail services, much of the work of creating links so that services can be chosen has already been done. Links relating to the default services are set up in the `/etc/alternatives` directory. Definitions that identify the alternative components of sendmail, exim, and postfix mail servers are contained in the `/var/lib/alternatives` directory.

Because much of the configuration has been done in advance, the first step in switching between the different mail services installed on your computer is only a couple of clicks away. To switch the default mail services on your computer, do the following:

- 1. To switch mail service, type **system-switch-mail**. The switcher window appears. Install the system-switch-mail package if this command is not installed.
- 2. Click on the service you want to switch to — Sendmail, Exim, or Postfix for mail, depending on which are installed. (If the one you want is already selected, you can just cancel.)
  - If the switch is successful, a pop-up window tells you to restart the new service.
- 3. Click OK to complete the switch and close the pop-up window.

The next time your computer boots, your new mail service takes over that service. All the links are in place and the startup scripts are changed. However, your system is still running the old service. The startup scripts for those services are in the `/etc/init.d` directory. They are as follows:

- **exim** — for the Exim mail service
- **sendmail** — for the Sendmail mail service
- **postfix** — for the Postfix mail service

To stop the old service so that the new one can take over, type the following (replacing *service* with the name of the service you want to stop):

```
# service servicename stop
```

To start the new service, type the following (replacing *service* with the name of the service you want to start):

```
# service servicename start
```

Providing that the new service was configured properly, it should now be available to the users of your computer.

### Using mail alternatives

The mail-transport services that the alternatives facility allows you to change rely on many of the same command names. For example, both Postfix and Sendmail have a `newaliases` command and `mailq` commands for updating aliases and checking the mail queue, respectively.

So, to the user, a change in the local mail service should (in theory) be nearly invisible. Users can send mail as they always did and the fact that a different mail transport is being used should make no difference.

## Using Security Enhanced Linux

Security Enhanced Linux (SELinux) is a security model that offers the potential to compartmentalize and secure every component of a Linux system (processes, files, directories, users, devices, and so on). Instead of the all-or-nothing, either-you-have-root-privilege-or-you-don’t approach to security in traditional Linux and UNIX systems, SELinux allows much finer granularity in how permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When you first install Fedora, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources the services can access.

Targeted policies limit the impact that an attack on the following services can have on your server as a whole: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies is practical today and provides further boundaries around what are already quite secure features. In most cases, you can use this policy set without modification.

This section sets out to give you an understanding of what SELinux is. It describes how to turn on SELinux in Fedora. Then it provides an overview of how Fedora’s targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

### Understanding Security Enhanced Linux

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root user) could override ownership, read/write/execute permissions, and processer scheduling priorities. Likewise, an attack on a Web server (httpd daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual host resources.

Organizations such as the United States National Security Agency (NSA) recognized the need to have operating systems in secure environments be able to separate information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, where the risk of one exploit taking down the whole operating system was unacceptable. The mechanism that NSA recommended to implement highly secure systems is referred to as *Mandatory Access Control* (MAC).

Traditional UNIX and Linux permissions are *Discretionary Access Controls* (DAC), because determining who has permission to access a resource is left to the discretion of the resource owner. For example, a user can make his files group- or world-readable or wrtable. With SELinux, however, a mandatory policy declares that even if a user set files in their home directory to world-readable or wrtable, other daemons, even running as root, would not be allowed to read or write to those files.

The SELinux project aims at providing MAC functionality in the Linux kernel. By implementing rules for what all operating system components can and can't do, an application that has security flaws or has been taken over for malicious intent can be contained. In other words, gaining control of one component of a system doesn't allow a cracker to take over the entire computer.

### Types and roles in SELinux

The mechanisms for implementing security rules in SELinux are referred to as *policies*. Any system that implements SELinux selects a particular policy (strict, targeted, and so on) that results in a consistent set of rules that meet the level of security required on the system. Fedora defaults to a *targeted* policy being turned on.

Using policy configuration files, SELinux implements two different security models: *Type Enforcement* (TE) and *Role-Based Access Control* (RBAC).

- **Type Enforcement** — Under the TE model, every object in the operating system is bound to a security attribute called a *type*. Every process is bound to a security attribute called a *domain*. This approach allows for very tight control of every object in the operating system. Every user is allowed to access objects in the operating system based on the domain in which he or she is allowed to operate.
- **Role-Based Access Control** — Using the RBAC model, SELinux lets each user operate in a specific role. The roles are arranged in a hierarchy, with specific permissions associated with each role provided by type enforcement.

In traditional Linux, a user is assigned a specific user ID (UID) and group ID (GID), which affords that user certain access to system resources. For instance, it gives the user certain rights to read, write, or execute files and directories based on whether that user owns the file or directory or is part of a group assigned to that file or directory.

In SELinux, a data file, directory, or application can have many more attributes associated with it. SELinux helps ensure that having access to the component wouldn't necessarily give that user control of that component in a way that could be exploited beyond what the security policies allow the user to do.
