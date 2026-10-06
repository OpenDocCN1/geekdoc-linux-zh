34. B. The responses linux emergency, linux s, and linux single start the system in runlevel 1. But, only linux emergency omits the initial processes. See Chapter 20 for more information.

35. A, B, D. All three Apache configuration files must exist; directives can be placed in any file. See Chapter 21 for more information.

36. C. The in.telnet program need not be, and is not, PAM-aware since it invokes the PAM-aware login program to establish a login session. See Chapter 22 for more information.

37. B, C. If the remote host is under the same administrative control as the local host, the remote host can be listed in /etc/hosts.eq; otherwise, it should be listed in /etc/hosts.lpd. The host name must be resolvable, but the host must not be listed in /etc/hosts; for example, the host could be resolved by DNS or NIS. See Chapter 23 for more information.

38. C. By default, authpriv messages are sent to /var/log/secure, so that ordinary users cannot view them. See Chapter 24 for more information.

39. A. Red Hat Linux places each ordinary user in a user private having 1 member. See Chapter 25 for more information.

40. A, C, D. These services can reveal useful information to a cracker. The identd service can help verify user identities across your network. See Chapter 25 for more information.

41. C. The --kickstart flag specifies non-interactive operation to the extent possible. The --expert flag lets you override probed information. See Chapter 26 for more information.

42. B, D. The xvidtune and xf86config tools let you vary operating characteristics that can damage a monitor. In the case of xf86config, any damage will occur after the tool is run, since the tool itself operates only in text mode. See Chapter 26 for more information.

43. A. The ~/.clients-default script checks the contents of the ~/.wm_style file. See Chapter 27 for more information.