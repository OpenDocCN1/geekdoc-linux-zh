In section 13, you are permitted to map NetWare usernames to Linux names, and it is highly recommended that you do so. This is because the automatic mapping options, which I will describe next, have no way of using the Linux password and if automatic mapping is enabled, you will end up with a common password for all users.

If you do opt to use automatic mapping of NetWare usernames to Linux usernames, you will need to use section 15 of the configuration file, shown in Listing 18.11.

# LISTING 18.11 Section 15 of the /etc/nwserv.conf File—Automatic Mapping of NetWare Users to Linux Users

```
# ===========================================================================
# Section 15: automatic mapping of logins (decision required)
#
# If you have a large number of accounts on your Linux-machine, you may
# want to map all Linux-logins automatically to "mars_nwe"-logins.
#
# At this stage this section is only a quick hack to make life a bit
# easier for the administrator.
#
# WARNING: as there is no algorithm to convert the encrypted
# "Linux-passwords" into the encrypted format used by the DOS-clients (and
# therefore "mars_nwe"), you have to supply a common password for all
# automatically mapped users. This is a big security concern and you
# should never make this common password public (and, of course you
# should choose a sufficient 'secure' (read: difficult) password).
# Type the common password to grant access to the users login and the
# command "setpass" instead of telling the password to the user.
#
# Only those Linux-logins will handled automatically that don't have a
# "x" or "*" as their encrypted password.
#
#
# ===========================================================================
# Syntax:
# 15 FLAG DEFAULT_PASSWORD
#
# FLAG:
#
# 0 DON'T map the Linux-logins automatically to
# "mars_nwe"-logins (default)
#
# 1 YES, DO the automatic mapping and provide every login
# created this way with the common password given with
# "DEFAULT_PASSWORD"
#
# 99 re-read the logins from /etc/passwd and overwrite even the
```