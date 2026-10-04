# Workstation Configuration

Workstations require most of the procedures outlined in the previous section “Reviewing General Practices for Server Configuration.” With workstations, however, new variables and requirements exist that pose an entirely different set of risks. One such variable is the graphical desktop, which is often a requirement for users. Another is the users themselves, who may or not intentionally act out of malice. Workstations require more logging than the average host, and also stricter requirements for password security.

# Desktops

Most workstations use desktop applications, which require X and a desktop manager. As previously mentioned, X, as well as any desktop management software, include a variety of applications to provide ease of use, and act as a friendly wrapper to many of the command line interface utilities used on Unix systems. Many of the applications included with X and desktop managers are installed with setuid bits, and execute with elevated privileges. This is often a requirement, as the design of Unix systems usually requires root access to some applications on the console.

The quantity of programs that are setuid and the risk of exploitation to gain elevated privileges locally are directly proportional. Also, as mentioned previously, errors occur when applications are written. Applications included with X and desktop managers that do not require elevated privileges either have their permissions changed if it will not adversely affect system performance, or should be removed.

Most desktop managers have a master configuration file on the host that permits the changing of the desktop environment and allows users to create their own configurations. Master configuration files should be altered to provide the minimum functionality required, preventing users from accessing unauthorized applications. The desktop manager and X server should also be configured to ignore any user-supplied configuration files, as this may give the user opportunity to gain unauthorized access to the system.

# Users

Users are another risk to the security of workstations, as they are often collaborators in compromising a system, either wittingly or unwittingly. Users without administrative access to a system may be dismayed by not being able to control the system, and exploit it to gain elevated privileges. Users with administrative