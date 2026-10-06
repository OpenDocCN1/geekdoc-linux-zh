
## Selecting mail and printing alternatives

Beginning with Red Hat Linux 7.3, which was the first version to offer the alternatives feature, two major services were configured to use alternatives: mail transport and printing services. The alternatives facility system administrators choose the following, related to mail transport and printing: 

- **Mail Agent (MTA)** — If the sendmail, exim and postfix mail transport agents are installed, as an administrator you can choose which of services is the default for sending and receiving e-mail.
- **Printing** — If LPRng and CUPS printing services are installed, you can choose which service is the default for printing documents.

As an administrator, you need to configure each alternative service to work. Descriptions for configuring sendmail and postfix mail-transport agents are contained in Chapter 19. Information on setting up the CUPS printing service is in Chapter 17 (LPRng is no longer delivered with Fedora or RHEL, although it is still available from sites such as rpmfind.net; the feature for the printing service described below is not included with Fedora or RHEL, but can still be in earlier Red Hat Linux systems.).

In terms of setting up the alternatives side of mail services, the work of creating links so that the services can be chosen has already been done. Links relating to the default services are set up in /etc/alternatives directory. Definitions that identify the alternative components of sendmail, exim, and postfix mail servers are contained in the /var/lib/alternatives directory.

Because of the configuration has been done, the first step in switching between the different mail services installed on your computer is only a couple of clicks away. To switch the default mail services on your computer, do the following:

- 1. To switch mail service, use **system-switch-mail**. The switcher window appears.
- 2. Click on the service you want to switch — Sendmail, Exim, or Postfix for mail, depending on which are installed. (If the one is already selected, you can just cancel.).
- 3. Click OK to complete the switch and close the pop-up window tells to restart the new service.

The next time your computer boots, your new mail service takes over that service. All the links are in place and the start-up scripts are changed. However, your system is still running the old service. The start-up scripts for those services are in the /etc/init.d directory. They are as follows:

- **exim** — for the Exim mail service
- **sendmail** — for the Sendmail mail service
- **postfix** — for the Postfix mail service

To stop the old service so that the new one can take over, type the following (replacing service with the name of the service you want to stop):

```bash
# /etc/init.d/service stop
```

To start the new service, type the following (replacing service with the name of the service you want to start):

```bash
# /etc/init.d/service start
```

Providing that the new service was configured properly, it should now be available to the users of your computer.

## Using mail alternatives

The mail-transport services that the facility allows you to rely rely on many of the same command names. For example, Postfix and Sendmail have a newalias command and mailq commands for updating aliases and checking the mail queue, respectively.

So, to the user, a change in the local mail service (in theory) would be nearly invisible. Users can send mail as they always did and the fact that a different mail transport is being used should make no difference.

## Using Security Enhanced Linux

Security Enhanced Linux (SELinux) is a security model that offers the potential to compartmentalize and secure every component of a Linux system (processes, files, directories, users, devices, and so on). Instead of the all-or-nothing, either-you-have-root-privilege-or-you-approach to security in traditional Linux and UNIX systems, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

## Understanding Security Enhanced Linux

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

## Types and roles in SELinux

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, SELinux allows much finer granularity in permissions to run and alter components on the computer are handed out. With SELinux, you can drastically limit the damage caused by a person who cracks one part of a Linux system.

When install Fedora or RHEL, you have the opportunity to enable or disable SELinux. If enabled, the targeted policy is used by default. Targeted policies focus on services with vulnerable daemon processes, as well as the resources they can access.

Targeted policies limit the impact that an attack on the following services such as: Apache (Web server), Samba (Windows file and print sharing), FTP (file transfer protocol), NFS (network file system), and others. The targeted set of policies practical today provides further boundaries around what are quite secure features. In most cases, you can use this policy set without modification.

This section sets out your understanding of what SELinux is. It describes how to turn SELinux in Fedora or RHEL. It provides an overview of how Fedora's targeted policy is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

## Users in SELinux

The model that SELinux uses to define the rights that users have on an SELinux-enabled system can coexist with the existing Linux user model, rather than replace it. With SELinux enabled, users still have their accounts defined before in the /etc/passwd file. A user who is also assigned a role in SELinux is referred to as a Defined User.

Special identities in SELinux include the system_u (which is the user identity assigned to system processes) and user_u (which is the assignment used to indicate if general users, in particular those without specific identities, are allowed to use the feature in question). There is also a root identity, which is retained to allow compatibility with existing file contexts. This allows existing identities to remain valid if they have root as their user identity.

## Policies in SELinux

As noted earlier, with Fedora and RHEL the choice of turning either SELinux or turning it on. The values in the /etc/selinux/config file determine which type of policy is on (only the targeted policy is available by default, however a strict policy is also available) and when not SELinux is:

- enforcing: The current SELinux policy is on and is enforced.
- permissive: The current SELinux policy is on, but not enforced (so you only see warning messages describing how the policy would be enforced).
- disabled: SELinux is off, so only standard Linux permissions are enforced (as they were always on systems not including SELinux).

Fedora and RHEL contain a compiled policy for the targeted policy they deliver. For example, in the current version of Fedora /etc/selinux/targeted/policy/policy.23 is the compiled policy set used when that policy is active.
