# LISTING 18.9 continued

```
#
# Example:
# 12      SUPERVISOR    nw-adm    top-secret

12 SUPERVISOR adm *
```

Two notes of caution on the setting in section 12: It is possible that you could map the NetWare SUPERVISOR account to the Linux root account; however, if you do you will have to expose the root password in clear text until you start the nwserv daemon for the first time. It is therefore not a recommended practice to do this. The other caution is that the entry in the configuration file that comes with Red Hat is not useful. You should define a password when you start up mars_nwe for the first time and then either remove the entry from the nwserv.conf file or change it to an asterisk as shown.

Section 13 of the configuration file is used to map NetWare user accounts with accounts on your Linux system. This section of the file is shown in Listing 18.10 and is optional. The syntax for this section is the same as for section 12.

# LISTING 18.10 Section 13 of the /etc/nwserv.conf File—User Logins

```
# ===================================================
# Section 13: user-logins (optional)
#
# You can provide mappings from the regular login-names of your Linux-Box
# to "mars_nwe"-logins here.
# Every "mars_nwe"-user _must_ have a login-name on the Linux side (even
# if he can't log in into the account associated with the login-name,
# because you locked it with a "*") in order to 'own' files.
# If you specify a Linux-login that doesn't exist (one could think of a
# typo), the user will only have the minimal rights defined in
# sections 10/11.
#
# See section 12 for a description of the syntax.
#
# Unlike in section 12, you can define users with no password.
#
# Example:
# 13      MARTIN        martin
```