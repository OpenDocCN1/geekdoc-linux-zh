by users or the operating system. If the system powers down without cleaning up these open files and unmounting file systems, errors can occur.

The commands to shut down Linux are:

/sbin/shutdown -h now causes a system halt

or

/sbin/shutdown -r now causes a system reboot

# MANAGING USERS AND GROUPS

A Linux system can have only a few users or can have hundreds of users, depending on the system's purpose. A network server that provides DHCP information may require only a few users, whereas a file server that provides file space for users may require many user accounts. One of the key administrative tasks with Linux is managing users and groups. The primary reason for user accounts is to verify the identity of each individual using a computer system. A secondary reason for user accounts is to permit the per-individual tailoring of resources and access privileges. Resources can include files, directories, and devices. Controlling access to these resources is a primary task of an administrator.

A user can represent either a person or an application. A user account that represents a person is used by an individual to gain access to the Linux operating system. An application such as Oracle has an account that is used to run the application. This practice is safer than using the root account to run everything because the permissions for the Oracle account can restrict access to areas that only Oracle uses, whereas the root account has no restrictions.

Groups are a logical expression of organization. Groups tie together users that have a common purpose. For example, an organization may have persons responsible for accounts payable and others responsible for payroll. By placing the user accounts in an accounts payable group common permissions can be given to all the members of that group. Members of the accounts payable group would not have access to the information and resources of the payroll group. Users within the same group have the same read, write, or execute privileges of group resources.

# Usernames

Each user account can have several properties assigned to it. The most commonly known properties are the username and the password.

Usernames have one major requirement: They must be unique. In other words, a username identifies only one account and no other user can have the same username. Because of this requirement, it is important to have a policy, or naming convention, that states how usernames will be created.

# Naming Conventions

Naming conventions make “thinking up” usernames much easier. By putting some thought into how usernames will be created, the same policy can be applied for all subsequent users. Naming conventions can be very simple or very complex. The convention used is a product of the type and structure of organization.

The size of an organization has to be considered because it determines how many usernames must be supported. For example, a very small organization could use first names as usernames, whereas a large organization would have to use something more unique.

In a very large organization it is appropriate to consider the organization structure when deciding on usernames. For example, using the department or plant name in the username would help make usernames unique and provide a way to identify where the associated user is. Some commonly used conventions include:

+   • First name (Huey, Dewey, Louie, etc.)
• Last name (Doe, Smith, Duncan, etc.)
• First initial followed by last name (ldoe, dsmith, lduncan, etc.)
• Department followed by the user’s first initial and last name (AP-ldoe, PR-dsmith, AR-lduncan, etc.)