
[bob@pcbsd-2823] ~% 

+   - You are in! Log out.

```
[bob@pcbsd-2823] ~% logout
$
```

+   - You're back at the original shell prompt.

+   - From a remote machine, rlogin or rsh into the PC-BSD host you just enabled rlogin and rsh on.

For a Solaris server:

+   - Put the proper hostnames, IP addresses, and user permissions in your home directory's .login file and also in the /etc/hosts.equiv file. See the man pages for rlogin and rsh for directions.

+   - Check to see if rlogin is enabled and running with the following two commands:

```
bob@solaris:~$ svcadm enable svc://network/login:rlogin
svcadm: svc://network/login:rlogin: is not complete, missing general/complete (see svcs -xv svc://network/login:rlogin for details)
bob@solaris:~$ svcs -xv svc://network/login:rlogin
svc://network/login:rlogin (?)
State: -
Reason: Service is incomplete, defined only by profile /etc/svc/profile/generic.xml. To install this service, identify and install the package which provides the service's primary manifest. Use "pkg search 'svc://network/login\:rlogin'" to identify the package, then "pkg install <pkgs>" to install the indicated package.
Impact: This service is not running.
```

+   - Based on this, follow the instructions given in the svcs command as superuser.

```
bob@solaris:~$ su
Password: xxx
```

+   - Do a pkg search.

```
root@solaris:~# pkg search 'svc://network/login\:rlogin'
INDEX            ACTION VALUE            PACKAGE
```

+   - Now test both rlogin and rsh from a remote client machine to the server you just enabled and ran rlogin on.

## 23.3 USER ADMINISTRATION

The two most important objectives of user administration are service and security: providing a service to ensure that the user base has access to and can fully take advantage of the resources that a modern UNIX system can provide, and securing the files and processes that the user base needs to utilize those resources. Later in this chapter we go over some of the security methodologies that a system administrator can deploy to keep the system secure. In Chapter 25, we will also show security methods that revolve around virtualization technologies such as Jails, Zones, and VirtualBox VMs.

The traditional UNIX technique for providing service and security is through access privileges, for the individual user, the group, or all others on the system, to specific objects on the system, such as files. We showed how to set access privileges on files in Chapter 5, Sections 5.4 and 5.5. Designing and implementing user groups, and access privileges for user groups, are the most important parts of this technique.

Certainly, user account creation and configuration is the first step in providing maximum service and security to the user base.

In the following section, we concentrate on how to manage user accounts and groups on both PC-BSD and Solaris. These activities are done a significant time after the initial installation of your UNIX system, but that does not mean that they cannot be done during initialization of the system. The examples in the following section illustrate:

+   - Two simple cases of text-based user account creation and configuration on PC-BSD
+   - A GUI account creation and configuration in PC-BSD
+   - A text-based account creation and configuration in Solaris

Adding a new user account to a UNIX system generally involves the following steps:

+   1. Assign the user a username, a user ID number, and a primary group, and decide which other groups the new user should be a member of. Enter this data into the system user account configuration files.
+   2. Assign a password to the new account.
+   3. Create a home directory for the user.
+   4. Place default or custom initialization files in the user’s home directory.
+   5. Give the new user ownership of their home directory and initialization files.
+   6. Set other user account configuration details that would be useful for your system. This would include things like disk quotas and other resource limits, and system privileges.
